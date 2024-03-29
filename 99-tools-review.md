
<!-- The md file is generated from this Rmd; please edit this file and then from R do rmarkdown::render("99-tools-review.Rmd")-->

## Tools that automatize any part of the process of phylogenetic reconstruction:

### 1\. Mining databases to generate DNA datasets suitable for phylogenetic reconstruction

| Tool                                                                                                                                                                                                                                                                                                                      | Citation                    |  Cited by   |                                                                                                                                                                           Description                                                                                                                                                                           | Supermatrix/gene tree/species tree |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | :---------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------: |
| Phylota                                                                                                                                                                                                                                                                                                                   | @sanderson2008phylota       | 122 studies |                                                                                                                                         finds sets of DNA homologs on the GenBank database; phylogenetic reconstruction                                                                                                                                         |            Supermatrix             |
| PHLAWD                                                                                                                                                                                                                                                                                                                    | @smith2009mega              | 234 studies |                                                                                                                                        Baited search of DNA markers on the GenBank database; phylogenetic reconstruction                                                                                                                                        |            Supermatrix             |
| Unnamed [ruby pipeline](https://www.zfmk.de/en/research/research-centres-and-groups/taming-of-an-impossible-child-pipeline-tools-and-manuals), only available from [supplementary data](https://static-content.springer.com/esm/art%3A10.1186%2F1741-7007-9-55/MediaObjects/12915_2011_480_MOESM1_ESM.ZIP) of the journal | @peters2011taming           | 64 studies  |                                                                                   mining public DNA databases, focuses on filtering massive amounts of mined sequences by using established “criteria of compositional homogeneity and defined levels of density and overlap”                                                                                   |            Supermatrix             |
| Unnamed                                                                                                                                                                                                                                                                                                                   | @grant2014building          | 38 studies  |                                                                       predecessor of phylotol; homolog clustering; public and/or personal DNA database; phylogenetic reconstruction; broad taxon analyses; remove contaminant sequences, based on similarity and on phylogenetic position                                                                       |            supermatrix             |
| Unnamed                                                                                                                                                                                                                                                                                                                   | @chesters2014protocol       | 10 studies  |                                                                                                             algorithm that mines GenBank data to delineate species in the insecta. The authors present a nice comparison with the phylota algorithm                                                                                                             |          Species trees??           |
| PUmPER                                                                                                                                                                                                                                                                                                                    | @izquierdo2014pumper        | 14 studies  |                                                                                                                                                    perpetual updating with newly added sequences to GenBank                                                                                                                                                     |            not sure yet            |
| DarwinTree                                                                                                                                                                                                                                                                                                                | @meng2015darwintree         |  6 studies  |                                                                                                                predecessor is Phylogenetic Analysis of Land Plants Platform (PALPP), takes data from GenBank, EMBL and DDBJ for land plants only                                                                                                                |              not sure              |
| NCBIminer                                                                                                                                                                                                                                                                                                                 | @xu2015ncbiminer            |  4 studies  |                                                                                                                                                                       part of darwintree                                                                                                                                                                        |              not sure              |
| SUMAC                                                                                                                                                                                                                                                                                                                     | @freyman2015sumac           | 19 studies  |                                                                                                 both “baited” analyses and single‐linkage clustering methods, as well as a novel means of determining when there are enough overlapping data in the DNA matrix                                                                                                  |              not sure              |
| STBase                                                                                                                                                                                                                                                                                                                    | @mcmahon2015stbase          |  7 studies  |                                                                                                                             pipeline for species tree construction and the public database of one million precomputed species trees                                                                                                                             |           species trees            |
| Unnamed                                                                                                                                                                                                                                                                                                                   | @papadopoulou2015automated  | 17 studies  |                                                                                                                                        Automated DNA-based plant identification for large-scale biodiversity assessment                                                                                                                                         |              not sure              |
| BIR                                                                                                                                                                                                                                                                                                                       | @kumar2015bir               |  6 studies  |                                                                                                                                            blast, align, identify homologs via constructed trees, curate and realign                                                                                                                                            |            supermatrix             |
| SUPERSMART                                                                                                                                                                                                                                                                                                                | @antonelli2017toward        | 35 studies  |                                                                                                                                                    baited analyses up to bayesian divergence time estimation                                                                                                                                                    |            supermatrix             |
| SOPHI                                                                                                                                                                                                                                                                                                                     | \[@chesters2017construction | 17 studies  |                                                                                                                              Searches DNA sequence data from repos other than GenBank, such as transcriptomic and barcoding repos                                                                                                                               |              not sure              |
| phyloSkeleton                                                                                                                                                                                                                                                                                                             | @guy2017phyloskeleton       |  5 studies  |                                                                                                                           focuses on taxon sampling; baited genomic sequences; public database (NCBI and JGI); marker identification                                                                                                                            |            supermatrix             |
| OneTwoTree                                                                                                                                                                                                                                                                                                                | @drori2018onetwotree        |  7 studies  |                                                                                             Web‐based, user-friendly, online tool for species-tree reconstruction, based on the *supermatrix paradigm* and retrieves all available sequence data from NCBI GenBank                                                                                              |            supermatrix             |
| pyPhlawd                                                                                                                                                                                                                                                                                                                  | @smith2019pyphlawd          |  6 studies  |                                                                                                                                                                 baited and clustering analyses                                                                                                                                                                  |      Supermatrix or gene tree      |
| Phylotol                                                                                                                                                                                                                                                                                                                  | @ceron2019phylotol          |  5 studies  | “phylogenomic pipeline to allow easy incorporation of data from high-throughput sequencing studies, to automate production of both multiple sequence alignments and gene trees, and to identify and remove contaminants. PhyloToL is designed for phylogenomic analyses of diverse lineages across the tree of life”, i.e., bacteria and unicellular eukaryotes |     supermatrix and gene trees     |
| phylotaR                                                                                                                                                                                                                                                                                                                  | @bennett2018phylotar        |   studies   |                                                                                                                                                                                                                                                                                                                                                                 |                                    |

According to @ceron2019phylotol, PhyLoTA and BIR “focus on the
identification and collection of homologous and paralog genes from
public databases such as GenBank”, while both AMPHORA and PHLAWD “focus
on the construction and refinement of robust alignments rather than the
collection of
homologs.”

### 2\. Mining databases to generate protein/aminoacid (AA) datasets suitable for phylogenetic reconstruction

AMPHORA | @wu2008simple | 458 studies | baited search; protein markers
on phylogenomic data; personal database of genomes or metagenomic data,
manually downloaded either from a public database or from private data;
phylogenetic reconstruction | Supermatrix |

### 3\. Searching phylogenetic tree databases

PhyloFinder \[@chen2008phylofinder\] - cited by 18: a search engine for
phylogenetic databases, using trees from TreeBASE - more related to
phylotastic’s goal than to updating/creating phylogenies

### 4\. Mining phylogenetic tree databases

PhyloExplorer \[@ranwez2009phyloexplorer\] - cited by 21: a python and
MySQL based website to facilitate assessment and management of
phylogenetic tree collections. It provides “statistics describing the
collection, correcting invalid taxon names, extracting taxonomically
relevant parts of the collection using a dedicated query language, and
identifying related trees in the TreeBASE database”.

### 5\. Pipeline for phylogenetic reconstruction

PhySpeTre \[@fang2019physpetree\] - no citations yet - no sequence
retrieval, just phylogenetic reconstruction pipeline.

### 5\. getting metadata and not sequences from GenBank.

Datataxa @ruiz2019datataxa - no citations yet - focus on extracting
metadata from GenBank sequence information.

## Phylota overview

Phylota was published as a website to summarize and browse the
phylogenetic potential of the GenBank database
\[@sanderson2008phylota\].

Since then, it has been cited 122 times for different reasons.

1.  As an example of a tool that mines GenBank data for phylogenetic
    reconstruction, or that is useful in any way for phylogenetics:
      - original publication of PHLAWD \[@smith2009mega\]
      - an analysis identifying research priorities and data
        requirements for resolving the red algal tree of life
        \[@verbruggen2010data\]
      - @beaulieu2012modeling cites phylota as an example study of very
        large and comprehensive phylogeny from mined DNA sequence data,
        (even if no phylogeny was really published there, only the
        method to do so)
      - a review for ecologists about phylogenetic tools
        \[@roquet2013building\]
      - a study constructing a dated seed plant phylogeny using pyPHLAWD
        \[@smith2018constructing\]
      - a study presenting an “assembly and alignment free” method for
        phylogenetic reconstruction using genomic data. It aims to be
        incorporated into a pipeline such as phylota some day
        \[@fan2015assembly\].
      - nexml format presentation \[@vos2012nexml\] - cites phylota as a
        tool that uses stored phyloinformatic data that could benefit
        from adopting nexml, to increase interoperability.
      - a study of fruit evolution, analysing a previously published
        phylogeny of 8911 tips of the Campanulidae, constructed with
        PHLAWD \[@beaulieu2013fruit\]
      - a study of Southeast Asia plant biodiversity inventory
        \[@webb2010biodiversity\] - cites phylota as a tool that would
        allow rapid phylogenetic placing of newly discovered species,
        and generation of phylogenetically informed guides for field
        identification.
      - a study of wood density for carbon stock assessments
        \[@flores2011estimating\], cites phylota as an initiative to
        “get supertrees resolved up to species level”.
      - a study proposing something similar to Open tree but applied
        only to land plants \[@beaulieu2012synthesizing\]
      - an analysis of the phylogenetic diversity-area curve
        \[@helmus2012phylogenetic\], cited phylota as a method
        alternative to phylomatic to “obtain plant phylogenetic trees
        for ecophylogenetic studies”.
      - a study generating a phylogeny of 6,098 species of vascular
        plants from China \[@chen2016tree\] - uses DarwinTree
        \[@meng2015darwintree\] and generates sequence data *de novo*
        for 781 genera.
      - a review of the state of methods and knowledge generated by
        molecular systematics \[@san2010molecular\] cites phylota as a
        tool “intended to systematize GenBank information for
        large-scale molecular phylogenetics analysis”.
      - the first phylotastic paper \[@stoltzfus2013phylotastic\] cites
        phylota as a “phylogeny related resource that provides ways to
        generate custom species trees for downstream use”.
      - @antonelli2017toward cites phylota as a “pipeline that
        pre-processes entire GenBank releases in pursuit of sufficiently
        overlapping reciprocal BLAST hits, which are then clustered into
        candidate data sets”. They also use the PHYLOTA database in its
        own pipeline.
      - @deepak2014evominer present an algorithm for mining of frequent
        subtrees (common patterns) in collections of phylogenetic trees,
        as a way to extract meaningful phylogenetic information from
        collections of trees when compared to maximum agreement subtrees
        and majority-rule trees. They cite phylota as one of such tree
        collections available along with TreeBASE \[@piel2009treebase\].
      - @ranwez2009phyloexplorer cites phylota as a “program providing
        basic statistics on data availability for molecular datasets”.
        They propose a tool to upload and explore user phylogenies to
        obtain detailed summary statistics on user tree collections.
      - @freyman2015sumac cites phylota as a tool that “provides a web
        interface to view all GenBank sequences within taxonomic groups
        clustered into homologs” but that does not mine for targeted
        sequences, as opposed to NCBIminer or PHLAWD. They compare the
        performance of SUMAC to Phylota. This is also presented in their
        PhD dissertation \[@freyman2017phylogenetic\].
      - @chesters2013resolving cites phylota as a data mining tool that
        compiles metadata from mining of public DNA databases “for
        construction of large phylogenetic trees and multiple gene sets”
        and that the authors have recognised that gene annotations in
        public databases are insufficient and that careful partitioning
        of orthologous sequences is needed for supermatrix construction.
        @chesters2013resolving present a procedure that minimizes the
        problem of forming multilocus species units in a large
        phylogenetic data set using algorithms from graph theory.
      - @chesters2014protocol present an algorithm to delineate species
        form GenBank DNA data, and cites phylota as a tool that
        partitions “the contents of a database according to homology”,
        by “grouping of database sequences according to internal
        criteria”, searching “from a standardized set of references
        \[…\] patterns in sequence similarity and overlap.”
      - the paper presenting phylotaR, a pipeline that recreates the
        phylota output but uses the most updated GenBank release, and is
        available in R \[@bennett2018phylotar\], cites phylota as its
        predecessor and inspiration. The authors mention that phylotaR
        pipeline mimics phylota’s pipeline but with improvements.
      - The paper presenging PhyloBase \[@jamil2016visual\], cites
        phylota as one of its resources to get phylogenies, along with
        TreeBASE and others.
      - The paper presenting STBase, a database of one million
        precomputed species trees \[@mcmahon2015stbase;
        @deepak2013managing\], cites phylota as a databse of gene trees
        or mul-trees, “trees having multiple sequences with the same
        taxon name”.
      - @drori2018onetwotree present a Web‐based, user-friendly, online
        tool for species-tree reconstruction, based on the *supermatrix
        paradigm* and retrieves all available sequence data from NCBI
        GenBank. They cite phylota in the intro as a tool that is
        “designed to provide users with precomputed sets of clusters
        that were assembled through a single‐linkage clustering approach
        and additionally provides precomputed gene trees that were
        reconstructed for each cluster. In particular, the results
        obtained by PhyLoTa are taxonomically constrained; that is, all
        sequences of the most recent common ancestor are collected even
        if one specifies only part of a clade”.
      - A study developing a tool to link wikipedia data to NCBI
        taxonomy \[@page2011linking\] cites phylota as a phylogenetic
        resource that uses the NCBI taxonomy.
      - the study that present DarwinTree \[@meng2015darwintree\], and
        all derived studies: the study presenting an approach to screen
        sequence data for The Platform for Phylogenetic Analysis of Land
        Plants (PALPP), using the MapReduce paradigm to parallelize
        BLAST \[@yong2010screening\], as well as @gao2011solution,
        @li2013partfasttree, @meng2014rapidtree, @meng2015sotree, and
        @meng2015solution, all cite phylota using the exact same
        introduction and sentence: as one among other “studies based on
        data mining large numbers of taxa or loci”.
      - A study presenting a tool to asses gene sequence quality for
        automatic construction of databases \[@meng2012gsqct\], as well
        as their parallelized version using MapReduce
        \[@meng2012cloud\], cite phylota (along with @yong2010screening)
        as a tool that relies on sequence similarity (BLAST) and not
        taxon name annotations in the database, for mining large numbers
        of taxa or loci, without making any control on the quality of
        the sequencing.
      - A review on online plant databases aiming to “provide
        recommendations for current information managers and developers
        concerning the user interface and experience; and to provide a
        picture about the possible directions to take for those in
        charge of the creation of information at all levels”. They cite
        phylota as a tool allowing researchers “to acces equally and
        globally, without travel, a \[phylogenetic?\] model of plants at
        the kingdom level” \[@jones2014trends\].
      - a paper aiming to establish an online information system for the
        legumes and to outline “best practices for development of a
        legume portal to enable data sharing and a better understanding
        of what data are available, missing, or erroneous, and
        ultimately facilitate cross-analyses and collaboration within
        the legume-systematics community and with other stakeholders”
        \[@bruneau2019towards\], cites phylota (along with supersmart
        and pyphlawd) as a “pipeline for large-scale retrieval of
        GenBank data of particular taxa or clades”. In their Table 1,
        they also list phylota as a potential data source for developing
        a legume portal.
      - A study on morphological evolution of electric fish skull, that
        uses phylotaR to retrieve sequences of the family Apteronotidae,
        order Gymnotiformes \[@evans2019bony\], cites phylota as the
        inspiration and fundament of phylotaR.
      - A phylogenetic revision of the Gymnotidae fish (Teleostei:
        Gymnotiformes), uses phylotaR to retrieve seqeunces, but cites
        phylota as “a pipeline that implements BLAST searches to both
        identify and download sequence clusters for listed taxonomic
        groups to assemble a robust collection of sequences in a
        reproducible way based on publicly-available gene sequences
        while avoiding selection bias on the part of the assembler”.
      - A master thesis on SearchTree, a “software tool that allows
        users to query efficiently on an arbitrary user taxon list and
        returns high scoring matches from approximately one billion
        phylogenetic trees being constructed from molecular sequence
        data in GenBank” \[@deepak2010searchtree\], that seems to be the
        preliminary work for STBase \[@mcmahon2015stbase\], cites
        phylota as “a standard strategy, to assemble sets of homologous
        sequences (clusters) from a database of all-against-all BLAST
        searches, \[in which\] clusters are constructed in the context
        of the NCBI taxonomy tree for convenience of display, thus child
        clusters are contained within parent clusters, following the
        NCBI hierarchy”. In opposition, SearchTree uses true
        agglomerative hierarchical clustering (AHC: @day1984efficient)
        based on the BLAST estimates of sequence dissimilarity rather
        than the NCBI tree".
      - a recent review on the state of large phylogeny (namely insects)
        generation using tools of the data-driven era
        \[@chesters2019phylogeny\] cites phylota as a tool for homology
        inference and retrieval.
      - the study presenting phylotol \[@ceron2019phylotol\], cites
        phylota as a tool that “focus on the identification and
        collection of homologous genes from public databases”.
      - The [iPTOL
        project](https://www.researchgate.net/profile/Douglas_Soltis/publication/228815637_Assembling_the_Tree_of_Life_for_the_Plant_Sciences_iPTOL/links/56a7c6bc08aeded22e3700dc.pdf)
        cites phylota as a resource of phylogenetic trees.
      - @mahmood2015avian PhD dissertation presents a database of avian
        Raptor sequences (raptorbase), based on the phylota pipeline.
      - @ruiz2019datataxa develops datataxa and cite phylota as
        “software that has been developed to mine the massive amount
        of information stored in GenBank”, along with its R version
        \[phylotaR; @bennett2018phylotar\] and restez
        <https://www.rdocumen-tation.org/packages/restez/versions/1.0.0>.
      - The phylotastic project \[@stoltzfus2013phylotastic\] cites
        phylota as a “phylogeny-related resource providing ways to
        generate custom species trees *de novo* for downstream use”
        along with CIPRES.
2.  When the software was actually used to construct (partially or in
    full) a DNA data set to be used for phylogenetic reconstruction:
      - A 1000 tip phylogeny of the family of the nightshades
        \[@sarkinen2013solanaceae\]
      - A 56 tip phylogeny of crustacean zooplancton
        \[@helmus2010communities\] – ecological study
      - A 63 tip phylogeny of the Salmonidae family
        \[@crete2012salmonidae\]
      - A 321 tip phylogeny of Testudines \[@thomson2010sparse\]
      - A 69 taxa phylogeny of the family Cyprinodontidae of the pupfish
        \[@martin2011trophic\]
      - A 2,957 taxa phylogeny of the class Moniloformopses of living
        ferns \[@lehtonen2011towards\]
      - A 2,573 species phylogeny of the Papilionoidea
        \[@hardy2014specialization\]
      - A 23 taxa phylogeny of the California flora
        \[@anacker2011origins\]
      - Phylogenies of 6 different clades of flowering plants
        representing an independent evolutionary origin of extrafloral
        nectaries: *Byttneria* (Malvaceae), *Pleopeltis*
        (Polypodiaceae), *Polygoneae* (Polygoneaceae), *Senna*
        (Fabaceae), *Turnera* (Passifloraceae), and *Viburnum*
        (Adoxaceae) \[@weber2014defense\].
      - To supplement DNA data sets of various pre-existing mammalian
        phylogenetic trees sampled at different taxonomic levels
        \[@faurby2015species\]
      - A 900 species tree of muroid rodents, Muroidea
        \[@steppan2017muroid\], where 300 species were newly added by
        the study and the rest obtained using phylota.
      - A 95 taxa phylogeny of Gymnosperms, focused on Ephedra, Gnetales
        \[@ickert2009fossil\]
      - A 1061 genera phylogeny of the Oscine birds
        \[@selvatti2015paleogene\]
      - A 268 species phylogeny of sharks, representing all 8 orders and
        32 families \[@sorenson2014effect; @sorenson2014evolution\]
      - A 466 species phylogeny of the Proteaceae, focusing on the
        species found in the Cape Floristic Region
        \[@tucker2012incorporating\].
      - A series of small phylogenies of unreported exact size, of
        sister groups of gall-forming insects \[@hardy2010gall\].
      - A 196 species phylogeny of the family Boraginaceae
        \[@nazaire2012broad\]. The authors actually found data for 318
        Boraginaceae spp using phylota, but decided to reduce their data
        set to focus on the monophyly of genus *Mertensia*.
      - A phylogeny of 401 species of scale insects Coccoidea, Hemiptera
        \[@ross2013large\], with some sequences generated *de novo*.
      - Two phylogenies sampling all species of two different clades of
        insectivorous lizards, agamids and diplodactyline geckos, groups
        considered to be radiating in the Australia’s Great Victoria
        Desert \[@rabosky2011species\]
      - A phylogeny of 91 species of sparid and centracanthid fishes,
        Sparidae, Percomorpha, plus 2 outgroups, a lethrinid and a
        nemipterid exemplar \[@santini2014first\].
      - Updating a phylogeny of Arecaceae, constructing relationships in
        6 cldes within the group: subfamilies Calamoideae and
        Coryphoideae, the tribe Ceroxyleae within subfamily
        Ceroxyloideae and three groups within subfamily Arecoideae: (1)
        Iriarteeae,
    <!-- end list -->
    2)  Cocoseae: Attaleinae except Beccariophoenix and (3) a group
        containing six tribes; Euterpeae, Leopoldinieae, Pelagodoxeae,
        Manicarieae, Geonomateae and Areceae \[@faurby2016all\].
    <!-- end list -->
      - A phylogeny of 768 Gesneriaceae species and 58 outgroups for a
        total species sampling of 826 taxa \[@roalson2016distinct\] some
        sequence were generated *de novo*.
      - A phylogeny of 47 species of scombrid fishes, with 2 outgroups,
        a gempylid and a trichiurid \[@santini2013first\].
      - to update a dataset underlying a large-scale fern phylogeny
        \[@lehtonen2017environmentally\], data set in
        <https://zenodo.org/record/345670#.Xr9QFRPYqqg>, also in
        TreeBASE, but it is one of those studies that is broken.
      - A phylogeny of 13 species of billfishes, order Istiophoriformes:
        Acanthomorpha, and four outgroups \[@santini2013first\]
      - A phylogeny of 765 aphid species, family Aphididae
        \[@hardy2015evolution\]
      - A phylogeny of less than 100 taxa of the family Ranunculaceae
        \[@lehtonen2016sensitive\], even though they retrieved info from
        phylota for 194 taxa within the family, they reduced their data
        set because of low sampling of markers for some taxa.
      - A phylogeny of 144 neobatrachian genera, assuming the
        monophyletic status of genera to increase matrix-filling levels
        \[@frazao2015gondwana\].
      - A 179 species phylogeny of the bird family Picidae (woodpeckers,
        piculets, and wrynecks) \[@dufort2016augmented;
        @dufort2015coexistence\], augmented with data from an updated
        GenBank release and newly sequenced data.
      - A phylogeny of species of freshwater fish endemic to
        NorthAmerica \[@strecker2014fish\], phylota found data for 54
        out of 66 spp.
      - A phylogeny of 520 species of the order Ericales
        \[@hardy2012testing\]
      - A phylgeny of 16 fish species of the family Sphyraenidae
        (Percomorpha), as well as two outgroup species of the
        Centropomidae (barracudas) \[@santini2015first\]
      - A phylogeny of 34 vole species, Arvicolinae, Rodentia
        \[@garcia2016role\]
      - @kolmann2017dna uses phylota to download all 1691 co1 sequences
        belonging to the order Carchariniformes, to place
        phylogenetically DNA samples obtained from fish markets.
      - A phylogeny of 329 bird species in the Tyrannidae (77% of the
        species in the family) \[@gomez2020speciation;
        @gomez2015behavioral\]
      - Retrive 145 sequences registered as *Holothuria* species, but
        kept 84 as ingroup, plus 4 outgroup sequences from *Stichopus
        ocellatus*, all belonging to the order Apodida of sea cucumbers
        \[@kamarudin2016phylogenetic\]
      - On a master thesis, to get the sequences of the outgroups of
        Melinidinae, family Poaceae, namely several spp of the subfamily
        Panicoideae, plus *Gynerium sagittatum*, *Chasmanthium
        latifolium*, and *Zea mays*, \[@salariato2010filogenia\].
        Interestingly, phylota was not used in the published study of
        the thesis \[@salariato2010molecular\]. Ingroup sequences were
        generated *de novo*.
      - On a PhD thesis, to construct a phylogeny of Platyrrhini
        (internal group), Catarrhini (outgroup), and Tarsiiformes
        @pereira2013padroes. Have not found a published study.
      - The 10k trees project \[@arnold201010ktrees\] uses phylota to
        construct a tree of 301 primate species and the outgroup species
        *Galeopterus variegates*, a tree of 17 extant odd-toed ungulates
        species and the outgroup species *Bos taurus*, and a tree of 70
        different species of carnivorans and *Equus caballus* as
        outgroup. However, the do not cite it on the paper, but only on
        their documentation
        <http://www.academia.edu/download/49690788/10kTrees_Documentation.pdf>.
      - @freyman2015sumac \[also in @freyman2017phylogenetic\], use
        phylota to construct a phylogeny (or maybe only mine genbank???)
        of the Onagraceae and Lythracea, and compare it to the tool they
        propose, SUMAC.
      - @blackmon2017synthesis PhD study applies phylota to reconstruct
        a 822 mite species tree.
      - A study of the effect of poliploidy on niche evolution
        \[@baniaga2018polyploid\], uses phylota to get a DNA data set
        for 132 unique taxa of vascular plants from 16 families and 25
        genera, and a tree of 33 genera from 20 different families
        comprising 1706 taxa.
3.  When the website was used to identify sequences and markers
    available in GenBank for a particular group. In this cases, the
    dataset mining was either performed with other tools, or not
    performed at all and just used for discussion:
      - A 812 tips phylogeny of the Order Chiroptera
        \[@shi2015speciation\] – dataset constructed with PHLAWD
      - A 1276 tips phylogeny of the Fabaceae \[@legume2013legume\] –
        dataset constructed by hand (I think??)
      - A review of dated phylogenies of fire-prone tropical savanna
        species from Brazil \[@simon2012cerrado\] – just for discussion
        of the lack of markers available for these species on GenBank
      - A review of the phylogeetic sof the Apicomplexa, a parasitic
        phylum on unicellular protists \[@morrison2009apicomplexa\].
      - Three data sets from phylota (the suborder Pleurodira of
        side-necked turtles; the family Cactaceae of cacti; and the
        Amorpheae, a clade of legumes) were used to demonstrate and
        exemplify phylogenetic decisiveness
        \[@sanderson2010phylogenomics\]
      - Mentioned in a PHD thesis \[@gagnon2016systematique\], but not
        on the final publication \[@gagnon2016new\], phylota was used to
        state that there are very few sequences available for the
        Legumes (7,482 out of 19,500 spp) on GenBank’s release 194
        (Feb2013).
4.  Sometimes, it was cited by mistake:
      - In this 630 tip phylogeny of the Caryophyllaceae study
        \[@greenberg2011caryophyllaceae\] it might have been originally
        cited as an example of large phylogenies that reflect well
        supported relationships from previous smaller phylogenies.
        However, it was removed from the text but not from the final
        list of references. The DNA data set was constructed by hand
        most probably.
      - a study reconstructing the insect tree of life with 49,358
        species, 13,865 genera, and 760 families within the order
        Insecta \[@chesters2017construction\], uses its own algorithm
        (SOPHI) to mine public DNA databases \[@chesters2014protocol\].
        It does not reference to phylota in the main text (they should
        bc they used it), but includes it in their references.
5.  When phylota was used to extract full trees (not only DNA data sets
    or markers):
      - @page2013bionames uses it to generate phylogenies for the
        [bionames website](http://bionames.org), a “database linking
        taxonomic names to their original descriptions, to taxa, and to
        phylogenies” generated with phylota.
      - @deepak2013extracting uses a sample of phylota trees to test
        their method to remove conflict from MUL-trees (short for
        multi-labeled trees), that is, phylogenetic trees with two or
        more leaves sharing a label, e.g., a species name, which can
        imply multiple conflicting phylogenetic relationships for the
        same set of taxa.
      - A review by @sanderson2016perspective, takes 134 595 gene trees
        from phylota GenBank rel. 176 and estimates its degree of
        resolutin, calculating that less than half of clades are
        supported with minilam statistical support (0.53 ± 0.32).
