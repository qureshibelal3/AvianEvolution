# AvianEvolution
Bionformatics final project

## Overview
This project explores the evolutionary relationships among different bird species using CYTB gene sequences

## Progress
- **Data Collection:** Collected CYTB gene bird sequences
- **Alignment:** Used `mafft` for aligning the sequences. IQTREE to generate the tree 
- **Phylogenetic Tree Construction:** Utilized the `ape` package in R to construct a family tree.

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
mafft --auto Anas_platyrhynchos_cytb_selected.fasta > Anas_platyrhynchos_cytb_selected_aligned.fasta
mafft --auto Gallus_gallus_cytb_selected.fasta > Gallus_gallus_cytb_selected_aligned.fasta
mafft --auto Serinus_canaria_cytb_selected.fasta > Serinus_canaria_cytb_selected_aligned.fasta
mafft --auto Ficedula_albicollis_cytb_selected.fasta > Ficedula_albicollis_cytb_selected_aligned.fasta
mafft --auto Struthio_camelus_cytb_selected.fasta > Struthio_camelus_cytb_selected_aligned.fasta

```

IQTREE command: 

```
cd bird3

cat Anas_platyrhynchos_cytb_selected.fasta \
    Ficedula_albicollis_cytb_selected.fasta \
    Gallus_gallus_cytb_selected.fasta \
    Serinus_canaria_cytb_selected.fasta \
    Struthio_camelus_cytb_selected.fasta > all_cytb.fasta


iqtree -s all_cytb_aligned.fasta -m LG -bb 1000 -pre cytb_tree


```

- `phylogenetic_tree.R`: R script for constructing the phylogenetic tree.

  
## Dataset Commands
- ==`

## Final Products

