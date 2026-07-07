# 05 Community visualization

> **Estimated time:** 25 minutes

---

# Why visualise microbial communities?

Thousands or even millions of sequencing reads may be classified during a metagenomics experiment.

Summarising these classifications in a meaningful way is essential before biological interpretation.

---

# Taxonomic summaries

Kaiju can summarise classifications at multiple taxonomic levels.

For example

- phylum;
- class;
- order;
- family;
- genus;
- species.

Depending on the biological question, different taxonomic levels may be most informative.

---

# Creating a taxonomic table

```bash
kaiju2table \
-t nodes.dmp \
-n names.dmp \
-r family \
-o readset_kaiju.table \
-v \
-p readset_kaiju.out
```

Experiment with different taxonomic ranks.

Questions to consider

- Which family is most abundant?

- Which phylum dominates?

- How much changes when moving from family to genus?

---

# Interactive visualisation with Krona

Krona provides an interactive hierarchical representation of community composition.

Generate the Krona input

```bash
kaiju2krona ...

ktImportText ...
```

Open the generated HTML file in your browser.

---

<!-- Figure: Krona screenshot -->

Navigate through the taxonomic tree.

Notice how relative abundances change as you zoom into different clades.

---

## Exercise

Identify

- dominant bacterial phyla;
- dominant genera;
- members of the Terrabacteria clade;
- the most abundant *Chlamydia* species.

You will encounter this organism again later during genome reconstruction.

---

# Interpreting abundance

Remember that sequencing reads measure **relative abundance**, not absolute cell numbers.

Changes in one organism automatically influence the relative abundance of all others.

---

```{important}
Community composition tells us **who is present**.

It does **not** directly tell us

- what organisms are doing,
- whether they are active,
- whether they interact,
- or whether they can be cultured.
```

---

# Looking ahead

Taxonomic classification analysed sequencing reads individually.

Next we will combine these reads into much longer DNA sequences using **metagenome assembly**.

This allows us to reconstruct microbial genomes rather than analysing individual reads.

---

## Biological takeaway

Taxonomic profiles provide an ecological overview of the microbial community and guide subsequent genome-resolved analyses.

---

---

⬅️ **Previous**: [04 Taxonomic classification](04-taxonomic-classification.md)

➡️ **Continue to**: [06 Metagenome assembly](06-metagenome-assembly.md)
