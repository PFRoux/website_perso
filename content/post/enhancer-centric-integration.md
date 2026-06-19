+++
title = "Make enhancer analyses gene-aware, but not gene-blind"
date = 2026-06-19T09:40:00
draft = false
authors = []
tags = ["Enhancers", "ChIP-seq", "ATAC-seq", "Transcriptomics", "GenomicRanges"]
categories = ["Genomics tips"]
summary = "A practical framework for integrating enhancer states, chromatin signal and gene expression without pretending that nearest gene assignment solves everything."

[header]
image = "research-p53-e4f1-metabolism.jpg"
caption = ""
preview = true
+++

Enhancer analyses often fall into two traps. The first is to treat enhancers as isolated genomic intervals. The second is to assign every enhancer to the nearest gene and pretend the problem is solved.

A better compromise is to make enhancer analyses gene-aware, but not gene-blind.

## Classify Enhancers Before Linking Them

Start by defining interpretable enhancer classes. For example:

- Active enhancers: H3K27ac and H3K4me1 positive.
- Poised enhancers: H3K4me1 positive, low H3K27ac.
- De novo enhancers: inactive at baseline, active after stimulation.
- Remnant enhancers: activity decreases but some chromatin memory remains.
- Stable enhancers: active across the experiment.

These classes make downstream plots much easier to interpret than one giant enhancer table.

## Link With Several Rules

Nearest gene is a useful baseline, but it is not enough. I like to keep multiple gene-linking strategies side by side:

1. Nearest transcription start site.
2. Genes within a fixed window, such as 50 kb or 100 kb.
3. Genes whose expression changes with enhancer activity.
4. Promoter-capture Hi-C, Hi-C or curated enhancer-gene links when available.

```r
library(GenomicRanges)

# enhancers: GRanges with class and signal columns
# tss: GRanges with gene_id

nearest_idx <- nearest(enhancers, tss)
enhancers$nearest_gene <- tss$gene_id[nearest_idx]
enhancers$distance_to_tss <- distance(enhancers, tss[nearest_idx])
```

## Add Expression Without Overclaiming

Once enhancers are linked to candidate genes, ask whether enhancer classes show coherent expression patterns.

```r
linked <- data.frame(
  enhancer_class = enhancers$class,
  gene_id = enhancers$nearest_gene,
  distance_to_tss = enhancers$distance_to_tss
)

linked <- merge(linked, expression_results, by = "gene_id")

boxplot(logFC ~ enhancer_class, data = linked,
        las = 2, ylab = "Gene expression log2 fold-change")
```

If de novo enhancers are associated with induced genes, that supports a regulatory relationship. It does not prove that each enhancer controls the assigned gene.

## Make Metaprofiles For Each Class

Metaprofiles are useful because they show whether enhancer classes behave globally as expected.

For each enhancer class, compare:

- H3K27ac signal.
- H3K4me1 signal.
- ATAC-seq accessibility.
- TF binding or motif footprinting.
- Distance to TSS.
- Associated gene expression.

The best enhancer stories usually combine local examples and global class-level behavior. A genome browser snapshot can be persuasive, but a metaprofile tells you whether it is representative.

## The Trick

Keep ambiguous enhancers in the analysis, but label them. For example, an enhancer with several candidate genes within 50 kb should not be forced into a single-gene story too early. Ambiguity is not a flaw; it is information about the regulatory landscape.

