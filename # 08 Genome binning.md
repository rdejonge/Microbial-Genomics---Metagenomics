# 08 Genome binning

> **Estimated time:** 45–60 minutes

---

# Biological question

> **Which assembled contigs belong to the same microbial genome?**

Assembly produces thousands of contigs originating from many organisms.

Genome binning attempts to reconstruct individual genomes by grouping contigs that likely originate from the same organism.

---

<!-- Figure: GC-content versus coverage -->

# What information is used?

Genome binning combines multiple sources of evidence.

Most algorithms consider

- sequencing coverage;
- GC content;
- tetranucleotide frequencies;
- contig length.

Contigs sharing these characteristics are likely derived from the same genome.

---

# Manual inspection

Before using an automated algorithm, inspect the assembly yourself.

Calculate GC content

```bash
stats.sh \
    in=final.contigs.fa \
    gc=gc.txt \
    gcformat=4
```

Download

- gc.txt
- abundance.txt

Create a scatter plot

Coverage (x-axis)

GC percentage (y-axis)

---

## Exercise

Experiment with

- logarithmic coverage scale;
- minimum contig length;
- axis limits.

Can you visually identify clusters?

These clusters often correspond to individual genomes.

---

# Automated genome binning

Now compare your observations with MetaBAT.

Run

```bash
runMetaBat.sh \
    -t 2 \
    final.contigs.fa \
    megahit_sorted.bam
```

MetaBAT combines coverage and sequence composition to assign contigs into putative genomes.

The resulting bins are known as

**Metagenome-Assembled Genomes (MAGs).**

---

## Exercise

Determine

- number of MAGs;
- total number of contigs assigned;
- unbinned contigs.

Why might some contigs remain unbinned?

---

```{tip}
Very short contigs usually contain too little information for reliable binning and are therefore frequently excluded.
```

---

# Are these really genomes?

At this stage the MAGs are only **hypotheses**.

The next lesson evaluates

- completeness;
- contamination;
- strain heterogeneity.

Only after this quality assessment can we determine whether a MAG represents a reliable microbial genome.

---

## Under the hood (optional)

Modern binning algorithms increasingly combine:

- sequence composition;
- coverage;
- graph connectivity;
- machine learning.

MetaBAT remains widely used because it performs well while requiring relatively little manual parameter tuning.

---

## Biological takeaway

Genome binning transforms assembled contigs into candidate microbial genomes, providing the foundation for genome-resolved metagenomics.

---

---

⬅️ **Previous**: [07 Read mapping and coverage](07-read-mapping.md)

➡️ **Continue to**: [09 MAG quality assessment](09-mag-quality.md)