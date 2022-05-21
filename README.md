# BI_project_Borgs

Supervisors:
- Mikhail Rayko
- Lavrentii Danilov

Students: 
- Alexandra Kolodyazhnaya [@alvlako](https://github.com/alvlako)
- Vera Emelianenko [@Vera-Emelianenko](https://github.com/Vera-Emelianenko)  

## Introduction



## Goal and objectives 

## Workflow



## Materials and methods

### Data 

Genome sequences of Borgs and their annotated proteins were downloaded from https://ggkbase.berkeley.edu/BMp/organisms after registering on the databse website. 

### Analysing core genes

Orthologous genes were identified in all complete and near-complete Borgs with proteinortho 6.0.33, with the default parameters. The resulting table (`data/borgs.proteinortho.tsv`) was then filtered to contain only orthogroups present in 12 or more genomes, and these proteins were extracted from the fasta files using custom python scripts. Each orthogroup was aligned with MUSCLE v3.8.1551 with the default parameters (`data/alignments/group_0-75.afa.zip`). Only the alignments with > 60% identity were analysed.  

### Functional analysis of cluster proteins 

Cluster proteins were extracted with custom python scripts using the ncbi id and coordinates in identified clusters, and the obtained fasta file was annotated using the web-version of eggNOG-mapper (http://eggnog-mapper.embl.de/) (`data/cluster_proteins.emapper.annotations.tsv`). 

## Key results 

## Conclusion and further plans

## References 

Borgs are giant extrachromosomal elements with the potential to augment methane oxidation
Al-Shayeb, B., Schoelmerich, M. C., West-Roberts, J., Valentin-Alvarado, L. E., Sachdeva, R., Mullen, S., ... & Banfield, J. F. 
bioRxiv (2021). https://doi.org/10.1101/2021.07.10.451761

ggKbase: https://ggkbase.berkeley.edu/

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

Accelerated Profile HMM Searches. 
Eddy SR. 2011. PLoS Comput. Biol. 7:e1002195.

Sensitive protein alignments at tree-of-life scale using DIAMOND.
Buchfink B, Reuter K, Drost HG. 2021.
Nature Methods 18, 366–368 (2021). https://doi.org/10.1038/s41592-021-01101-x

MMseqs2 enables sensitive protein sequence searching for the analysis of massive data sets.
Steinegger M & Söding J. 2017. Nat. Biotech. 35, 1026–1028. https://doi.org/10.1038/nbt.3988

Prodigal: prokaryotic gene recognition and translation initiation site identification.
Hyatt et al. 2010. BMC Bioinformatics 11, 119. https://doi.org/10.1186/1471-2105-11-119.


