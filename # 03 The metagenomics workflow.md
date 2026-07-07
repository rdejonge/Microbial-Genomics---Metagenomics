# 03 The metagenomics workflow

> **Estimated time:** 15 minutes

---

# Introduction

Modern metagenomics experiments generate millions to billions of sequencing reads from complex microbial communities.

Extracting biological insight from these raw sequencing reads requires multiple computational steps, each addressing a different scientific question.

Rather than viewing these as independent software tools, it is useful to think of the workflow as a series of increasingly refined biological questions.

---

<!-- Figure: Complete metagenomics workflow -->

# The workflow

The workflow used throughout this practical is shown below.

DNA

↓

Shotgun sequencing

↓

Raw sequencing reads

↓

Taxonomic classification

↓

Metagenome assembly

↓

Read mapping

↓

Genome binning

↓

MAG quality assessment

↓

Biological interpretation

Each step produces information that is required for the next step.

---

# Step 1 — Taxonomic classification

**Question**

> Who is present?

Each sequencing read is compared against a reference database to determine from which organism it most likely originated.

Output:

- taxonomic assignments
- abundance estimates
- community composition

---

# Step 2 — Metagenome assembly

**Question**

> Can short sequencing reads be reconstructed into longer genomic fragments?

Assemblers combine overlapping sequencing reads into longer DNA sequences called **contigs**.

Output:

- assembled contigs
- assembly statistics
- N50
- contig length distribution

---

# Step 3 — Read mapping

**Question**

> How well does the assembly represent the original sequencing data?

The original sequencing reads are aligned back to the assembled contigs.

Output:

- mapping percentage
- per-contig coverage
- sequencing depth

Coverage information is an important feature used during genome binning.

---

# Step 4 — Genome binning

**Question**

> Which contigs belong to the same organism?

Genome binning algorithms combine multiple pieces of evidence, including

- coverage,
- GC content,
- tetranucleotide frequencies,

to group contigs into putative genomes.

The resulting genomes are called **metagenome-assembled genomes (MAGs).**

---

# Step 5 — MAG quality assessment

**Question**

> Can these reconstructed genomes be trusted?

MAG quality is evaluated using conserved single-copy marker genes.

Important metrics include

- completeness;
- contamination;
- strain heterogeneity.

These metrics help determine whether a MAG is suitable for downstream analyses.

---

```{important}
No single analysis step provides the complete answer.

Each contributes one piece of evidence that together allows us to interpret the microbial community.
```

---

# Throughout this practical...

Every time you run a program, ask yourself

1. What biological question is this step answering?

2. What information does it produce?

3. What assumptions does it make?

---

## Biological takeaway

Metagenomics is not a single analysis but a chain of complementary analyses that progressively transform raw sequencing reads into biological knowledge.

---

---

⬅️ **Previous**: [02 Shotgun versus amplicon sequencing](02-shotgun-vs-amplicon.md)

➡️ **Continue to**: [04 Taxonomic classification](04-taxonomic-classification.md)