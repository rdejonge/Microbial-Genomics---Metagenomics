# 10 Discussion and biological interpretation

> **Estimated time:** 30–40 minutes

---

# Congratulations!

You have completed a complete genome-resolved metagenomics workflow.

Starting with raw sequencing reads you have

✓ classified sequencing reads

✓ explored microbial community composition

✓ assembled a metagenome

✓ evaluated assembly quality

✓ reconstructed microbial genomes

✓ assessed MAG quality

This workflow forms the basis of many contemporary microbiome studies.

---

# Looking back

Throughout this practical we repeatedly asked four biological questions.

| Question | Analysis |
|-----------|----------|
| Who is present? | Taxonomic classification |
| What genomes are present? | Assembly |
| Which contigs belong together? | Genome binning |
| Can we trust these genomes? | CheckM |

Notice how each analysis depended on the previous one.

---

# Reflection

## Question 1

How did the Kaiju taxonomic profile compare with the reconstructed MAGs?

Did every abundant organism produce a high-quality genome?

If not, why?

---

## Question 2

Which analysis step introduced the greatest uncertainty?

Consider

- taxonomic classification;
- assembly;
- mapping;
- binning;
- quality assessment.

Discuss your reasoning.

---

## Question 3

Suppose you wanted to discover a completely new bacterial species.

Would taxonomic classification or genome assembly be more informative?

Why?

---

## Question 4

Imagine your metagenome originated from agricultural soil instead of a mock community.

Which additional challenges would you expect?

Consider

- species richness;
- strain diversity;
- sequencing depth;
- computational requirements.

---

# Limitations of metagenomics

Metagenomics is extremely powerful, but it also has limitations.

Sequencing DNA tells us

✓ what genetic material is present

It does **not** directly tell us

✗ which genes are expressed;

✗ which organisms are metabolically active;

✗ which organisms interact;

✗ whether detected DNA originates from living cells.

Answering these questions requires complementary approaches such as

- metatranscriptomics;
- metaproteomics;
- metabolomics;
- stable isotope probing;
- cultivation.

---

# Modern developments

Genome-resolved metagenomics continues to evolve rapidly.

Recent developments include

- hybrid short- and long-read assembly;
- Hi-C assisted genome binning;
- nanopore sequencing;
- strain-resolved metagenomics;
- graph-based assembly;
- machine-learning binning;
- pangenome-aware analyses.

Many of these methods build directly upon the workflow you completed during this practical.

---

```{seealso}
Although the individual software packages used in this practical may change over time, the underlying biological questions remain the same.

Understanding these questions will help you evaluate future computational methods.
```

---

# Key messages

Before leaving this practical, remember these five principles.

1. Every computational method answers a biological question.

2. Every computational method has assumptions.

3. Every result contains uncertainty.

4. Multiple complementary analyses provide stronger evidence than a single method.

5. Biological interpretation is always more important than software output.

---

# Further reading

- Quince et al. (2017) *Shotgun metagenomics, from sampling to analysis.*

- Chen et al. (2020) *Accurate and complete genomes from metagenomes.*

- Bowers et al. (2017) *Minimum Information about a Metagenome-Assembled Genome (MIMAG).*

---

## Final biological takeaway

The objective of metagenomics is **not** to produce taxonomic tables, contigs or MAGs.

The objective is to understand how microbial communities are assembled, function, and interact with their environment.

Everything you have done in this practical is a step towards answering that broader biological question.

---

⬅️ **Previous**: [09 MAG quality assessment](09-mag-quality.md)

🏠 **Return to**: [Metagenomics Practical](README.md)