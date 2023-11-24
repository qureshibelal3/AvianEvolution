# AvianEvolution
Bionformatics final project

## Overview
This project explores the evolutionary relationships among different bird species 

## Progress
- **Data Collection:** Collected whole genome bird sequences
- **Alignment:** Used `mafft` for aligning the sequences. IQTREE to generate the tree 
- **Phylogenetic Tree Construction:** Utilized the `ape` package in R to construct a family tree.

## Scripts
- `download_bird_data.sh`: Script to download bird genome sequences.
```
#!/bin/bash

# List of species and their respective URLs
species_urls=(
  "https://ftp.ensembl.org/pub/release-110/fasta/struthio_camelus_australis/dna/Struthio_camelus_australis.ASM68674v1.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/lonchura_striata_domestica/dna/Lonchura_striata_domestica.Finch_dove_1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/cyanistes_caeruleus/dna/Cyanistes_caeruleus.Cyanistes_caeruleus_1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/lepidothrix_coronata/dna/Lepidothrix_coronata.L_coronata_1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/melopsittacus_undulatus/dna/Melopsittacus_undulatus.MelUnd1_0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/athene_cunicularia/dna/Athene_cunicularia.athCun1.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/gallus_gallus/dna/Gallus_gallus.GRCg6a.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/ficedula_albicollis/dna/Ficedula_albicollis.FicAlb_1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/serinus_canaria/dna/Serinus_canaria.SerCan1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/anas_platyrhynchos_platyrhynchos/dna/Anas_platyrhynchos_platyrhynchos.BGI_duck_1.0.dna.toplevel.fa.gz"
)

# Download and extract data for each species
for url in "${species_urls[@]}"; do
  wget "$url"
  file_name=$(basename "$url")
  gunzip "$file_name"
done
 

```
- alignment: # Multiple Sequence Alignment (MSA)

To align t gene sequences, the MAFFT tool was used. The following command was executed in the terminal:

```bash
mafft --auto data/*.fasta > alignment.fasta
```

- `phylogenetic_tree.R`: R script for constructing the phylogenetic tree.

  
## Dataset Commands
- To download Cytochrome b gene sequences: `./download_data.sh`

## Final Products

