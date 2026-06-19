+++
# Projects widget.
widget = "projects"
active = true
date = 2016-04-20T00:00:00

title = "Research Projects"
subtitle = "Metabolism, genome regulation and integrative omics across aging, cancer and skin biology."

# Order that this section will appear in.
weight = 15

# Content.
# Display content from the following folder.
# For example, `folder = "project"` displays content from `content/project/`.
folder = "project"

# View.
# Customize how projects are displayed.
# Legend: 0 = list, 1 = cards.
view = 1

# Filter toolbar.

# Default filter index (e.g. 0 corresponds to the first `[[filter]]` instance below).
filter_default = 0

# Add or remove as many filters (`[[filter]]` instances) as you like.
# Use "*" tag to show all projects or an existing tag prefixed with "." to filter by specific tag.
# To remove toolbar, delete/comment all instances of `[[filter]]` below.
[[filter]]
  name = "All"
  tag = "*"

[[filter]]
  name = "Senescence"
  tag = ".cellular-senescence"

[[filter]]
  name = "Aging"
  tag = ".aging"
  
[[filter]]
  name = "Functional genomics"
  tag = ".functional-genomics"

[[filter]]
  name = "Skin biology"
  tag = ".skin-biology"
  
+++


My research connects experimental biology, functional genomics and computational modelling to understand how metabolic states reshape regulatory networks. Across projects, I combine molecular and cellular biology with RNA-seq, ATAC-seq, CUT&RUN, ChIP-seq, metabolomics, quantitative genetics and machine-learning strategies to move from omic profiles to mechanistic hypotheses.
