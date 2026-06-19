+++
slug = "In silico and statistical analyses of epigenomic data with UNIX and R"

# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Epigenomic data analysis with UNIX and R"

# Project summary to display on homepage.
summary = "Hands-on training in ChIP-seq, ATAC-seq and MNase-seq analysis, from sequencing quality control to peak calling, normalization and functional interpretation."

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "teaching-epigenomics.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["ChIP-seq", "ATAC-seq", "MNase-seq", "UNIX", "R", "Bioconductor"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "teaching-epigenomics.jpg"

+++


To support molecular and cell biologists in their quest for autonomy when dealing with bio-informatics, bio-statistics, genomics or systems biology, Pr Sandrine Lagarrigue - supported by [Agrocampus Ouest](http://formationcontinue.agrocampus-ouest.fr/infoglueDeliverLive/) - started offering a highly multidisciplinary and modular workshop dedicated to biologists ten years ago. I joined the teaching staff in 2014 and have since contributed to yearly training days on sequence bio-informatics and statistical analyses for genomic and epigenomic data.

The workshop dedicated to epigenomic data analysis addresses the following topics:

<div class="institution-badges">
  <span class="institution-badge"><i class="fa fa-university"></i> Institut Agro Rennes-Angers, continuing education Omic & NGS, since 2014</span>
  <span class="institution-badge"><i class="fa fa-university"></i> SIRIC Montpellier Cancer, ATAC-seq practical training, since 2025</span>
</div>

* Introduction to epigenome screening technologies (ChIP-seq, ATAC-seq, MNase-seq ...)
* Biases and noise in sequencing data
* Introduction to UNIX environment and Bash scripting
* Work on a cluster with job schedulers (SLURM and SGE)
* Use parallel environments
* Use genomic databases (Ensembl, UCSC)
* Quality check of ChIP-seq data
* Pre-processing and alignment of ChIP-seq data
* Peak calling
* Irreproducible discovery rate
* Use of R Bioconductor for functional genomics
* Normalization strategies for epigenomic assays (RPM, TMM, Lowess)
* Functional enrichment for epigenomic assays
* Motif enrichement analysis

The pedagogical objective is to help experimental biologists understand what each computational step actually measures. Rather than presenting pipelines as black boxes, the course links library preparation, assay-specific biases, alignment choices, normalization, peak calling and downstream interpretation to concrete biological questions.

In recent teaching activities, I have also extended this logic to ATAC-seq-focused training, including chromatin accessibility, nucleosome positioning, transcription factor footprinting and the interpretation of peak-centered functional enrichment analyses.

Below, you will find slides from our last ChIP-seq workshop (*in french*).

**Day 1**
<script async class="speakerdeck-embed" data-id="7815e4704cc34aa086bc8eff4ec8b36e" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

**Day 2**
<script async class="speakerdeck-embed" data-id="785d1031571840edb403807585c82bb9" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

**Bioconductor guide for ChIP-seq analysis**
<script async class="speakerdeck-embed" data-id="6c84a410aa0a4fc7a2dfb7dc3a8087ed" data-ratio="0.772830188679245" src="//speakerdeck.com/assets/embed.js"></script>
