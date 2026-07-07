# 09 MAG quality assessment

> **Estimated time:** 40–50 minutes

---

# Biological question

> **Can we trust the reconstructed genomes?**

Genome binning produces candidate genomes called **Metagenome-Assembled Genomes (MAGs)**.

However, these are computational predictions rather than experimentally verified genomes. Before using a MAG for downstream analyses we must evaluate its quality.

The most widely used software for this purpose is **CheckM**.

---

# Why do MAGs contain errors?

Genome reconstruction is difficult because:

- multiple organisms may have similar DNA composition;
- low-abundance organisms produce fragmented assemblies;
- repetitive DNA complicates assembly;
- closely related strains may become mixed.

As a result, reconstructed genomes may

- miss genomic regions,
- contain contaminating contigs,
- contain sequences from multiple strains.

---

<!-- Figure: Good MAG versus contaminated MAG -->

# CheckM

CheckM evaluates MAG quality using **single-copy marker genes**.

Many bacterial lineages possess genes that

- are highly conserved;
- occur only once per genome.

These marker genes provide an internal quality control.

---

# The three most important metrics

## Completeness

How much of the genome appears to have been recovered?

High completeness indicates that most expected marker genes are present.

---

## Contamination

Are marker genes present more than once?

Duplicated marker genes often indicate that contigs from different organisms have been grouped into the same MAG.

---

## Strain heterogeneity

Do duplicated marker genes originate from highly similar strains?

This helps distinguish contamination from naturally occurring strain variation.

---

```{note}
MIMAG guidelines classify MAGs according to completeness and contamination thresholds.

High-quality MAGs generally have:

- >90% completeness
- <5% contamination
```

---

# Running CheckM

```bash
checkm lineage_wf \
    -t 1 \
    -x fa \
    --tab_table \
    -f checkm.output \
    metabat_bins/ \
    checkm_results/
```

Depending on the size of the dataset this analysis may require substantial memory and computation time.

---

# Inspecting the output

The CheckM output contains several important columns.

| Column | Interpretation |
|----------|----------------|
| Completeness | Fraction of expected marker genes detected |
| Contamination | Estimated contamination from additional genomes |
| Strain heterogeneity | Similarity of duplicated marker genes |
| Marker lineage | Reference lineage used for evaluation |

---

## Exercise 1

Identify

- the most complete MAG;
- the least complete MAG;
- the most contaminated MAG.

---

## Exercise 2

Why does CheckM estimate contamination from duplicated marker genes?

Could there be biological explanations other than contamination?

---

## Exercise 3

Compare the MAG taxonomy with the organisms identified earlier using Kaiju.

Do both methods identify similar dominant organisms?

Can you locate the previously observed *Chlamydia* species?

---

# Improving MAGs

Poor-quality MAGs can often be improved by

- removing contaminating contigs;
- refining genome bins;
- increasing sequencing depth;
- combining multiple samples;
- using long-read sequencing.

Modern studies frequently perform several rounds of bin refinement before publication.

---

## Under the hood (optional)

CheckM assumes that conserved marker genes occur once per genome.

Although this assumption is remarkably robust, unusual evolutionary events such as gene duplication or genome reduction may occasionally violate it.

This is why CheckM provides **estimates**, not absolute truths.

---

```{important}
A MAG is always a computational reconstruction.

Never interpret a MAG without first considering its completeness and contamination.
```

---

## Biological takeaway

Genome reconstruction does not end after binning.

Quality assessment is essential before drawing biological conclusions from reconstructed genomes.

---

⬅️ **Previous**: [08 Genome binning](08-genome-binning.md)

➡️ **Continue to**: [10 Discussion and biological interpretation](10-discussion.md)
