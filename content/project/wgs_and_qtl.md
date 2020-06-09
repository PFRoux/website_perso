+++
slug = "Integrating linkage analysis with whole genome sequencing to dissect complex phenotypes"

# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Integrating linkage analysis with whole genome sequencing to dissect complex phenotypes"

# Project summary to display on homepage.
summary = ""

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "dna-1903318_640.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["DNA-seq", "QTL mapping", "GWAS"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/bubbles-wide.jpg"

+++

The ultimate goal of quantitative trait loci (QTL) mapping approaches is to gain a better understanding of biological mechanisms involved in these phenotypes to offer molecular tools for medical diagnosis or animal selection. Over the past three decades, several thousand QTL have been mapped for different traits in many species. In this context, whereas genome-wide association study is developing as the reference QTL mapping method for human populations, most of the QTL referenced today in experimental or livestock species were mapped by linkage analysis approaches through F2 genetic crosses. This is especially the case for species such as chicken, for which the individual production is inexpensive; in this case, for each phenotype of interest, divergent lines are usually created to maximize QTL heterozygosity after crossing parental lines. To date, 4714 QTL have been referenced in the Mouse Genome Database and 8006, 8935, and 3923 QTL for cattle, pigs, and chickens, respectively, in the animal QTLdb database. The major weakness of QTL mapped with linkage analysis is their large size, usually in the range of several megabases (Mbs). These intervals may contain up to hundreds of genes, which impedes the identification of causal underlying genes. When dealing with these large genomic regions and the numerous positional candidate genes they contain, it is tempting to focus narrowly on functional candidates. Hence, many of the causal genes identified to date were already known as being functionally related to the complex trait, limiting the research scope.

To overcome these limitations, in collaboration with [Simon Boitard](https://genphyse.toulouse.inra.fr/people/boitard/simon), I developped an approach combining signature selection mapping with hapFLK[^1]in divergent lines for one complex trait, cis-eQTL analysis and single nucleotide polymorphisms (SNPs) annotation in coding regions by using DNA-seq and improve identification of causal genes underlying QTL regions with no presupposed function.

{{< figure src="/img/Figure_QTL_project.jpg" title="Overview of the strategy used to combine WGS and QTL mapping. QTL: quantitative trait locus; cis-eQTL: QTL for gene expression and acting in cis; ASE: allele-specific expression; VeP: Variant Effect Predictor tool from the Ensembl API; NGS-SNP: variant annotation tool; GWAS: genome-wide association study; HMDP: Hybrid Mouse Diversity Panel." numbered="true" >}}

[^1]: For more details on hapFLK method, please refer to [Fariello et al. 2013](http://www.genetics.org/content/early/2013/01/07/genetics.112.147231)

