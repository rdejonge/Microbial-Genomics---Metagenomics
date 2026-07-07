# 02 Shotgun metagenomics versus amplicon sequencing

> **Estimated time:** 20 minutes

---

# Introduction

There are two principal strategies for studying microbial communities using DNA sequencing.

1. **Amplicon sequencing (metabarcoding)**
2. **Shotgun metagenomics**

Although both methods begin with DNA extracted from an environmental sample, they answer different biological questions and have different strengths and limitations.

Understanding these differences is essential before beginning the practical.

---

<!-- Figure: Shotgun versus amplicon workflow -->

# Amplicon sequencing

Amplicon sequencing targets a **single marker gene** that is shared by many organisms.

For bacteria this is almost always the **16S rRNA gene**.

The workflow is relatively straightforward:

Environmental sample

↓

DNA extraction

↓

PCR amplification of the 16S rRNA gene

↓

Sequencing

↓

Taxonomic classification

Because only one small genomic region is sequenced, amplicon sequencing is relatively inexpensive and allows many samples to be analysed simultaneously.

However, it provides only limited information about each organism.

---

## Advantages

- inexpensive;
- high sample throughput;
- well-established analysis pipelines;
- suitable for ecological surveys.

## Limitations

- only organisms amplified by the PCR primers can be detected;
- provides limited functional information;
- PCR amplification introduces biases;
- usually cannot reconstruct genomes.

---

# Shotgun metagenomics

Shotgun metagenomics sequences **all DNA molecules** present in a sample.

Instead of targeting one marker gene, sequencing reads originate from every genome in the microbial community.

This allows us to investigate both taxonomy and functional potential.

Because sequencing is performed randomly across genomes, sufficient sequencing depth is required to capture low-abundance organisms.

---

## Advantages

- detects bacteria, archaea, viruses and fungi simultaneously;
- enables functional analysis;
- enables genome reconstruction;
- avoids PCR amplification bias.

## Limitations

- considerably more expensive;
- computationally intensive;
- requires greater sequencing depth;
- assembly becomes difficult in highly complex communities.

---

# Comparison

| Feature | Amplicon sequencing | Shotgun metagenomics |
|-----------|-------------------|----------------------|
| Cost | Low | High |
| Taxonomy | Excellent | Excellent |
| Functional genes | Indirect | Direct |
| Genome reconstruction | No | Yes |
| PCR bias | Yes | No |
| Computational requirements | Low | High |

---

```{note}
Neither approach is universally "better".

The optimal sequencing strategy depends entirely on the biological question being asked.
```

---

# Which method would you choose?

Consider the following situations.

```{exercise}
You want to analyse bacterial diversity in 3,000 soil samples.

Which sequencing strategy would you choose, and why?
```

---

```{exercise}
You wish to reconstruct complete bacterial genomes from a plant root microbiome.

Which sequencing strategy would you choose?
```

---

```{exercise}
A previously unknown metabolic pathway is suspected to be present in a microbial community.

Which sequencing strategy would provide the strongest evidence?
```

---

# Looking ahead

During this practical we will work exclusively with **shotgun metagenomic data**.

The reason is simple:

Our goal is not only to determine **who is present**, but also to reconstruct microbial genomes and investigate their genetic potential.

This would not be possible using amplicon sequencing alone.

---

## Summary

You should now understand:

- how shotgun metagenomics differs from metabarcoding;
- why shotgun sequencing is required for genome reconstruction;
- the advantages and limitations of both approaches.

---

⬅️ **Previous**: [01 Learning objectives](01-learning-objectives.md)

➡️ **Continue to**: [03 The metagenomics workflow](03-metagenomics-workflow.md)