+++
# Projects widget.
widget = "projects"
active = true
date = 2016-04-20T00:00:00

title = "Research Projects"
subtitle = "Three research threads linking multi-omic data, gene regulation and complex phenotypes."

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
  tag = ".senescence"
  
[[filter]]
  name = "RNA editing"
  tag = ".editing"

[[filter]]
  name = "WGS and QTLs"
  tag = ".QTL"
  
+++


My work connects experimental biology and computational analysis, from genome-wide assays to integrative models of regulatory networks.
