# 01 Learning objectives

> **Estimated time:** 10 minutes  
> **Prerequisites:** Linux command line, basic genomics, FASTA/FASTQ formats

---

# Why are we doing this practical?

Microbial communities are found everywhere: in soil, oceans, the human gut, on plant roots, and even in extreme environments. These communities often contain hundreds or thousands of different microorganisms that interact with one another and with their environment.

Traditionally, microbiologists studied microorganisms by isolating them in pure culture. Although this approach has yielded enormous insights, we now know that the majority of microorganisms cannot be cultured using standard laboratory techniques. As a result, studying only cultured isolates provides an incomplete view of natural microbial communities.

Metagenomics overcomes this limitation by sequencing DNA directly from environmental samples, allowing us to investigate entire microbial communities without first culturing individual organisms.

In this practical you will analyse a shotgun metagenomics dataset using many of the same computational approaches employed in modern microbiome research.

---

# Learning objectives

After completing this practical you should be able to:

## Understand

- explain the difference between **shotgun metagenomics** and **amplicon sequencing**;
- describe the major steps in a metagenomics workflow;
- explain why different computational tools are required throughout the analysis.

## Perform

- classify sequencing reads taxonomically;
- visualise microbial community composition;
- assemble a metagenome;
- map sequencing reads back onto an assembly;
- reconstruct metagenome-assembled genomes (MAGs);
- evaluate MAG quality using completeness and contamination estimates.

## Interpret

- recognise the strengths and limitations of different metagenomic approaches;
- critically interpret taxonomic and genome-resolved analyses;
- understand how computational choices influence biological conclusions.

---

# The four biological questions

Throughout the practical, every analysis step addresses one of four biological questions.

| Biological question | Computational analysis |
|---------------------|------------------------|
| **Who is present?** | Taxonomic classification |
| **What genomes are present?** | Metagenome assembly |
| **Which contigs belong together?** | Genome binning |
| **Can we trust these genomes?** | MAG quality assessment |

Notice that the software itself is **not** the objective. Instead, each program provides one piece of evidence that helps answer a biological question.

---

```{important}
Throughout this course, always ask yourself:

1. What biological question does this analysis answer?

2. Which assumptions does the method make?

3. How confident am I in the result?
```

---

# Learning pathway

By the end of Day 1 you will know **who is present** in your microbial community.

By the end of Day 2 you will have reconstructed microbial genomes from that same community and evaluated how reliable those genomes are.

---

# Before continuing

Before moving on, make sure you can answer the following questions.

```{exercise}
What is the difference between a microbial isolate and a metagenome?
```

```{exercise}
Why is DNA extracted directly from an environmental sample instead of culturing microorganisms first?
```

```{exercise}
Why might two different computational methods provide different answers for the same metagenomic dataset?
```

---

## Summary

After this lesson you should understand the goals of the practical and the biological questions that will guide each computational step.

⬅️ **Back to**: [Metagenomics Practical](README.md)

➡️ **Continue to**: [02 Shotgun versus amplicon sequencing](02-shotgun-vs-amplicon.md)
