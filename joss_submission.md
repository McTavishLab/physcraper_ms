---
# Example from https://joss.readthedocs.io/en/latest/submitting.html
title: 'Physcraper: A Python package for continually updated gene trees'
tags:
  - Python
  - phylogenetics
  - update
  - species tree
  - Open Tree
authors:
  - name: Luna L. Sanchez Reyes
    orcid: 0000-0000-0000-0000
    affiliation: 1 # (Multiple affiliations must be quoted, like this: "1, 2")
  - name: Martha Kandziora
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Emily Jane McTavish
    orcid: 0000-0000-0000-0000
    affiliation: 1
affiliations:
 - name: University of California, Merced
   index: 1
citation_author: Sanchez-Reyes et. al.
date: '26 May, 2020'
year: 2020
bibliography: paper.bib
output: rticles::joss_article
csl: apa.csl
journal: JOSS
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

1. Physcraper implements node by node comparison of the the original and the updated
trees using the conflict API of OToL.

1. We hope the physcraper workflow demonstrates the benefits of opening results in phylogenetics and encourages researchers to strive for better data sharing practices.

1. Physcraper can be used with any OS. Detailed instructions for installation and
use are available at <https://github.com/McTavishLab/physcraper>.


# Introduction

Phylogenies are important.
Generating phylogenies is not easy.
The process of phylogenetic reconstruction implies many steps that can be generalized to the following:

1. Obtention of molecular or morphological character data -- get DNA from some organisms
and sequence it, or get it from an online repository, such as GenBank.
1. Assemble a hypothesis of homology -- Create a matrix of your character data, by
aligning the sequences, in the case of molecular data.
1. Analyse this hypothesis of homology to infer phylogenetic relationships among
the organisms you are studying -- Use different available programs to infer molecular
evolution, trees and times of divergence.
1. Discuss the inferred relationships in the context of previous hypothesis, the
biology and biogeography of the organisms, etc. -- Answer the question, *is this phylogenetic solution fair/reasonable?*

Each of these steps require different types of specialized training: in the field,
in the lab, in front of a computer, discussions with experts in the methods, and/or in the biological group of study.
All of these steps also require considerable amounts of time for training and implementation.

In the past decade, various studies have developed solutions to automatize the first and second steps, by creating
pipelines that mine already available molecular data from the GenBank repository,
to obtain homologous characters that can be used for phylogenetic reconstruction.
These tools have been presented as aid for the nonspecialist to decrease some of
the difficulties in the generation of phylogenetic knowledge. However, they are
not that often used as so, suggesting that there are still difficulties for the nonspecialist.
The phylogenetic community has some reserves towards these tools, too. Mainly because they sometimes act as a black box.
However, automatizing the assembly of the character data set is a crucial step towards
reproducibility for a task that was otherwise primarily artisanal and hence largely
non-reproducible.

Even if it is hard to obtain phylogenies, we invest copious amounts of time and energy in generating them.
They are crucial to solve problems such as food security, global warming, global health.
There is a lot of phylogenetic knowledge already available in published peer-reviewed studies.
In this sense, the non-specialists (and also the specialist) face a new problem: how do I choose the best phylogeny.

Public phylogenies can be updated with the ever increasing amount of genetic data that is available on GenBank.

A way to automatize the comparison of phylogenetic hypotheses and to allow reproducibility of the last step of the process.


A key aspect of the standard phylogenetic workflow is comparison with already existing
phylogenetic hypotheses and with phylogenies that are considered "best" by experts
not only in phylogenetics, but also experts on the focal group of study.

It is well known that GenBank holds enormous amounts of genetic data, and it continues to grow.
A lot of this genetic data has the potential to be used to reconstruct the phylogenetic
history of various organisms [@sanderson2008phylota].
Pipelines that harness this potential have been available for over a decade now, such
as the Phylota browser, and PHLAWD. New ones keep on being developed, such as SUPERSMART
and the upgraded version of PHLAWD, PyPHLAWD.
Notably large phylogenies have been constructed using some of these tools,
Some other have not been used that much. So, how well accepted is this approach in the community?

Concerns with these tools:
Errors in identification of sequences
Little control along the process
Too much of a black box?

Most of these phylogenies are being constructed by people learning about the methods,
so they want to know what is going on.

The pipelines are so powerful and they will give you an answer, but there
is no way to assess if it is better than previous answers, it just assumes it is
better because it used more data.

All these pipelines start tree construction from zero?

The goal of Physcraper is to build upon previous phylogenetic knowledge,
allowing a direct comparison of existing phylogenies to phylogenies that are constructed
using new genetic data from GenBank

To achieve this, Physcraper uses the Open Tree of Life phylesystem and connects it
to the TreeBase database, to (1) get the original DNA data set matrices (alignments) that produced
a phylogeny that was published and then made available in the OToL database, (2)
use this DNA alignments as a starting point to get new genetic data belonging
to the focal group of study, to (3) finally update the phylogenetic relationships in the group.

A less automated workflow is one in which the alignments that generated the published
phylogeny are stored in other public database (such as DRYAD) or elsewhere (the users computer), and
are provided by the users.

The original tree is by default used as starting tree for the phylogenetic searches, but it
can also be set as a full topological constraint or not used at all, depending on
the goals of the user.

Physcraper implements node by node comparison of the the original and the updated trees, using the conflict API of OToL.

# How does Physcraper work?

## The input: a study tree and an alignment

- The phylogenetic tree should be already in the Open Tree of Life store, or submitted
  via the curator system [@mctavish2015phylesystem].
  A user can choose from a variety of published trees supporting any node of the Tree of Life. If the tree you are
  interested in is not in Open Tree of Life, you can easily upload it via the curator
  tool (ADD URL).
- The alignment should be a gene alignment that was used to generate the tree. The
  alignments are usually stored in a public repository such as TreeBase [@piel2009treebase; @vos2012nexml],
  DRYAD (<http://datadryad.org/>), or the journal were the tree was originally published.
  If the alignment is stored in TreeBase, `physcraper` can download it directly
  either from the TreeBASE website (<https://treebase.org/>)
  or through TreeBASE GitHub repository, SuperTreeBASE (<https://github.com/TreeBASE/supertreebase>).
  If the alignment is on another repository, a copy of it has to be
  downloaded by the user, and it's local path has to be provided as an argument.
- A taxon name matching step is performed to verify that all taxon names on the tips
  of the tree are in the DNA character matrix and vice versa.
- A ".csv" file with the summary of taxon name matching is produced for the user.
- Unmatched taxon names are dropped from both the tree and alignment.
  <!--***What is the minimum amount of tips necessary for a physcraper run??*** Just one!-->
  Technically, just one matching name is needed to perform the searches. See below.
- A ".tre" and ".aln" files are generated and saved for a `physcraper` run.


## DNA sequence search and cleaning

- The next step is to identify and validate the search taxon. This must be a taxon (a named clade)
  from the NCBI taxonomy. It will be used to constraint the DNA sequence search on
  the GenBank database within that taxonomic group.
  By default, the search taxon is the most recent common ancestor (MRCA) of the
  matched taxa that is also a named clade in the NCBI taxonomy. This is refered to as the most recent common
  ancestral taxon (MRCAT) or the least inclusive common ancestral taxon (LICA).
  It can be different from the phylogenetic MRCA when the latter is an unnamed clade.
  This is done using the Open Tree API [taxonomy/mrca](https://github.com/OpenTreeOfLife/germinator/wiki/Taxonomy-API-v3#mrca).
  <!-- ***Does physcraper takes into account the focal clade from Open Tree in any way???***
  Not really, the focal clade is a search MRCA more than a taxonomic MRCA, physcraper's default is to get the ingroup from Otol, which is not the focal group.-->
  In the case that only one taxon is matched in both the tree and alignment, the MRCAT
  for that single taxon would be determined as HOW?,
  A search taxon can also be given by the user. It can be a more inclusive
  clade, if the user wants to perform a wider search, outside the MRCAT of the matched taxa, e.g., including all taxa within
  the family or the order. It can also be a less inclusive clade, if the user only
  wants to focus on enriching a particular clade/region within the tree.
- The BLAST algorithm is used to identify similarity between DNA sequences in a GenBank nucleotide
  database within the search taxon, and the remaining sequences on the alignment.
  <!--***How does the blast is setup? Is it an all-blast-all??***-->
- A pairwise all-against-all BLAST search is performed. This means that each sequence
  in the alignment is BLASTed against DNA sequences in a GenBank database constrained to the search
  taxon. Results from each one of these BLAST runs are recorded, and matched sequences are saved
  along with their corresponding GenBank accesion numbers. This information will be
  used later to store the whole sequences into a new library.
- The DNA sequence similarity search can be done on a local database that is easily
  setup by the user. In this case, the BLASTn algorithm is used to performs the similarity search.
- The search can also be performed remotely, on the NCBI database. In this case, the
  bioPython BLAST algorithm is used to perform the similarity search.
- Matched sequences below an e-value, percentage similarity, and outside a minimum
  and maximum length threshold are discarded. This filtering leaves out genomic sequences.
  All acepted sequences are asigned an internal identifier, and are further filtered.
- Because the original alignments usually do not have the GenBank accession numbers
  on the sequence names, a filtering process is needed. Accepted sequences that belong to the
  same taxon of the query sequence, and that are either identical or shorter than
  the original sequence are also discarded. Only longer sequences belonging to the
  same taxon as the orignal sequence will be considered for further analyses.
- Among the remaining filtered sequences, there are usually several exemplars per taxon.
  Although it can be useful to keep some of them to, for example, investigate monophyly
  within species, there can be hundreds of exemplar sequences per taxon for some markers.
  To control the number of sequences per taxon kept for further analyses, by default
  5 sequences per taxon are chosen at random. This number can be controlled by the user.
  <!--***How does pyphlawd, or phylota does the exemplar per sepcies choosing?***-->
- Reverse complement sequences are identified and translated.
- This cycle of sequence search is performed two times. ***Is there an argument to control the number of cycles of blast searches with new sequences***
- A fasta file containing all sequences resulting from the BLAST searches is generated for the user.

## DNA sequence alignment

- The software MUSCLE [@edgar2004muscle] is implemented to perform alignments.
- First, all new seweunces are aligned using default MUSCLE options.
- Then, a MUSCLE profile alignment is performed, in which the alignment of new sequences
  is aligned against the original alignment, working as a template. This ensures that
  the final alignment follows the homology criteria established by the original alignment.
- The final alignment is not further processed automatically. We encourage users
  to check it by eye and eliminate columns with no information.

## Tree reconstruction

- A gene tree is reconstructed for each alignment provided, using RAxML with bootstrap replicates.
- The final result is a gene tree coupled to the conlict info.

## Tree comparison

- Conflict information can only be generated in the context of the whole Open Tree of
Life. Otherwise, it is not really possible to get conflict data.
***- One way to compare two independent phylogenetic trees is to compare them both to
the synthetic OToL and then measure how well they do against each other***

# Use case/ example

Imagine you are starting to work on a new biological group X. You have not much of an idea about
its phylogenetic relationships, you are a newly established researcher, and the group
is not anything any of your collaborators have worked on before.
A good idea is to start an intensive literature review on the phylogenetics of the group.
Rapidly, you find out there are 5 different phylogenies, that used different markers, and that
the papers, published at different times, do not discuss which phylogeny is
the one accepted by the expert community on X. You might need
to go to the annual conference of X, and even then, you might only find
different and contrasting opinions.
Somewhere along these months or even years doing this task, you looked into the
the OToL database. You found in there some or all the published trees of X, along
with a tree that has been deemed the best tree by curators and ideally experts on X?

## Ascomycota Example

Let's be more specific now about our X group and say it is the Ascomycota.
The best tree currently available in OToL was published by @schoch2009ascomycota.
The first step, is to get the Open Tree of Life study id. There are some options to do this:
- You can go to the Open Tree of Life website and browse until you find it, or
- you can get the study id using R tools:
  - By using the TreeBase ID of the study (which is not fully exposed on the
    TreeBase website home page of the study, so you have to really look it up manually):

```r
rotl::studies_find_studies(property = "treebaseId", value = "S2137")
##   study_ids n_trees         tree_ids candidate study_year title
## 1    pg_238       2 tree109, tree110                 2009      
##                                 study_doi
## 1 http://dx.doi.org/10.1093/sysbio/syp020
```
  - By using the name of the focal clade of study (but this behaved very differently):

```r
rotl::studies_find_studies(property="ot:focalCladeOTTTaxonName", value="Ascomycota")
```

Once we have the study id, we can gather the trees published on that study:

```r
rotl::get_tree_ids(rotl::get_study_meta("pg_238"))
## [1] "tree109" "tree110"
rotl::candidate_for_synth(rotl::get_study_meta("pg_238"))
## NULL
my_trees <- rotl::get_study("pg_238")
```
Both trees from this study have 434 tips.

Let's check what one of the trees looks like:

<!-- ```{r fungi-phylo, eval = TRUE, fig.retina = 2, fig.width = 2} -->
<!-- ape::plot.phylo(ape::ladderize(my_trees[[1]]), type = "phylogram", cex = 0.1) -->
<!-- ``` -->

1. Download the alignment from TreeBase
If you are on the TreeBase home page of the study, you can navigate to the matrix tab, and manually download the alignments that were used to reconstruct the trees reported on the study that were also uploaded to TreeBase and to the Open Tree of Life repository.
To make this task easier, you can use a command to download everything into your working folder:
```
physcraper_run.py -s pg_238 -t tree109 -o ../physcraper_example/pg_238
```
In this example, all alignments posted on TreeBase were used to reconstruct both trees.

1. With the study id and the alignment files saved locally, we can do a physcraper run with the command:

```
physcraper_run.py -s pg_238 -t tree109 -a treebase_alns/pg_238tree109.aln -as "nexus" -o pg_238
```

## Testudines example

Phylogeny of the Testudines 6 tips from @crawford2012more
There is just one tree in OToL.
There is just one alignment on [treebase](https://treebase.org/treebase-web/search/study/matrices.html?id=12742) with all the 1 145 loci.


```
physcraper_run.py -s pg_2573 -t tree5959 -tb -db ~/branchinecta/local_blast_db/ -o pg_2573
```
# Discussion

There are many tools that are making use of DNA data repositories in different ways.
Most of them focus on efficient ways to mine the data -- getting the most homologs.
Some focus on accurate ways of mining the data - getting real and clean homologs.
Others focus on refinement of the alignment.
Most focus on generating full trees *de novo*, mainly for regions of the Tree of
Life that have no phylogenetic assessment yet in published studies, but also for
regions that have been already studied and that have phylogenetic data already.

All these tools are great efforts for advancing towards reproducibility in phylogenetics,
a field that has been largely recognised as somewhat artisanal.
We propose adding focus to other sources of information available from data repositories.
Taking advantage of public DNA data bases have been the main focus. However, phylogenetic knowledge is
also accumulating fast in public and open repositories.
In this way, the physcraper pipeline can be complemented with other tools that have
been developed for other purposes.

We emphasize that physcraper takes advantage of the knowledge and intuition of the expert
community to build upon phylogenetic knowledge, using not only data accumulated in
DNA repositories, but phylogenetic knowledge accumulated in tree repositories.
This might help generate new phylogenetic data. But physcraper does not seek to generate full phylogenies *de novo*.

Describe again statistics to compare phylogenies provided by physcraper via OpenTreeOfLife.
Mention statistics provided by other tools: PhyloExplorer [@ranwez2009phyloexplorer].
Compare and discuss.



## Tools that do similar things at different levels

### 1. Mining DNA databases for phylogenetic reconstruction

| Tool | Citation | Cited by | Descriptio | Supermatrix/gene tree/species tree |
|-----|------|:------:|:------:|:------:|
| Phylota | @sanderson2008phylota | cited by 122 studies | finding homologs on GenBank database | Supermatrix |

- PHLAWD [@smith2009mega] - cited by 234, and pyPhlawd [@smith2019pyphlawd] - cited by 6: baited analyses

- AMPHORA [@wu2008simple] - cited by 458: a tool for mining public whole genomes and constructing phylogenies
using whole genomic data. According to @ceron2019phylotol, both AMPHORA and PHLAWD
"focus on the construction and refinement of robust alignments rather than the collection of homologs."

A [ruby pipeline](https://www.zfmk.de/en/research/research-centres-and-groups/taming-of-an-impossible-child-pipeline-tools-and-manuals),
only available from the [supplementary data](https://static-content.springer.com/esm/art%3A10.1186%2F1741-7007-9-55/MediaObjects/12915_2011_480_MOESM1_ESM.ZIP)
of the journal [[@peters2011taming]](https://bmcbiol.biomedcentral.com/articles/10.1186/1741-7007-9-55#Sec21)
- cited by 64:  mining public DNA databases, focuses on filtering massive amounts
of mined sequences by using established "criteria of compositional homogeneity and
defined levels of density and overlap".

### 2. Searching phylogenetic tree databases

- PhyloFinder [@chen2008phylofinder] - cited by 18: a search engine for phylogenetic databases using
trees from TreeBASE - more related to phylotastic's goal than to updating phylogenies

### 3. Mining phylogenetic tree databases

- PhyloExplorer [@ranwez2009phyloexplorer] - cited by 21: a python and MySQL based website to facilitate
assessment and management of phylogenetic tree collections. It provides "statistics describing the collection,
correcting invalid taxon names, extracting taxonomically relevant parts of the collection
using a dedicated query language, and identifying related trees in the TreeBASE database".

### 4. Synthesizing info from mined trees








@chesters2014protocol presents an algorithm that mines GenBank data to delineate species in the insecta.
The authors present a nice comparison with the phylota algorithm.

PUmPER [@izquierdo2014pumper] - perpetual updating with newly added sequences to
GenBank

DarwinTree [@meng2015darwintree] predecessor is Phylogenetic Analysis of Land Plants Platform (PALPP) - takes data from GenBank, EMBL and DDBJ for land plants only.

NCBIminer [@xu2015ncbiminer]

SUMAC [@freyman2015sumac] -  both “baited” analyses and single‐linkage clustering
methods, as well as a novel means of determining when there are enough overlapping data in the DNA matrix

STBase - @mcmahon2015stbase present a pipeline for species tree construction and
the public database of one million precomputed species trees

@papadopoulou2015automated - Automated DNA-based plant identification for large-scale biodiversity assessment

SUPERSMART [@antonelli2017toward] - baited analyses up to bayesian divergence time
estimation

SOPHI - [@chesters2017construction] - Searches DNA sequence data from repos other
than GenBank, such as transcriptomic and barcoding repos.

OneTwoTree [@drori2018onetwotree] present a Web‐based, user-friendly, online tool for species-tree
reconstruction, based on the *supermatrix paradigm* and retrieves all available
sequence data from NCBI GenBank.

PhySpeTre [@fang2019physpetree] - no sequence retrieval, just phylogenetic reconstruction
pipeline.

Phylotol [@ceron2019phylotol] - "phylogenomic pipeline to allow easy incorporation
of data from  high-throughput sequencing studies, to automate production of both
multiple sequence alignments and gene trees, and to identify and remove contaminants.
PhyloToL is designed for phylogenomic analyses of diverse lineages across the tree
of life", i.e., bacteria and unicellular eukaryotes.

Datataxa @ruiz2019datataxa focus on extracting metadata from GenBank seqeunce information.




# Phylota overview

Phylota was published as a website to summarize and browse the phylogenetic potential of the GenBank
database [@sanderson2008phylota].

Since then, it has been cited 122 times for different reasons.


1. As an example of a tool that mines GenBank data for phylogenetic reconstruction,
or that is useful in any way for phylogenetics:
    - original publication of PHLAWD [@smith2009mega]
    - an analysis identifying research priorities and data requirements for resolving
    the red algal tree of life [@verbruggen2010data]
    - @beaulieu2012modeling cites phylota As an example study of very large and comprehensive
    phylogeny from mined DNA sequence data, (even if no phylogeny was really published
    there, only the method to do so)
    - a review for ecologists about phylogenetic tools [@roquet2013building]
    - a study constructing a dated seed plant phylogeny using pyPHLAWD [@smith2018constructing]
    - a study presenting an assembly and alignment free method for phylogenetic reconstruction
    using genomic data, that aims to be incorporated in a tool as phylota some day [@fan2015assembly].
    - nexml format presentation [@vos2012nexml] - cites phylota as a tool that uses
    stored phyloinformatic data that could benefit from adopting nexml, to increase
    interoperability.
    - a study of fruit evolution, analysing a previously published phylogeny of 8911
    tips of the Campanulidae, constructed with PHLAWD [@beaulieu2013fruit]
    - a study of Southeast Asia plant biodiversity inventory [@webb2010biodiversity] -
    cites phylota as a tool that would allow rapid phylogentic placing of newly
    discovered species, and generation of phylogenetically informed guides for field
    identification.
    - a study of wood density for carbon stock assessments [@flores2011estimating],
    cites phylota as an initiative to "get supertrees resolved up to species level".
    - a study proposing something similar to Open tree but applied only to land plants [@beaulieu2012synthesizing]
    - an analysis of the phylogenetic diversity-area curve [@helmus2012phylogenetic],
    cited phylota as a method alternative to phylomatic to "obtain plant phylogenetic
    trees for ecophylogenetic studies".
    - a study generating a phylogeny of 6,098 species of vascular plants from China
    [@chen2016tree] - uses DarwinTree [@meng2015darwintree] and generates sequence
    data *de novo* for 781 genera.
    - a review of the state of methods and knowledge generated by molecular systematics
    [@san2010molecular] cites phylota as a tool "intended to systematize GenBank information
    for large-scale molecular phylogenetics analysis".
    - the first phylotastic paper [@stoltzfus2013phylotastic] cites phylota as a "phylogeny
    related resource that provides ways to generate custom species trees for downstream use".
    - @antonelli2017toward cites phylota as a "pipeline that pre-processes entire GenBank
    releases in pursuit of sufficiently overlapping reciprocal BLAST hits, which are
    then clustered into candidate data sets". I also uses the PHYLOTA database in its
    own pipeline.
    - @deepak2014evominer present an algorithm for mining of frequent subtrees (common patterns)
    in collections of phylogenetic trees, as a way to extract meaningful phylogenetic
    information from collections of trees when compared to maximum agreement subtrees
    and majority-rule trees. They cite phylota as one of such tree collections available
    along with TreeBASE [@piel2009treebase].
    - @ranwez2009phyloexplorer cites phylota as a "program providing basic statistics
    on data availability for molecular datasets". They propose a tool to upload and
    explore user phylogenies to obtain detailed summary statistics on user tree collections.
    - @freyman2015sumac cites phylota as a tool that "provides a web interface to view
    all GenBank sequences within ta xonomic groups clustered into homologs" but that
    does not mine for targeted sequences, as opposed to NCBIminer or PHLAWD. They
    compare the performance of SUMAC to Phylota. This is also presented in their PhD dissertation [@freyman2017phylogenetic].
    - @chesters2013resolving cites phylota as a data mining tool that compiles metadata
    from mining of public DNA databases "for construction of large phylogenetic trees
    and multiple gene sets" and that the authors have recognised that gene annotations
    in public databases are insufficient and that careful partitioning of orthologous
    sequences is needed for supermatrix construction. @chesters2013resolving present
    a procedure that minimizes the problem of forming multilocus species units in
    a large phylogenetic data set using algorithms from graph theory.
    - @chesters2014protocol present an algorithm to delineate species form GenBank
    DNA data, and cites phylota as a tool that partitions "the contents of a database
    according to homology", by "grouping of database sequences according to internal
    criteria", searching "from a standardized set of references [...] patterns in
    sequence similarity and overlap."
    - the paper presenting phylotaR, a pipeline that recreates the phylota output
    but uses the most updated GenBank release, and is available in R [@bennett2018phylotar],
    cites phylota as its predecessor and inspiration. The authors mention that phylotaR
    pipeline mimics phylota's pipeline but with improvements.
    - The paper presenging PhyloBase [@jamil2016visual], cites phylota as one of
    its resources to get phylogenies, along with TreeBASE and others.
    - The paper presenting STBase, a database of one million precomputed species
    trees [@mcmahon2015stbase; @deepak2013managing], cites phylota as a databse of gene trees or mul-trees,
    "trees having multiple sequences with the same taxon name".
    - @drori2018onetwotree present a Web‐based, user-friendly, online tool for species-tree
    reconstruction, based on the *supermatrix paradigm* and retrieves all available
    sequence data from NCBI GenBank. They cite phylota in the intro as a tool that is "designed to provide
    users with precomputed sets of clusters that were assembled through a single‐linkage
    clustering approach and additionally provides precomputed gene trees that were
    reconstructed for each cluster. In particular, the results obtained by PhyLoTa
    are taxonomically constrained; that is, all sequences of the most recent common
    ancestor are collected even if one specifies only part of a clade".
    - A study developing a tool to link wikipedia data to NCBI taxonomy [@page2011linking]
    cites phylota as a phylogenetic resource that uses the NCBI taxonomy.
    - the study that present DarwinTree [@meng2015darwintree], and all derived studies: the study
    presenting an approach to screen sequence data for The Platform
    for Phylogenetic Analysis of Land Plants (PALPP), using the MapReduce paradigm
    to parallelize BLAST [@yong2010screening], as well as @gao2011solution, @li2013partfasttree,
    @meng2014rapidtree, @meng2015sotree, and @meng2015solution, all cite phylota using the exact same
    introduction and sentence: as one among other "studies based on data mining large numbers of taxa or loci".
    - A study presenting a tool to asses gene sequence quality for automatic
    construction of databases [@meng2012gsqct], as well as their parallelized version using MapReduce
    [@meng2012cloud], cite phylota (along with @yong2010screening) as a tool that relies on sequence
    similarity (BLAST) and not taxon name annotations in the database, for mining
    large numbers of taxa or loci, without making any control on the quality of the
    sequencing.
    - A review on online plant databases aiming to "provide recommendations for current
    information managers and developers concerning the user interface and experience;
    and to provide a picture about the possible directions to take for those in charge
    of the creation of information at all levels". They cite phylota as a tool allowing
    researchers "to acces equally and globally, without travel, a [phylogenetic?] model
    of plants at the kingdom level" [@jones2014trends].
    - a paper aiming to establish an online information system for the legumes and
    to outline "best practices for development of a legume portal to enable data
    sharing and a better understanding of what data are available, missing, or erroneous,
    and ultimately facilitate cross-analyses and collaboration within the legume-systematics
    community and with other stakeholders" [@bruneau2019towards], cites phylota (along with supersmart and pyphlawd) as a
    "pipeline for large-scale retrieval of GenBank data of particular taxa or clades".
    In their Table 1, they also list phylota as a potential data source for developing a legume portal.
    - A study on morphological evolution of electric fish skull, that uses phylotaR
    to retrieve sequences of the family Apteronotidae, order Gymnotiformes [@evans2019bony],
    cites phylota as the inspiration and fundament of phylotaR.
    - A phylogenetic revision of the Gymnotidae fish (Teleostei: Gymnotiformes),
    uses phylotaR to retrieve seqeunces, but cites phylota as "a pipeline that implements
    BLAST searches to both identify and download sequence clusters for listed taxonomic
    groups to assemble a robust collection of sequences in a reproducible way based
    on publicly-available gene sequences while avoiding selection bias on the part
    of the assembler".
    - A master thesis on SearchTree, a "software tool that allows users to query
    efficiently on an arbitrary user taxon list and returns high scoring matches
    from approximately one billion phylogenetic trees being constructed from molecular
    sequence data in GenBank" [@deepak2010searchtree], that seems to be the preliminary
    work for STBase [@mcmahon2015stbase], cites phylota as "a standard strategy, to assemble sets of homologous sequences
    (clusters) from a database of all-against-all BLAST searches, [in which] clusters
    are constructed in the context of the NCBI taxonomy tree for convenience of display,
    thus child clusters are contained within parent clusters, following the NCBI hierarchy".
    In opposition, SearchTree uses true agglomerative hierarchical clustering
    (AHC: @day1984efficient) based on the BLAST estimates of sequence dissimilarity
    rather than the NCBI tree".
    - a recent review on the state of large phylogeny (namely insects) generation
    using tools of the data-driven era [@chesters2019phylogeny] cites phylota as
    a tool for homology inference and retrieval.
    - the study presenting phylotol [@ceron2019phylotol], cites phylota as a tool
    that "focus on the identification and collection of homologous genes from public
    databases".
    - The [iPTOL project](https://www.researchgate.net/profile/Douglas_Soltis/publication/228815637_Assembling_the_Tree_of_Life_for_the_Plant_Sciences_iPTOL/links/56a7c6bc08aeded22e3700dc.pdf)
    cites phylota as a resource of phylogenetic trees.
    - @mahmood2015avian PhD dissertation presents a database of avian Raptor sequences
    (raptorbase), based on the phylota pipeline.
    - @ruiz2019datataxa develops datataxa and cite phylota as "software that has
    been developed to mine the massive amount of information stored in GenBank",
    along with its R version [phylotaR; @bennett2018phylotar] and restez <https://www.rdocumen-tation.org/packages/restez/versions/1.0.0>.
    - The phylotastic project [@stoltzfus2013phylotastic] cites phylota as a "phylogeny-related resource providing ways to generate custom species trees *de novo* for downstream use" along with CIPRES.
2. When the software was actually used to construct (partially or in full) a DNA
data set to be used for phylogenetic reconstruction:
    - A 1000 tip phylogeny of the family of the nightshades [@sarkinen2013solanaceae]
    - A 56 tip phylogeny of crustacean zooplancton [@helmus2010communities] -- ecological study
    - A 63 tip phylogeny of the Salmonidae family [@crete2012salmonidae]
    - A 321 tip phylogeny of Testudines [@thomson2010sparse]
    - A 69 taxa phylogeny of the family Cyprinodontidae of the pupfish [@martin2011trophic]
    - A 2,957 taxa phylogeny of the class Moniloformopses of living ferns [@lehtonen2011towards]
    - A 2,573 species phylogeny of the Papilionoidea [@hardy2014specialization]
    - A 23 taxa phylogeny of the California flora [@anacker2011origins]
    - Phylogenies of 6 different clades of flowering plants representing an independent
    evolutionary origin of extrafloral nectaries: *Byttneria* (Malvaceae), *Pleopeltis* (Polypodiaceae),
    *Polygoneae* (Polygoneaceae), *Senna* (Fabaceae), *Turnera* (Passifloraceae), and *Viburnum*
    (Adoxaceae) [@weber2014defense].
    - To supplement DNA data sets of various pre-existing mammalian phylogenetic trees
    sampled at different taxonomic levels [@faurby2015species]
    - A 900 species tree of muroid rodents, Muroidea [@steppan2017muroid], where 300
    species were newly added by the study and the rest obtained using phylota.
    - A 95 taxa phylogeny of Gymnosperms, focused on Ephedra, Gnetales [@ickert2009fossil]
    - A 1061 genera phylogeny of the Oscine birds [@selvatti2015paleogene]
    - A 268 species phylogeny of sharks, representing all 8 orders and 32 families [@sorenson2014effect; @sorenson2014evolution]
    - A 466 species phylogeny of the Proteaceae, focusing on the species found in the Cape Floristic Region [@tucker2012incorporating].
    - A series of small phylogenies of unreported exact size, of sister groups of gall-forming insects [@hardy2010gall].
    - A 196 species phylogeny of the family Boraginaceae [@nazaire2012broad]. The authors
    actually found data for 318 Boraginaceae spp using phylota, but decided to reduce
    their data set to focus on the monophyly of genus *Mertensia*.
    - A phylogeny of 401 species of scale insects Coccoidea, Hemiptera [@ross2013large],
    with some sequences generated *de novo*.
    - Two phylogenies sampling all species of two different clades of insectivorous
    lizards, agamids and diplodactyline geckos, groups considered to be radiating
    in the Australia’s Great Victoria Desert [@rabosky2011species]
    - A phylogeny of 91 species of sparid and centracanthid fishes, Sparidae, Percomorpha,
    plus 2 outgroups, a lethrinid and a nemipterid exemplar [@santini2014first].
    - Updating a phylogeny of Arecaceae, constructing relationships in 6 cldes within
    the group: subfamilies Calamoideae and Coryphoideae, the tribe Ceroxyleae within
    subfamily Ceroxyloideae and three groups within subfamily Arecoideae: (1) Iriarteeae,
    (2) Cocoseae: Attaleinae except Beccariophoenix and (3) a group containing six
    tribes; Euterpeae, Leopoldinieae, Pelagodoxeae, Manicarieae, Geonomateae and Areceae
    [@faurby2016all].
    - A phylogeny of 768 Gesneriaceae species and 58 outgroups for a total species
    sampling of 826 taxa [@roalson2016distinct] some sequence were generated *de novo*.
    - A phylogeny of 47 species of scombrid fishes, with 2 outgroups, a gempylid and
    a trichiurid [@santini2013first].
    - to update a dataset underlying a large-scale fern phylogeny [@lehtonen2017environmentally],
    data set in <https://zenodo.org/record/345670#.Xr9QFRPYqqg>, also in TreeBASE,
    but it is one of those studies that is broken.
    - A phylogeny of 13 species of billfishes, order Istiophoriformes: Acanthomorpha,
    and four outgroups [@santini2013first]
    - A phylogeny of 765 aphid species, family Aphididae [@hardy2015evolution]
    - A phylogeny of less than 100 taxa of the family Ranunculaceae [@lehtonen2016sensitive],
    even though they retrieved info from phylota for 194 taxa within the family, they
    reduced their data set because of low sampling of markers for some taxa.
    - A phylogeny of 144 neobatrachian genera, assuming the monophyletic status of
    genera to increase matrix-filling levels [@frazao2015gondwana].
    - A 179 species phylogeny of the bird family Picidae (woodpeckers, piculets,
    and wrynecks) [@dufort2016augmented; @dufort2015coexistence], augmented with data from an updated GenBank
    release and newly sequenced data.
    - A phylogeny of species of freshwater fish endemic to NorthAmerica [@strecker2014fish],
    phylota found data for 54 out of 66 spp.
    - A phylogeny of 520 species of the order Ericales [@hardy2012testing]
    - A phylgeny of 16 fish species of the family Sphyraenidae (Percomorpha), as well
    as two outgroup species of the Centropomidae (barracudas) [@santini2015first]
    - A phylogeny of 34 vole species, Arvicolinae, Rodentia [@garcia2016role]
    - @kolmann2017dna uses phylota to download all 1691 co1 sequences belonging to
    the order Carchariniformes, to place phylogenetically DNA samples obtained from
    fish markets.
    - A phylogeny of 329 bird species in the Tyrannidae (77% of the species in the
    family) [@gomez2020speciation; @gomez2015behavioral]
    - Retrive 145 sequences registered as *Holothuria* species, but kept 84 as ingroup,
    plus 4 outgroup sequences from *Stichopus ocellatus*, all belonging to the order
    Apodida of sea cucumbers [@kamarudin2016phylogenetic]
    - On a master thesis, to get the sequences of the outgroups of Melinidinae, family Poaceae, namely several spp of the
    subfamily Panicoideae, plus *Gynerium sagittatum*, *Chasmanthium latifolium*,
    and *Zea mays*, [@salariato2010filogenia]. Interestingly, phylota was not used
    in the published study of the thesis [@salariato2010molecular]. Ingroup sequences were generated *de novo*.
    - On a PhD thesis, to construct a phylogeny of Platyrrhini (internal group),
    Catarrhini (outgroup), and Tarsiiformes @pereira2013padroes. Have not found a published study.
    - The 10k trees project [@arnold201010ktrees] uses phylota to construct a tree of 301 primate species
    and the outgroup species *Galeopterus variegates*, a tree of 17 extant odd-toed
    ungulates species and the outgroup species *Bos taurus*, and a tree of 70 different
    species of carnivorans and *Equus caballus* as outgroup. However, the do not
    cite it on the paper, but only on their documentation <http://www.academia.edu/download/49690788/10kTrees_Documentation.pdf>.
    - @freyman2015sumac [also in @freyman2017phylogenetic], use phylota to construct
    a phylogeny (or maybe only mine genbank???) of the Onagraceae and Lythracea,
    and compare it to the tool they propose, SUMAC.
    - @blackmon2017synthesis PhD study applies phylota to reconstruct a 822 mite
    species tree.
    - A study of the effect of poliploidy on niche evolution [@baniaga2018polyploid],
    uses phylota to get a DNA data set for 132 unique taxa of vascular plants from
    16 families and 25 genera,and a tree of 33 genera from 20 different families
    comprising 1706 taxa.
3. When the website was used to identify sequences and markers available in
GenBank for a particular group. In this cases, the dataset mining was either performed
with other tools, or not performed at all and just used for discussion:
    - A 812 tips phylogeny of the Order Chiroptera [@shi2015speciation] -- dataset
    constructed with PHLAWD
    - A 1276 tips phylogeny of the Fabaceae [@legume2013legume] -- dataset constructed
    by hand (I think??)
    - A review of dated phylogenies of fire-prone tropical savanna species from Brazil
    [@simon2012cerrado] -- just for discussion of the lack of markers available for
    these species on GenBank
    - A review of the phylogeetic sof the Apicomplexa, a parasitic phylum on unicellular
    protists [@morrison2009apicomplexa].
    - Three data sets from phylota (the suborder Pleurodira of side-necked turtles;
      the family Cactaceae of cacti; and the Amorpheae, a clade of legumes) were used
      to demonstrate and exemplify phylogenetic decisiveness [@sanderson2010phylogenomics]
    - Mentioned in a PHD thesis [@gagnon2016systematique], but not on the final publication [@gagnon2016new],
    phylota was used to state that there are very few sequences available for the Legumes (7,482 out of 19,500 spp) on GenBank's release 194 (Feb2013).
4. Sometimes, it was cited by mistake:
    - In this 630 tip phylogeny of the Caryophyllaceae study [@greenberg2011caryophyllaceae] it might have been originally
    cited as an example of large phylogenies that reflect well supported relationships
    from previous smaller phylogenies. However, it was removed from the text but
    not from the final list of references. The DNA data set was constructed by hand
    most probably.
    - a study reconstructing the insect tree of life with 49,358 species, 13,865
    genera, and 760 families within the order Insecta [@chesters2017construction],
    uses its own algorithm (SOPHI) to mine public DNA databases [@chesters2014protocol].
    It does not cite phylota as it should, but includes it in their references.
5. When phylota was used to extract full trees (not only DNA data sets or markers):
    - @page2013bionames uses it to generate phylogenies for the [bionames website](http://bionames.org),
    a "database linking taxonomic names to their original descriptions, to taxa, and
    to phylogenies" generated with phylota.
    - @deepak2013extracting uses a sample of phylota trees to test their method to
    remove conflict from MUL-trees (short for multi-labeled trees), that is, phylogenetic
    trees with two or more leaves sharing a label, e.g., a species name, which can
    imply multiple conflicting phylogenetic relationships for the same set of taxa.
    - A review by @sanderson2016perspective, takes 134 595 gene trees from phylota
    GenBank rel. 176 and estimates its degree of resolutin, calculating that less
    than half of clades are supported with minilam statistical support (0.53 ± 0.32).

# Acknowledgements

We acknowledge contributions from

# References
