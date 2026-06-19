+++
title = "ATAC-seq is more than a peak list"
date = 2026-06-19T09:30:00
draft = false
authors = []
tags = ["ATAC-seq", "Epigenomics", "Functional genomics", "Quality control"]
categories = ["Genomics tips"]
summary = "How to get more biological information from ATAC-seq by looking at fragments, nucleosomes, TSS profiles, footprints and genomic signal."

[header]
image = "research-atacseq-egattaca.jpg"
caption = ""
preview = true
+++

Many ATAC-seq analyses stop at peak calling: open regions in condition A, open regions in condition B, differential accessibility. That is useful, but it leaves a lot of information on the table.

ATAC-seq libraries carry several layers of signal: chromatin accessibility, fragment architecture, nucleosome positioning, transcription factor footprints, and sometimes even useful genetic information.

## Look At Fragment Classes

The fragment length distribution is one of the first things I inspect.

- Short fragments often reflect nucleosome-free accessible DNA.
- Mono-nucleosome fragments reflect protected DNA wrapped around one nucleosome.
- Di-nucleosome fragments give an additional periodicity check.
- Excess mitochondrial reads can indicate over-permeabilization or poor nuclei quality.

```bash
samtools view sample.bam \
  | awk '$9 > 0 {print $9}' \
  | sort -n \
  > fragment_lengths.txt
```

```r
frag <- scan("fragment_lengths.txt")
hist(frag[frag < 1000], breaks = 200, col = "grey70",
     xlab = "Fragment length", main = "ATAC-seq fragment sizes")
```

## TSS Profiles Are Fast And Informative

A strong ATAC-seq dataset should show enrichment around transcription start sites, but the exact profile depends on cell type and library preparation.

The goal is not to chase a universal perfect shape. The goal is to check whether samples are comparable and whether outliers are obvious before downstream modelling.

## Footprints Need Care

TF footprinting can be powerful, but it is easy to over-interpret. Tn5 insertion bias, motif redundancy, local accessibility and sequencing depth all affect footprint scores.

Before trusting a footprint:

- Check that the motif is expressed or the TF is biologically plausible.
- Compare footprint strength to chromatin accessibility.
- Inspect aggregate profiles around motif instances.
- Validate against ChIP-seq, CUT&RUN or perturbation data when possible.

## A Useful Mental Model

Think of ATAC-seq as a stack of questions:

1. Where is chromatin accessible?
2. How does accessibility change between conditions?
3. Which fragment classes drive the signal?
4. Which TF motifs are enriched or protected?
5. Do these features connect to expression, genotype or phenotype?

The peak list is only layer one.

