---
title: 'Physcraper: Abstract'
author:
  - Luna L. Sanchez Reyes
  - Martha Kandziora
  - Emily Jane McTavish
  - University of California, Merced
date: '24 June, 2020'
csl: apa.csl
output:
  
  redoc::redoc
keep_tex: true
---

# Abstract

1. Phylogenies are a key part of research in all areas of biology. Tools that automatize
some parts of the process of phylogenetic reconstruction (mainly character matrix construction)
have been developed for the advantage of both specialists in the field of phylogenetics and nonspecialists.
However, interpretation of results, comparison with previously available phylogenetic
hypotheses, and choosing of one phylogeny for downstream analyses and discussion still impose difficulties
to one that is not a specialist either on phylogenetic methods or on a particular group of study.

1. Physcraper is an open‐source, command-line Python program that automatizes the update of published
phylogenies by making use of public DNA sequence data and taxonomic information,
providing a framework for comparison of published phylogenies with their updated versions.

1. Physcraper can be used by the nonspecialist, as a tool to generate phylogenetic
hypothesis based on already available expert phylogenetic knowledge.
Phylogeneticists and group specialists will find it useful as a tool to facilitate comparison
of alternative phylogenetic hypotheses (topologies).
***Is physcraper intended for the nonspecialist?? We have two types of nonspecialists:
the ones that do not know about phylogenetic methods and the ones that might know
about phylogenetic methods but do not know much about a certain biological group.***

1. Physcraper implements node by node/topology comparison of the the original and the updated
trees using the conflict API of OToL, and summarizes differences.

1. We hope the physcraper workflow demonstrates the benefits of opening results in phylogenetics and encourages researchers to strive for better data sharing practices.

1. Physcraper can be used with any OS. Detailed instructions for installation and
use are available at <https://github.com/McTavishLab/physcraper>.

