+++
title = "A QC checklist before trusting ChIP-seq or ATAC-seq peaks"
date = 2026-06-19T09:10:00
draft = false
authors = []
tags = ["ChIP-seq", "ATAC-seq", "Quality control", "Epigenomics"]
categories = ["Genomics tips"]
summary = "A compact checklist for deciding whether ChIP-seq or ATAC-seq peak calls are biologically interpretable."

[header]
image = "teaching-epigenomics.jpg"
caption = ""
preview = true
+++

Peak calling is not the beginning of an epigenomic analysis. It is a consequence of many upstream choices: library quality, mapping behavior, duplication, background, blacklisted regions and replicate structure.

Before interpreting peaks, I like to ask a simple question: would I trust this experiment if I ignored the peak caller entirely?

## Start With The Library

Check these before any biological interpretation:

- Per-base quality and adapter content.
- Fraction of aligned reads.
- Fraction of uniquely mapped reads.
- Duplicate rate.
- Mitochondrial fraction, especially for ATAC-seq.
- Fragment length distribution.
- Enrichment in expected genomic compartments.

For ATAC-seq, fragment length is especially informative: nucleosome-free fragments and mono-/di-nucleosome periodicity tell you whether the assay captured chromatin structure.

## Remove Regions You Already Know Are Trouble

Some genomic regions accumulate signal for technical reasons across many assays. Excluding blacklisted regions is not cosmetic; it prevents a small number of problematic loci from dominating correlations, PCA, heatmaps and peak calls.

```bash
bedtools intersect \
  -v \
  -a peaks.raw.bed \
  -b hg38.blacklist.bed \
  > peaks.filtered.bed
```

## Compare Replicates Before Comparing Conditions

A good replicate correlation heatmap should mostly answer two questions:

1. Do biological replicates cluster together?
2. Do samples also separate by the biology you care about?

If batch dominates everything, do not hide it. Model it, visualize it and report how it affects the analysis.

```r
library(pheatmap)

# counts: peak/bin x sample matrix
log_counts <- log2(counts + 1)
cor_mat <- cor(log_counts, method = "spearman")

pheatmap(cor_mat, annotation_col = sample_metadata)
```

## Use Multiple QC Views

No single QC plot is sufficient. I usually want at least:

- A genome-wide correlation heatmap.
- PCA or MDS on normalized signal.
- Saturation analysis or subsampling.
- Average profiles around expected landmarks such as TSS.
- Example genome browser tracks at known positive and negative loci.

## The Trick

Do not wait for the final figure to inspect genome browser tracks. Looking at a few loci early often reveals problems that summary metrics miss: weird background, one dominant replicate, local mapping artifacts, or signal that is shifted relative to the expected feature.

