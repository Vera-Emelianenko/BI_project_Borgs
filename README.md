# Borgs - new entities in archaeal genomes?

This project was performed as a spring semester project in the [Bioinformatics Institute](https://bioinf.me/en) (academic year 2021-2022). 

Supervisors:
- Mikhail Rayko
- Lavrentii Danilov

Students: 
- Alexandra Kolodyazhnaya [@alvlako](https://github.com/alvlako)
- Vera Emelianenko [@Vera-Emelianenko](https://github.com/Vera-Emelianenko)  

## Introduction

In a preprint published on bioarchive in July 2021, authours describe misterious new entities in archeal genomes [(Al-Shayeb et al., 2021.)](https://www.biorxiv.org/content/10.1101/2021.07.10.451761v1.full). According to the authors, these genomic elements are associated with *Methanoperedens* archaea, range in size between ~6,5 - 9 Mb, contain mostly hypothetical proteins and share some structural features. Authours claim that this elements are neither plasmids nor viruses and at the same time they are not the part of the *Methanoperedens* chromosome. The definition of these elements is somewhat ambiguous. Authours define them them the following way: "We infer that these are a new type of archaeal extrachromosomal element with a distinct evolutionary origin. Gene sequence similarity, phylogeny, and local divergence of sequence composition indicate that many of their genes were assimilated from methane-oxidizing Methanoperedens archaea. We refer to these elements as “Borgs”". 

We used the Borgs sequences published in this paper along with the open-source metagenomic data to find out what are Borgs, how can they be defined and whether they have representatived in metagenomic data. 

## Goal and objectives 

The main goal of the project was to find, annotate and classify Borg-like entities from publicly available metagenomes.

## Workflow

![Workflow](workflow.png)

## Materials and methods

### Data 

Genome sequences of Borgs and their annotated proteins were downloaded from https://ggkbase.berkeley.edu/BMp/organisms after registering on the databse website. 

### Nucleotide blast of Borg contigs

Complete borg genomes were blasted against the nr/nt database with 'blastn', using 'Archaea environmental samples (taxid:48510)' as organism.

### Finding new Borgs

The archaeal metagenomic environmental samples nucleotide sequences of > 20 000 bp were downloaded from NCBI (by taxonomy ID: 48510). The protein sequences were obtained with Prodigal. Complete and incomplete Borg genomes were downloaded and annotated with Prodigal. The resulted proteins were used for searching against archaeal metagenomic proteome with MMseqs2 profile search.

### GC-content comparison

The GC-content information was extracted from Prodigal output for archaeal metagenomic and Borgs' sequences. The GC-content distribution was plotted with R ggplot2.


### Identification of the core genes

Orthologous genes were identified in all complete and near-complete Borgs with proteinortho 6.0.33, with the default parameters. The resulting table (`data/borgs.proteinortho.tsv`) was then filtered to contain only orthogroups present in 12 or more genomes, and these proteins were extracted from the fasta files using custom python scripts. Each orthogroup was aligned with MUSCLE v3.8.1551 with the default parameters (`data/alignments/group_0-75.afa.zip`). Only the alignments with > 60% identity were analysed.  

### Functional analysis of new Borgs proteins 

New Borgs proteins were extracted with custom python scripts using the ncbi id and coordinates, and the obtained fasta file was annotated using the web-version of eggNOG-mapper (http://eggnog-mapper.embl.de/) (`data/cluster_proteins.emapper.annotations.tsv`). The same annotation was performed for the archeal metagenome proteins (`archaea_metagenomes_combined_lin.faa`, `microbiome_proteins.emapper.annotations.tsv`). KEGG enrichment analysis was performed in R using the enricher() function of the clusterProfiler package, with the default options, using archeal metagenome proteins + borg cluster proteins as a universe. Pie-chart visualisations were created using BlastKOALA (https://www.kegg.jp/blastkoala/) with Prokaryotes as taxonomy group and species_prokaryotes as KEGG GENES database. 

### Phylogeny reconstruction

The most represented protein of the complete and incomplete Borgs was derived from the biggest protein cluster. The protein clusters were obtained with `mmseqs cluster` with the 0.8 sequence identity threshold (`--min-seq-id 0.8`). The cluster representative protein was used to blast against bacteria/archaea/eukaryotes/viruses (blastp, "nr/nt database", "include <one of the taxa>"). From the blast results, up to 10 matches per taxon were extracted. Then protein members of the biggest Borgs' cluster (excluding paralogs) and the blastp results were aligned with EBI Muscle (https://www.ebi.ac.uk/Tools/services/rest/muscle). The tree was build from the alignment with iqtree (http://iqtree.cibiv.univie.ac.at) and visualized with iTOL (https://itol.embl.de/tree/1347638133273481652347057).

## Key results 

 - New elements similar to Borgs were discovered in archaeal metagenomes by protein homology. 
 -  The core genes of the Borgs were identified, showing that Borgs are related and have some common genes or pathways. The functional and pathway analysis has revealed the enrichment in metabolic genes.
 
 ![image](https://user-images.githubusercontent.com/56854264/169652661-f1fc257f-a2a8-4412-890b-7830889da997.png)

 - The comparison of the GC-content of Borgs and archaeal metagenomic samples has shown that Borgs have a very characteristic peak which differs from the wide distribution in archeal sequences.
 
![image](https://user-images.githubusercontent.com/56854264/169651457-bd74a5e2-0e39-46fc-a092-e69767b73701.png)
 
 - The tree based on the homologs of the most representative Borg protein, demonstrates that Borgs, with the one exception, form the separate clade which seems to be related to the archaeal clade. 
 
 ![image](https://user-images.githubusercontent.com/56854264/169652614-f7888eb7-e044-4e01-bdd6-f2a997ce4b1c.png)

## Conclusions and further plans

 The current work shows that Borgs are most probably distinct entitites, having some common signatures (metabolic genes), allowing the discovery of the new Borgs-like elements. Borgs seem to be related to archaea but separated from them some time ago accordingly to the phylogenetic and GC-content analysis. 
 In the future, the k-mers analysis to confirm Borgs' separation from archaea and exploration of the whole contigs where the new Borg-like elements were found are planned.


## References 

Borgs are giant extrachromosomal elements with the potential to augment methane oxidation
Al-Shayeb, B., Schoelmerich, M. C., West-Roberts, J., Valentin-Alvarado, L. E., Sachdeva, R., Mullen, S., ... & Banfield, J. F. 
bioRxiv (2021). https://doi.org/10.1101/2021.07.10.451761

ggKbase: https://ggkbase.berkeley.edu/

Database resources of the national center for biotechnology information.
Sayers, Eric W., Tanya Barrett, Dennis A. Benson, Evan Bolton, Stephen H. Bryant, Kathi Canese, Vyacheslav Chetvernin et al.
Nucleic acids research 39, no. suppl_1 (2010): D38-D51. DOI: 10.1093/nar/gkab1112

MUSCLE: multiple sequence alignment with high accuracy and high throughput. 
Edgar, R.C., 2004. 
Nucleic acids research, 32(5), pp.1792-1797. doi: 10.1093/nar/gkh340

eggNOG-mapper v2: functional annotation, orthology assignments, and domain 
prediction at the metagenomic scale. Carlos P. Cantalapiedra, 
Ana Hernandez-Plaza, Ivica Letunic, Peer Bork, Jaime Huerta-Cepas. 2021.
Molecular Biology and Evolution, msab293, https://doi.org/10.1093/molbev/msab293

eggNOG 5.0: a hierarchical, functionally and phylogenetically annotated
orthology resource based on 5090 organisms and 2502 viruses. Jaime
Huerta-Cepas, Damian Szklarczyk, Davide Heller, Ana Hernández-Plaza, Sofia
K Forslund, Helen Cook, Daniel R Mende, Ivica Letunic, Thomas Rattei, Lars
J Jensen, Christian von Mering, Peer Bork Nucleic Acids Res. 2019 Jan 8;
47(Database issue): D309–D314. doi: 10.1093/nar/gky1085 

IQ-TREE 2: New models and efficient methods for phylogenetic inference in the genomic era.  
 B.Q. Minh, H.A. Schmidt, O. Chernomor, D. Schrempf, M.D. Woodhams, A. von Haeseler, R. Lanfear (2020).
 Mol. Biol. Evol. https://doi.org/10.1093/molbev/msaa015
 
Interactive Tree Of Life (iTOL) v5: an online tool for phylogenetic tree display and annotation.
Letunic I and Bork P (2021) Nucleic Acids Res doi: 10.1093/nar/gkab301 

Accelerated Profile HMM Searches. 
Eddy SR. 2011. PLoS Comput. Biol. 7:e1002195.

Sensitive protein alignments at tree-of-life scale using DIAMOND.
Buchfink B, Reuter K, Drost HG. 2021.
Nature Methods 18, 366–368 (2021). https://doi.org/10.1038/s41592-021-01101-x

MMseqs2 enables sensitive protein sequence searching for the analysis of massive data sets.
Steinegger M & Söding J. 2017. Nat. Biotech. 35, 1026–1028. https://doi.org/10.1038/nbt.3988

Prodigal: prokaryotic gene recognition and translation initiation site identification.
Hyatt et al. 2010. BMC Bioinformatics 11, 119. https://doi.org/10.1186/1471-2105-11-119.

BlastKOALA and GhostKOALA: KEGG tools for functional characterization of genome and metagenome sequences. 
Reference: Kanehisa, M., Sato, Y., and Morishima, K. 2016. 
J. Mol. Biol. 428, 726-731
