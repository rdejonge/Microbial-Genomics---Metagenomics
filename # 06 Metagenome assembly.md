# 06 Metagenome assembly

> **Estimated time:** 40–50 minutes

---

# Biological question

> **Can we reconstruct longer genomic sequences from millions of short sequencing reads?**

Modern Illumina sequencers typically produce reads of only 150–300 nucleotides. Individual reads are therefore much shorter than the genomes we wish to study.

Metagenome assembly attempts to reconstruct these genomes by identifying overlapping sequencing reads and merging them into longer DNA fragments called **contigs**.

Unlike isolate genome assembly, metagenome assembly is considerably more difficult because reads originate from many different organisms that vary widely in abundance.

---

<!-- Figure: de Bruijn graph assembly -->

# Why assemble?

Taxonomic classification analyses each sequencing read independently.

Assembly provides additional information:

- longer sequences
- complete genes
- operons
- plasmids
- eventually complete genomes (MAGs)

Without assembly, genome reconstruction is impossible.

---

# The assembler: MEGAHIT

In this practical we use **MEGAHIT**, one of the most widely used metagenome assemblers.

MEGAHIT constructs a **de Bruijn graph**, where:

- nodes represent k-mers
- edges represent overlaps

The assembler then searches this graph for paths representing genomic sequences.

---

## Running MEGAHIT

```bash
megahit \
    -1 read1.fq \
    -2 read2.fq \
    -t 2 \
    -o megahit_out
```

The assembly may require 15–20 minutes.

During this time, inspect the documentation or discuss the questions below.

---

# Understanding k-mers

MEGAHIT performs assembly using multiple k-mer sizes.

Why?

Small k-mers

- connect reads more easily
- tolerate sequencing errors
- work well for rare organisms

Large k-mers

- reduce ambiguities
- improve contiguity
- separate repetitive regions

Modern assemblers therefore combine many k-mer sizes during a single assembly.

---

## Exercise

Inspect the logfile.

Answer:

- Which k-mer sizes were used?
- Why are multiple k values advantageous?
- What trade-offs exist?

---

# Assembly statistics

Several statistics describe assembly quality.

Important metrics include

- number of contigs
- total assembly size
- longest contig
- average contig length
- N50

---

## What is the N50?

The N50 is the contig length at which **50% of the assembled bases are contained in contigs of that length or longer.**

Larger N50 values generally indicate more contiguous assemblies.

However:

```{warning}
A large N50 does **not** automatically imply a biologically better assembly.

Misassemblies can also increase the N50.
```

---

## Exercise

Determine

- total number of contigs;
- assembly size;
- longest contig;
- N50.

Discuss which statistics are most informative.

---

## Under the hood (optional)

Assembly is fundamentally a graph problem.

Modern assemblers simplify enormous de Bruijn graphs by removing sequencing errors, bubbles and dead ends before extracting the most likely genomic paths.

Understanding these graph simplifications explains why assembly quality depends strongly on sequencing depth and community complexity.

---

## Biological takeaway

Assembly transforms millions of short reads into biologically meaningful DNA fragments that can subsequently be grouped into microbial genomes.

---

---

⬅️ **Previous**: [05 Community visualisation](05-community-visualization.md)

➡️ **Continue to**: [07 Read mapping and coverage](07-read-mapping.md)