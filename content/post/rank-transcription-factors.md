+++
title = "Rank transcription factors by evidence, not only by enrichment"
date = 2026-06-19T09:50:00
draft = false
authors = []
tags = ["Transcription factors", "Motifs", "Networks", "Functional genomics"]
categories = ["Genomics tips"]
summary = "A practical way to prioritize transcription factors by combining motif enrichment, expression, chromatin accessibility, timing and network position."

[header]
image = "research-senescence-systems.jpg"
caption = ""
preview = true
+++

Motif enrichment is a good starting point, but it is a weak ending point. A motif can be enriched because many related transcription factors share the same binding preference, because the region set is GC-rich, or because accessibility has changed without direct TF binding.

When I try to prioritize candidate regulators, I prefer to build an evidence table. Each transcription factor gets several independent scores, and the interesting candidates are those supported by multiple layers.

## Build An Evidence Table

Useful columns include:

- Motif enrichment in the genomic regions of interest.
- TF expression level in the relevant samples.
- TF expression dynamics across the experiment.
- Accessibility or footprint signal at motif instances.
- Histone-mark context around candidate binding sites.
- Co-occurrence with other motifs.
- Correlation with target gene modules.
- Timing relative to downstream transcriptional changes.

The point is not to make a perfect causal model. The point is to avoid over-ranking a TF because of one attractive metric.

## A Minimal Scoring Table

```r
tf_table <- data.frame(
  tf = motif_results$tf,
  motif_fdr = motif_results$fdr,
  motif_enrichment = motif_results$enrichment,
  expression_log2cpm = expression[ motif_results$tf, "mean_log2cpm" ],
  expression_logfc = expression[ motif_results$tf, "logFC" ],
  footprint_delta = footprints[ motif_results$tf, "delta" ],
  module_correlation = module_cor[ motif_results$tf, "cor" ]
)

tf_table$score <- with(tf_table,
  -log10(motif_fdr) +
  scale(motif_enrichment)[, 1] +
  scale(abs(expression_logfc))[, 1] +
  scale(abs(footprint_delta))[, 1] +
  scale(abs(module_correlation))[, 1]
)

tf_table <- tf_table[order(tf_table$score, decreasing = TRUE), ]
head(tf_table, 20)
```

This is deliberately simple. The score is not a truth machine; it is a prioritization device. It helps you decide which factors deserve manual inspection, validation or perturbation.

## Add Timing

Timing is often more informative than amplitude. A TF whose activity changes before a gene module may be more plausible as an upstream regulator than a TF that changes afterward.

```r
first_change <- function(x, threshold = 1) {
  idx <- which(abs(x) >= threshold)
  if (length(idx) == 0) return(NA_integer_)
  idx[1]
}

tf_table$tf_first_change <- apply(tf_activity_matrix, 1, first_change)
tf_table$module_first_change <- module_timing[tf_table$linked_module]
tf_table$precedes_module <- tf_table$tf_first_change < tf_table$module_first_change
```

This simple precedence flag can prevent a common mistake: calling a factor a driver when it is more likely a downstream marker of the state.

## Think In Families

Many motifs cannot distinguish close paralogs. AP-1, ETS, FOX, RUNX or TEAD family members often share similar motifs. When motif ambiguity is high, rank TF families first, then use expression, perturbation or ChIP/CUT&RUN evidence to nominate individual factors.

## The Trick

Keep the evidence table readable. A compact table with six well-chosen columns is more useful than a giant spreadsheet nobody can interpret. The best candidate regulator is rarely the one with the strongest motif enrichment alone; it is the one whose motif, expression, chromatin context, timing and network behavior tell a coherent story.

