+++
title = "Use pseudoreplicates to make peak sets less fragile"
date = 2026-06-19T09:20:00
draft = false
authors = []
tags = ["Peak calling", "IDR", "ChIP-seq", "ATAC-seq"]
categories = ["Genomics tips"]
summary = "A generic strategy for using pseudoreplicates and IDR-like thinking to build more robust ChIP-seq and ATAC-seq peak sets."

[header]
image = "research-atacseq-egattaca.jpg"
caption = ""
preview = true
+++

Peak sets are surprisingly fragile. Change one replicate, one depth threshold or one peak-calling parameter, and thousands of regions may appear or disappear.

A useful way to reduce this fragility is to ask whether peaks are reproducible under resampling. This is the logic behind pseudoreplicates and IDR-style workflows.

## The Core Idea

For each biological replicate:

1. Randomly split aligned reads into two pseudoreplicates.
2. Call peaks on the original replicate.
3. Call peaks on each pseudoreplicate.
4. Pool reads across replicates.
5. Split the pooled reads into pooled pseudoreplicates.
6. Keep peaks that behave reproducibly across these views.

This helps distinguish robust regulatory signal from peaks that depend too strongly on a particular sample or depth.

## A Minimal Shell Skeleton

```bash
# Shuffle alignments before splitting.
samtools view -h sample.bam \
  | awk 'BEGIN{srand(1)} /^@/ {print; next} {print rand() "\t" $0}' \
  | sort -k1,1n \
  | cut -f2- \
  | samtools view -bS - > sample.shuffled.bam

# Split into two pseudoreplicates.
total=$(samtools view -c sample.shuffled.bam)
half=$((total / 2))

samtools view -h sample.shuffled.bam \
  | awk -v n="$half" 'BEGIN{i=0} /^@/ {print > "pr1.sam"; print > "pr2.sam"; next} {i++; if (i <= n) print > "pr1.sam"; else print > "pr2.sam"}'

samtools view -bS pr1.sam | samtools sort -o sample.pr1.bam
samtools view -bS pr2.sam | samtools sort -o sample.pr2.bam
samtools index sample.pr1.bam
samtools index sample.pr2.bam
```

In production, I would make this more robust with workflow management and proper random seeds. The point is the principle: stress-test peak discovery by resampling reads.

## What To Compare

For narrow peaks, compare ranked peak lists with IDR or an equivalent reproducibility metric. For broad marks, exact boundaries are less meaningful, so compare overlap, rank stability and signal consistency across merged regions.

Useful questions:

- Are top-ranked peaks stable?
- Are replicate-specific peaks biologically plausible or mostly noise?
- Does pooling create many new peaks that no single replicate supports?
- Do pseudoreplicates preserve the same global signal distribution?

## Practical Advice

Do not treat IDR as a magic binary filter. Use it as a diagnostic layer. If a peak fails reproducibility but overlaps a known biologically important locus, inspect the raw signal before discarding it. Conversely, if a peak passes but sits in a problematic region, blacklist and genome-browser inspection still matter.

