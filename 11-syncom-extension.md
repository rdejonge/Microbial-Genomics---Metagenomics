# Extra task — Reconstructing a genome from a SynCom inoculum

**For students who finish the main practical early.** Apply the workflow you have already learned to a new dataset. Commands are provided only for the two new tools: **minimap2** and **FastANI**.

We recently prepared an inoculum containing approximately **40 microorganisms** for a synthetic community (SynCom) experiment. Can you recover a convincing genome from this sample, identify its closest culture collection relatives, and assess whether it received enough sequencing coverage?

## Input data

The paired-end reads are on the course server:

```text
/science/projects/courses/B-MBIMIGE/B-MBIMIGE2024_data/metagenomics_ronnie/aux/Syncom31_synt_inoculum_R1.fastq.gz
/science/projects/courses/B-MBIMIGE/B-MBIMIGE2024_data/metagenomics_ronnie/aux/Syncom31_synt_inoculum_R2.fastq.gz
```

The individual reference genomes and their list are in the same shared location:

```text
/science/projects/courses/B-MBIMIGE/B-MBIMIGE2024_data/metagenomics_ronnie/aux/references/
/science/projects/courses/B-MBIMIGE/B-MBIMIGE2024_data/metagenomics_ronnie/aux/references.txt
```

These are genomes from the [Arabidopsis culture collection dataset](https://zenodo.org/records/10992416). No download or unpacking is needed. I would recommend created symbolic links to these files from your CWD.

## 1. Assemble, map and inspect the community

Follow sections [06](06-metagenome-assembly.md), [07](07-read-mapping.md) and [08](08-genome-binning.md) of the main practical. Keep in mind this is a shared server. Be gentle with requested resources. Advice: maximum of 2 threads!

1. Assemble the paired-end reads using **MEGAHIT**.
2. Record total assembly length, number of contigs and N50.
3. Map the reads against the **complete MEGAHIT assembly** using **BBMap**, and create a sorted BAM file with **Samtools**.
4. Calculate the mapping percentage and per-contig mean depth using the tools from the practical. Retain the depth table for step 5.
5. Calculate GC content for the contigs and join the GC, length and depth information by contig identifier.

Prepare a **GC–abundance scatterplot for contigs longer than 5,000 bp**:

- **X-axis:** GC content (%).
- **Y-axis:** mean read depth (×), as a proxy for abundance. A logarithmic axis may help distinguish clusters; state the scale used.
- Each point represents one contig.

**Questions:** Can you distinguish potential genome clusters? Why might different organisms overlap in this plot? Does a highly abundant contig necessarily belong to a different organism from a less abundant one?

## 2. Bin the contigs and select one genome

Use **MetaBAT** to bin the assembly and **CheckM** to assess all bins, following sections [08](08-genome-binning.md) and [09](09-mag-quality.md).

Select the **single bin with the highest CheckM completeness**. Record its original identifier, length, contig count, completeness and contamination.

Highlight the selected bin's contigs on your GC–abundance plot. Keep the >5,000 bp filter for this plot only.

**Questions:** Do these contigs form a coherent cluster? Does the contamination estimate support treating the bin as one genome?

## 3. Find candidate relatives using minimap2
minimap2 documentation: [minimap2](https://github.com/lh3/minimap2/)

Use **minimap2** to align the selected bin to the combined culture collection reference file. Its sequence headers include the isolate name, for example `isolateA|contig1`, so you can identify the source genome of each match.

In the command below, replace `COMBINED_REFERENCES.fna` with the path to the combined reference file:

```bash
~/data/metagenomics_ronnie/aux/references/combined.fna
```

```bash
minimap2 -x asm5 -c -N 5 -t 2 COMBINED_REFERENCES.fna selected_bin.fa > bin_matches.paf
```

The `asm5` preset is intended for closely related assemblies. `-c` requests base-level alignments, and `-N 5` allows up to 5 secondary alignments per query, helping retain alternative candidate genomes.

Open the tab-separated PAF output in a spreadsheet (or in your terminal):

| Column | Meaning |
| --- | --- |
| 1 | Contig from your selected bin |
| 3 and 4 | Start and end of its aligned region |
| 6 | Matching reference sequence, including the isolate name |
| 10 | Number of matching bases |
| 11 | Alignment length, including gaps |

Identify a small shortlist of candidate isolates, preferably **2–5**, supported by long alignments across several bin contigs. Use column 6 to group matches by isolate. Avoid choosing candidates from a single short conserved match or simply counting alignment rows.

Very similar reference genomes can be difficult to distinguish, and even retained secondary alignments do not guarantee that every relevant relative appears.

## 4. Score the candidates using FastANI

**FastANI** estimates average nucleotide identity (ANI) between genomes [FastANI](https://github.com/ParBliSS/FastANI). Create a plain-text file named `candidate_genomes.txt`, containing the **absolute paths to the individual candidate genome FASTA files**, one per line, without a header.

Use the shared `references.txt` to find the filenames and absolute paths.

Compare your bin with the shortlisted genomes:

```bash
fastANI -q selected_bin.fa --rl candidate_genomes.txt -t 2 -o bin_ani.tsv
```

The output columns are:

| Column | Meaning |
| --- | --- |
| 1 | Query genome: your bin |
| 2 | Reference genome |
| 3 | ANI (%) |
| 4 | Number of matching query fragments |
| 5 | Total query fragments |

Calculate the **query alignment fraction** as column 4 divided by column 5. Consider this alongside ANI: high identity across only a small fraction of a bin is weaker evidence than high identity across most of it.

**Questions:** Which candidate is the strongest match? Is the difference from the next-best candidate convincing? Can you identify one isolate, or only a group of closely related isolates?

To help interpret close matches, also compare the candidate reference genomes **among themselves**, using the same list as both query and reference:

```bash
fastANI --ql candidate_genomes.txt --rl candidate_genomes.txt -t 2 -o candidates_ani.tsv
```

Ignore self-comparisons. Are the candidate genomes themselves nearly identical? Explain how this affects confidence in assigning your bin to a particular isolate.

## 5. Is the selected bin sufficiently covered?

Return to the reads mapped to the **whole MEGAHIT assembly** in step 1. Match the selected bin's contig identifiers to the per-contig depth table. Do not remap the reads only to this bin. `Why?`

Calculate the bin's **length-weighted mean depth**, using all its contigs, including those ≤5,000 bp and those with zero depth:

```text
Mean bin depth = sum(contig length × mean contig depth) / sum(contig length)
```

You can do this in a spreadsheet or on bash using [awk](https://www.geeksforgeeks.org/linux-unix/awk-command-unixlinux-examples/): multiply each contig's length by its depth, sum the products, and divide by the total bin length.

To put this coverage in context, calculate the length-weighted mean depth of the **whole assembly** in the same way, then report:

```text
Relative coverage = mean bin depth / mean assembly depth
```

This ratio describes coverage relative to the assembled metagenome. Also locate the bin's depth relative to the other clusters in your plot.

For judging assembly adequacy, use the **absolute bin depth in ×**, not this ratio. As a practical benchmark, approximately **30–50× coverage** is often a useful starting point for short-read prokaryotic genome assembly. For context, [Illumina's bacterial de novo assembly technical note](https://support.illumina.com/documents/products/technotes/technote_denovo_assembly_ecoli.pdf) recommends at least 30–40× good-quality reads and demonstrates assembly at 50×. Treat this as a guide, not a universal threshold, particularly for a metagenome.

**Discuss:**

- Is your bin's mean depth below, within or above the 30–50× benchmark? Does it seem adequate?
- Are individual contigs similarly covered, or does the mean hide poorly covered regions?
- Does your conclusion agree with the bin's completeness and fragmentation?
- Why might repeats, closely related strains or uneven coverage prevent a good assembly even at high mean depth?

Remember that depth measured on recovered contigs does not tell you the depth of genomic regions that failed to assemble.

## What to hand in

Prepare a short report containing:

1. Assembly statistics, mapping percentage and number of bins.
2. The GC–abundance plot, with the most complete bin highlighted.
3. The selected bin's identity, length, contig count, CheckM completeness and contamination.
4. A small table of candidate reference genomes, ANI values and query alignment fractions, plus a brief interpretation of the reference-to-reference comparisons.
5. Mean bin depth, mean assembly depth and relative coverage, with your assessment of whether coverage was adequate.

Finish with a short conclusion: **Which culture collection genome best matches your bin, how certain is that identification, and how well was this genome recovered?** Include the commands you used.

## Resources

- [Main practical](https://rdejonge.github.io/Microbial-Genomics---Metagenomics/)
- [Culture collection genomes](https://doi.org/10.5281/zenodo.10992416)
- [Minimap2 documentation](https://github.com/lh3/minimap2)
- [FastANI documentation](https://github.com/ParBLiSS/FastANI)
