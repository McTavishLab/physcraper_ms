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
date: '16 May, 2020'
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
providing a framework for comparison of phylogenies.

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
1. Obtention of molecular or morphological character data -- get DNA from some organisms and sequence it, or get it from an online repository, such as GenBank.
1. Assemble a hypothesis of homology -- Create a matrix of your character data, by aligning the sequences, in the case of molecular data.
1. Analyse this hypothesis of homology to infer phylogenetic relationships among the organisms you are studying -- Use different available programs to infer molecular evolution, trees and times of divergence.
1. Discuss the inferred relationships in the context of previous hypothesis, the biology and biogeography of the organisms, etc. -- Answer the question, *is this phylogenetic solution fair/reasonable?*

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

- The phylogenetic tree has to be in the Open Tree of Life store [@mctavish2015phylesystem].
  You can choose from a variety of published trees supporting any node of the Tree of Life. If the tree you are
  interested in is not in Open Tree of Life, you can easily upload it via the curator
  tool.
- The alignment should be a gene alignment that was used to generate the tree. The
  alignments are usually stored in a public repository such as TreeBase [@piel2009treebase; @vos2012nexml],
  DRYAD (<http://datadryad.org/>), or th ejournal were the tree was originally published.
  If the alignment is stored in TreeBase, `physcraper` can download it directly
  either from the TreeBASE website (<https://treebase.org/>)
  or through TreeBASE GitHub repository, SuperTreeBASE (<https://github.com/TreeBASE/supertreebase>).
  If the alignment is on another repository, a copy of it has to be
  downloaded by the user, and it's local path has to be provided as an argument.
- A taxon name matching step is performed to verify that all taxon names on the tips
  of the tree are in the character matrix and vice versa.
- A ".csv" file with the summary of taxon name matching is produced for the user.
- Unmatched taxon names are dropped from the tree and alignment.
  <!--***What is the minimum amount of tips necessary for a physcraper run??*** Just one!-->
  Technically, just one matching name is needed to perform the searches. See below.
- A ".tre" and ".aln" files are generated and saved for a `physcraper` run.


## DNA sequence search and cleaning

- The next step is to identify the search taxon. This must be a taxon (a named clade)
  from the NCBI taxonomy. It will be used to constraint the DNA sequence search on
  the GenBank database within that taxonomic group.
  By default, the search taxon is the most recent common ancestor (MRCA) of the
  matched taxa that is also a named clade in the NCBI taxonomy. This is refered to as the most recent common
  ancestral taxon (MRCAT) or the least inclusive common ancestral taxon (LICA).
  It can be different from the phylogenetic MRCA when the latter is an unnamed clade.
  This is done using the Open Tree API [taxonomy/mrca](https://github.com/OpenTreeOfLife/germinator/wiki/Taxonomy-API-v3#mrca).
  <!-- ***Does physcraper takes into account the focal clade from Open Tree in any way???***
  Not really, it is a search MRCA more than a taxonomic, the default is to get the ingroup from Otol, which is not the focal group.-->
  A search taxon can also be given by the user. It can be a more inclusive
  clade, if the user wants to perform a wider search, outside the MRCAT of the matched taxa, e.g., including all taxa within
  the family or the order. It can also be a less inclusive clade, if the user only
  wants to focus on enriching a particular clade/region within the tree.
  When only one taxon is matched in both the tree and alignment, an MRCAT can be
  found for that single taxon, and thus a DNA sequence search can be performed even
  with only one sequence in the alignment.
- The BLAST algorithm is used to identify similarity among DNA sequences in the GenBank nucleotide
  database within the search taxon and the remaining sequences on the alignment.
  <!--***How does the blast is setup? Is it an all-blast-all??***-->
- The DNA sequence similarity search can be done on a local database that is easily setup by the user. In this case it uses the BLASTn algorithm.
- The search can also be performed remotely, using the bioPython BLASt algorithm.
- A BLAST run is performed for each sequence in the alignment. Results of each BLAST
  are recorded. All matched sequences are saved with their corresponding GenBank
  accesion numbers that will be used to download the whole sequences into a local library.
- Matched sequences below an e-value, percentage similarity, and outside a minimum
  and maximum length threshold are discarded. This will leave out genomic sequences.
  All acepted sequences are asigned an internal identifier, and are further filtered.
- Because we usually do not have the accession number from sequences in the original
  alignment, a filtering process is needed. Accepted sequences that belong to the
  same taxon in the query sequence and that are either identical or shorter than
  the original sequence are also discarded. Only longer sequences belonging to the
  same taxon as the orignal sequence will be considered for further analyses.
- Among the remaining filtered sequences, there are usually several exemplars per taxon.
  Although it can be useful to keep some of them to, for example, investigate monophyly
  within species, there can be hundreds of exemplar sequences per taxon for some markers.
  To control the number of sequences per taxon kept for further analyses, by default
  5 sequences per taxon are chosen at random. This number can be controlled by the user.
  <!--***How does pyphlawd, or phylota does the exemplar per sepcies choosing?***-->
- Reverse complement sequences are identified and translated.
- This cycle of sequence search is performed two times. ***Is there an arhument to control the number of cycles of blast searches with new sequences***
- A fasta file containing all sequences resulting from the BLAST searches is generated for the user.

## DNA sequence alignment

- The software MUSCLE [@edgar2004muscle] is implemented for profile alignment, in
  which the original alignment is used as a template to align all new sequences.

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


# Tools on a similar track

Tools that do similar things at different levels:

Phylota [@sanderson2008phylota] - cited by 122 studies.

PHLAWD [@smith2009mega] and pyPhlawd [@smith2019pyphlawd] - baited analyses

DarwinTree [@meng2015darwintree] predecessor is Phylogenetic Analysis of Land Plants Platform (PALPP) - takes data from GenBank, EMBL and DDBJ for land plants only.

NCBIminer [@xu2015ncbiminer]

A [ruby pipeline](https://www.zfmk.de/en/research/research-centres-and-groups/taming-of-an-impossible-child-pipeline-tools-and-manuals),
only available from the [supplementary data](https://static-content.springer.com/esm/art%3A10.1186%2F1741-7007-9-55/MediaObjects/12915_2011_480_MOESM1_ESM.ZIP)
of the journal [[@peters2011taming]](https://bmcbiol.biomedcentral.com/articles/10.1186/1741-7007-9-55#Sec21)

PUmPER [@izquierdo2014pumper] - perpetual updating with newly added sequences to
GenBank

SUMAC [@freyman2015sumac] -  both “baited” analyses and single‐linkage clustering
methods, as well as a novel means of determining when there are enough overlapping data in the DNA matrix

SUPERSMART [@antonelli2017toward] - baited analyses up to bayesian divergente time
estimation

SOPHI - [@chesters2017construction] - Searches DNA sequence data from repos other
than GenBank, such as transcriptomic and barcoding repos.

PhySpeTre [@fang2019physpetree] - no sequence retrieval, just phylogenetic reconstruction
pipeline.




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
    compare the performance of SUMAC to Phylota
1. When the software was actually used to construct (partially or in full) a DNA
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
    - A 268 species phylogeny of sharks, representing all orders and 32 families [@sorenson2014effect]
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
1. When the website was used to identify sequences and markers available in
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
1. Sometimes, it was cited by mistake:
    - In this 630 tip phylogeny of the Caryophyllaceae study [@greenberg2011caryophyllaceae] it might have been originally
    cited as an example of large phylogenies that reflect well supported relationships
    from previous smaller phylogenies. However, it was removed from the text but
    not from the final list of references. The DNA data set was constructed by hand most probably.
1. Other miscellaneous uses of phylota:
    - @page2013bionames uses it to generate phylogenies for the [bionames website](http://bionames.org),
    a "database linking taxonomic names to their original descriptions, to taxa, and
    to phylogenies" generated with phylota.

# Acknowledgements

We acknowledge contributions from

# References
