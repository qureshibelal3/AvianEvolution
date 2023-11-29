# AvianEvolution
Bionformatics final project

## Overview
This project explores the evolutionary relationships among different bird species using CYTB gene sequences

## Progress
- **Data Collection:** Collected CYTB gene bird sequences
- **Alignment:** Used `mafft` for aligning the sequences. IQTREE to generate the tree 
- **Phylogenetic Tree Construction:** Utilized the `ape` and `ggtree` packages in R to construct a family tree.

## Scripts
```
#!/bin/bash


# Anas platyrhynchos
esearch -db nucleotide -query 'Anas platyrhynchos CYTB' | efetch -format fasta > Anas_platyrhynchos_cytb.fasta

# Ficedula albicollis
esearch -db nucleotide -query 'Ficedula albicollis CYTB' | efetch -format fasta > Ficedula_albicollis_cytb.fasta

# Gallus gallus
esearch -db nucleotide -query 'Gallus gallus CYTB' | efetch -format fasta > Gallus_gallus_cytb.fasta

# Serinus canaria
esearch -db nucleotide -query 'Serinus canaria CYTB' | efetch -format fasta > Serinus_canaria_cytb.fasta

# Struthio camelus
esearch -db nucleotide -query 'Struthio camelus CYTB' | efetch -format fasta > Struthio_camelus_cytb.fasta



```
- alignment: # Multiple Sequence Alignment (MSA)

To align cytb gene sequences, the MAFFT tool was used. The following command was executed in the terminal:

```
cat Anas_platyrhynchos_cytb_selected.fasta \
    Ficedula_albicollis_cytb_selected.fasta \
    Gallus_gallus_cytb_selected.fasta \
    Serinus_canaria_cytb_selected.fasta \
    Struthio_camelus_cytb_selected.fasta > all_cytb.fasta

mafft --auto all_cytb.fasta > all_cytb_aligned.fasta


```
IQTREE command: 

```


iqtree -s all_cytb_aligned.fasta -m GTR -bb 1000 -pre cytb_tree



```
R script:
```
library(ggtree)

# Paste the content of your "contree" file within the quotes
shh_tree <- "(Anas_platyrhyncos:0.7919033481,((Ficedulla_albicollis:0.0670936537,Serinus_canaria:0.0893013987)72:0.0546753501,Gallus_gallus:0.1175383905)46:0.0251519198,Struthio_camelus:0.0795765884);"

# Read the tree
shh_tree <- read.tree(text=shh_tree)

# Plot the tree with species names
ggtree(shh_tree) + 
  geom_tiplab(geom="text", hjust=1, offset=0.5, size=5) +
  theme_tree2()

```
  

## Final Products


