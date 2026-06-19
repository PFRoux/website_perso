+++
slug = "Combined DNA and RNA sequencing for RNA editing event discovery"

# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Combined DNA and RNA sequencing for RNA editing event discovery"

# Project summary to display on homepage.
summary = "A stringent DNA/RNA-seq framework to distinguish genuine RNA editing events from sequencing, mapping and biological noise."

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "research-rna-editing.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["RNA editing", "editing", "RNA-seq", "DNA-seq", "Functional genomics", "genomics", "Bioinformatics"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "research-rna-editing.jpg"

+++


RNA editing refers to post-transcriptional processes that modify mature RNA sequences relative to their genomic DNA template. In animals, the best-characterized events are A-to-I substitutions mediated by ADAR enzymes and C-to-U substitutions mediated by APOBEC enzymes. These modifications can diversify transcript sequences, alter coding potential, affect RNA stability and contribute to gene regulation.

The rise of high-throughput sequencing made transcriptome-wide RNA editing screens possible, but it also exposed a difficult methodological problem. Apparent RNA-DNA differences can arise from true editing, inherited polymorphisms, sequencing errors, mapping artifacts, splice junction misalignment, paralogous regions or incomplete reference assemblies. During my PhD, the field was marked by strong discrepancies between studies, with estimates ranging from a few dozen to millions of edited sites depending on filtering strategies and experimental design.

To address this, I developed a stringent WGS/RNA-seq strategy for calling transcript-specific editing events while explicitly controlling for technical artifacts and biological replication. The core principle was simple: a candidate event should survive comparison to matched genomic DNA, sequencing quality filters, splice-aware mapping checks, local sequence context controls, and additional tests against unmapped genomic sequences to account for gaps or errors in the reference genome.

Applied to chicken liver, adipose tissue and embryos, this framework revealed that the number of high-confidence mRNA editing events is limited in this species, with fewer than 20 robust sites per tissue under stringent criteria. Several events were conserved with mammals, supporting the idea that core RNA editing mechanisms predate the sauropsid-synapsid divergence. The project also showed that editing levels can vary with tissue, genotype, age, diet and sex, linking RNA editing to biological context rather than treating it as a purely static sequence feature.

Beyond the biological findings, this project trained my approach to genomics: rigorous artifact control, matched DNA/RNA designs, biological replication, and explicit interpretation of uncertainty are essential when extracting biological meaning from high-throughput sequencing data.

{{< figure src="/img/Figure_RNA_editing_project.jpg" title="Impact of sequencing and mapping biases on mRNA editing discovery. Contribution of random or systematic sequencing biases and mapping artifacts to the false discovery of mRNA editing events using combined mRNA and DNA sequencings are given as a fraction (%) of the intial pool of candidate editing events subject to each source of bias in each tissue. WAT, white adipose tissue." numbered="true" >}}



[^1]: For a comprehensive overview the scientific debate around the extend of mRNA editing, please refer to [Schrider et al. 2011](https://www.ncbi.nlm.nih.gov/pubmed/22022455?dopt=Abstract), [Kleinman and Majewski 2012](https://www.ncbi.nlm.nih.gov/pubmed/22422962), [Lin et al. 2012](http://science.sciencemag.org/content/335/6074/1302.5), [Kleinman et al. 2012](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3425774/), [Piskol et al. 2013](https://www.ncbi.nlm.nih.gov/pubmed/23302925), [Lagarrigue et al. 2013](https://www.ncbi.nlm.nih.gov/pubmed/23410828)
