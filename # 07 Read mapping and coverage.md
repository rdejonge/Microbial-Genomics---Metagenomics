# 07 Read mapping and coverage

> **Estimated time:** 30–40 minutes

---

# Biological question

> **How well does the assembly represent the original sequencing data?**

After assembly we want to know whether the reconstructed contigs explain most of the sequencing reads.

To answer this question, we align the original reads back to the assembly.

---

# Why map reads?

Read mapping serves several purposes.

It allows us to

- evaluate assembly quality;
- calculate sequencing depth;
- estimate contig abundance;
- generate coverage profiles used during genome binning.

Coverage becomes one of the strongest signals for separating genomes.

---

# Building the index

Before reads can be aligned, BBMap builds an index of the assembled contigs.

```bash
bbmap.sh ref=final.contigs.fa
```

---

# Mapping reads

```bash
bbmap.sh \
    in=read1.fq \
    in2=read2.fq \
    out=megahit.sam
```

The resulting alignments are stored in SAM format.

Because SAM files are very large, they are normally converted to compressed BAM files.

```bash
./sam2bam.sh
```

---

# Mapping statistics

Calculate mapping statistics

```bash
samtools flagstat megahit_sorted.bam
```

Important questions include

- What proportion of reads mapped?
- How many read pairs aligned properly?
- How many reads remained unmapped?

---

```{note}
Environmental soil metagenomes often show mapping rates below 30%.

Highly complex microbial communities are much harder to assemble completely than simple mock communities.
```

---

## Exercise

Inspect the output.

Discuss:

- Does a low mapping percentage necessarily indicate a poor assembly?
- What biological factors could reduce mapping?

---

# Coverage

Next we calculate per-contig coverage.

```bash
pileup.sh \
    in=megahit_sorted.bam \
    out=cov.txt
```

Convert to abundance table

```bash
awk '{print $1"\t"$5}' cov.txt \
| grep -v '^#' \
> abundance.txt
```

---

## Exercise

Download the abundance file.

Calculate

- mean coverage;
- median coverage;
- minimum;
- maximum.

Visualise the distribution.

Do you observe a long tail?

---

## Under the hood (optional)

Coverage reflects how many sequencing reads align to a particular genomic position.

Organisms with high abundance in the community therefore tend to produce contigs with higher coverage than rare organisms.

Genome binning algorithms make extensive use of this property.

---

## Biological takeaway

Coverage provides quantitative information about microbial abundance and becomes an essential feature for reconstructing genomes.

---

---

⬅️ **Previous**: [06 Metagenome assembly](06-metagenome-assembly.md)

➡️ **Continue to**: [08 Genome binning](08-genome-binning.md)