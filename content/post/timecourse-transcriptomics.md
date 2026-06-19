+++
title = "Think in trajectories, not only in contrasts"
date = 2026-06-19T09:00:00
draft = false
authors = []
tags = ["Transcriptomics", "Time course", "Functional genomics", "R"]
categories = ["Genomics tips"]
summary = "A reusable strategy for extracting dynamic programs from time-course transcriptomic data with splines, clustering and module-level interpretation."

[header]
image = "research-senescence-systems.jpg"
caption = ""
preview = true
+++

Differential expression is often framed as a list of pairwise contrasts: treated versus control, late versus early, condition A versus condition B. That is useful, but it can flatten a time-course experiment into disconnected snapshots.

When samples are ordered in time, a better first question is: which genes follow similar trajectories? A transient pulse, a delayed induction and a progressive repression can all have the same fold change in one contrast, but they usually mean different biology.

## A Practical Workflow

1. Normalize the expression matrix and remove lowly expressed features.
2. Visualize samples before modelling: boxplots, clustering, PCA or MDS.
3. Correct unwanted technical variation only after checking that it does not erase the biological design.
4. Fit a model that represents time as a continuous variable.
5. Cluster genes on fitted trajectories, not only on raw noisy values.
6. Interpret clusters with functional enrichment, upstream regulators and genomic context.

## Model Time Explicitly

For simple experiments, a design with categorical time points is enough. For richer trajectories, splines are often more useful because they let expression vary smoothly through time.

```r
library(limma)
library(splines)

# expr: normalized gene x sample matrix
# meta: sample table with columns condition, time, batch

design <- model.matrix(
  ~ condition + ns(time, df = 3) + condition:ns(time, df = 3),
  data = meta
)

fit <- lmFit(expr, design)
fit <- eBayes(fit)

topTable(fit, coef = grep("condition.*time", colnames(design)), number = 20)
```

This asks whether the shape of the trajectory differs between conditions, rather than whether two selected time points differ.

## Cluster The Signal You Actually Want

Clustering raw expression values can recover batch structure, outlier samples or mean-expression effects. A cleaner trick is to cluster centered fitted values.

```r
fitted_values <- fitted(fit)
dynamic_genes <- rownames(topTable(fit, number = Inf, sort.by = "P"))

mat <- fitted_values[dynamic_genes, ]
mat <- t(scale(t(mat), center = TRUE, scale = TRUE))

set.seed(1)
km <- kmeans(mat, centers = 8, nstart = 50)
```

Once trajectories are clustered, treat each cluster as a biological object: ask whether it is enriched for pathways, transcription factor targets, chromatin states, or genomic loci.

## A Useful Sanity Check

Always plot the average profile of each module together with individual gene profiles. If the module average looks beautiful but individual genes are chaotic, you may be looking at a statistical artifact.

```r
module <- names(km$cluster[km$cluster == 1])
plot(colMeans(mat[module, ]), type = "l", lwd = 3)
```

## Why This Helps

Trajectory-first analysis makes it easier to distinguish early regulators, late effectors, transient stress responses and stable cell-state markers. It also gives you a natural bridge toward module methods such as WGCNA, self-organizing maps or transcription factor network inference.

