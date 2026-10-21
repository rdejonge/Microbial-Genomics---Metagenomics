# 04 Taxonomic classification

> **Estimated time:** 35–45 minutes

---

# Biological question

> **Who is present in the microbial community?**

Taxonomic classification is usually the first analysis performed on shotgun metagenomic data.

Unlike genome assembly, taxonomic classification works directly on the sequencing reads and therefore provides a rapid overview of community composition.

---

# Kaiju

In this practical we use **Kaiju**.

Unlike many other classifiers, Kaiju compares sequencing reads against a **protein database**.

Because protein sequences are generally more conserved than DNA sequences, Kaiju often detects more distant evolutionary relationships than nucleotide-based methods.

Today, Kraken2 is another widely used alternative.

---

```{note}
Different taxonomic classifiers may produce slightly different results because they use different databases and classification strategies.
```

---

# Dataset

Download the metagenomics dataset from this location: 
https://carpentries-lab.github.io/metagenomics-workshop/data/index.html

Unzip the 

The dataset contains paired-end Illumina sequencing reads.

---

# Running Kaiju

For this practical the classification has already been performed because the reference database is very large.

The command that was executed is

```bash
kaiju \
-t nodes.dmp \
-f kaiju_db_progenomes.fmi \
-i R1.fq \
-j R2.fq \
-z 24 \
-o JC1A.kaiju.out
```

Kaiju output was subsequently converted to a classification table using kaiju2table (JC1A.kaiju.genus.table) and to a krona file kaiju2krona (JC1A.kaiju2krona.html). 

Here we explore the raw kaiju output, the kaiju table and the krona file.

---

# Understanding the output

Each classified sequencing read receives

- a taxonomic identifier,
- the matching protein,
- the matching organism,
- alignment information.

Before interpreting any biological result, always inspect

- classification rate,
- database used,
- proportion of unclassified reads.

---

## Exercise 1

Determine the percentage of classified reads.

Hint:

Use the Kaiju documentation together with the logfile.

---

## Exercise 2

Inspect the first five classified reads.

For each read determine

- matching protein;
- matching organism;
- taxonomic identifier.

---

## Exercise 3

Locate the first matched protein in the reference database.

Identify

- protein length;
- alignment position;
- location of your sequencing read.

---

# Taxonomic classification with Kaiju: a one-hour practical.

A taxonomic assignment is **not** proof that an organism is present.

It represents the best database match for that sequencing read.

Confidence therefore depends on

- database completeness,
- read length,
- sequence conservation,
- sequencing quality.

---

```{warning}
A large fraction of unclassified reads does not necessarily indicate poor sequencing quality.

It mostly reflects organisms that are absent from the reference database.
```

---

## Biological takeaway

Taxonomic classification provides a rapid overview of community composition, but every classification depends on the available reference genomes.

---

---
