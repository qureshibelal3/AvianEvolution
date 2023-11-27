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
  "https://ftp.ensembl.org/pub/release-110/fasta/lonchura_striata_domestica/dna/Lonchura_striata_domestica.LonStrDom1.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/cyanistes_caeruleus/dna/Cyanistes_caeruleus.cyaCae2.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/lepidothrix_coronata/dna/Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/melopsittacus_undulatus/dna/Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/athene_cunicularia/dna/Athene_cunicularia.athCun1.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/gallus_gallus/dna/Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/ficedula_albicollis/dna/Ficedula_albicollis.FicAlb1.5.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/serinus_canaria/dna/Serinus_canaria.SCA1.dna.toplevel.fa.gz"
  "https://ftp.ensembl.org/pub/release-110/fasta/anas_platyrhynchos_platyrhynchos/dna/Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel.fa.gz"
)



# Download and unzip for each species
wget -O Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/anas_platyrhynchos_platyrhynchos/dna/Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel.fa.gz
gunzip Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel.fa.gz

wget -O Athene_cunicularia.athCun1.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/athene_cunicularia/dna/Athene_cunicularia.athCun1.dna.toplevel.fa.gz
gunzip Athene_cunicularia.athCun1.dna.toplevel.fa.gz

wget -O Cyanistes_caeruleus.cyaCae2.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/cyanistes_caeruleus/dna/Cyanistes_caeruleus.cyaCae2.dna.toplevel.fa.gz
gunzip Cyanistes_caeruleus.cyaCae2.dna.toplevel.fa.gz

wget -O Ficedula_albicollis.FicAlb1.5.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/ficedula_albicollis/dna/Ficedula_albicollis.FicAlb1.5.dna.toplevel.fa.gz
gunzip Ficedula_albicollis.FicAlb1.5.dna.toplevel.fa.gz

wget -O Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/gallus_gallus/dna/Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel.fa.gz
gunzip Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel.fa.gz

wget -O Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/lepidothrix_coronata/dna/Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel.fa.gz
gunzip Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel.fa.gz

wget -O Lonchura_striata_domestica.LonStrDom1.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/lonchura_striata_domestica/dna/Lonchura_striata_domestica.LonStrDom1.dna.toplevel.fa.gz
gunzip Lonchura_striata_domestica.LonStrDom1.dna.toplevel.fa.gz

wget -O Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/melopsittacus_undulatus/dna/Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel.fa.gz
gunzip Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel.fa.gz

wget -O Serinus_canaria.SCA1.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/serinus_canaria/dna/Serinus_canaria.SCA1.dna.toplevel.fa.gz
gunzip Serinus_canaria.SCA1.dna.toplevel.fa.gz

wget -O Struthio_camelus_australis.ASM69896v1.dna.toplevel.fa.gz https://ftp.ensembl.org/pub/release-110/fasta/struthio_camelus_australis/dna/Struthio_camelus_australis.ASM69896v1.dna.toplevel.fa.gz
gunzip Struthio_camelus_australis.ASM69896v1.dna.toplevel.fa.gz


# Unwrap the DNA sequences for each species

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel.fa > Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Athene_cunicularia.athCun1.dna.toplevel.fa > Athene_cunicularia.athCun1.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Cyanistes_caeruleus.cyaCae2.dna.toplevel.fa > Cyanistes_caeruleus.cyaCae2.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Ficedula_albicollis.FicAlb1.5.dna.toplevel.fa > Ficedula_albicollis.FicAlb1.5.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel.fa > Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel.fa > Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Lonchura_striata_domestica.LonStrDom1.dna.toplevel.fa > Lonchura_striata_domestica.LonStrDom1.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel.fa > Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Serinus_canaria.SCA1.dna.toplevel.fa > Serinus_canaria.SCA1.dna.toplevel_unwrap.fa

awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Struthio_camelus_australis.ASM69896v1.dna.toplevel.fa > Struthio_camelus_australis.ASM69896v1.dna.toplevel_unwrap.fa


```
- alignment: # Multiple Sequence Alignment (MSA)

To align t gene sequences, the MAFFT tool was used. The following command was executed in the terminal:

```
mafft --auto Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel_unwrap.fa > Anas_platyrhynchos_platyrhynchos.CAU_duck1.0.dna.toplevel_aligned.fa

mafft --auto Athene_cunicularia.athCun1.dna.toplevel_unwrap.fa > Athene_cunicularia.athCun1.dna.toplevel_aligned.fa

mafft --auto Cyanistes_caeruleus.cyaCae2.dna.toplevel_unwrap.fa > Cyanistes_caeruleus.cyaCae2.dna.toplevel_aligned.fa

mafft --auto Ficedula_albicollis.FicAlb1.5.dna.toplevel_unwrap.fa > Ficedula_albicollis.FicAlb1.5.dna.toplevel_aligned.fa

mafft --auto Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel_unwrap.fa > Gallus_gallus.bGalGal1.mat.broiler.GRCg7b.dna.toplevel_aligned.fa

mafft --auto Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel_unwrap.fa > Lepidothrix_coronata.Lepidothrix_coronata-1.0.dna.toplevel_aligned.fa

mafft --auto Lonchura_striata_domestica.LonStrDom1.dna.toplevel_unwrap.fa > Lonchura_striata_domestica.LonStrDom1.dna.toplevel_aligned.fa

mafft --auto Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel_unwrap.fa > Melopsittacus_undulatus.bMelUnd1.mat.Z.dna.toplevel_aligned.fa

mafft --auto Serinus_canaria.SCA1.dna.toplevel_unwrap.fa > Serinus_canaria.SCA1.dna.toplevel_aligned.fa

mafft --auto Struthio_camelus_australis.ASM69896v1.dna.toplevel_unwrap.fa > Struthio_camelus_australis.ASM69896v1.dna.toplevel_aligned.fa
```

- `phylogenetic_tree.R`: R script for constructing the phylogenetic tree.

  
## Dataset Commands
- `

## Final Products

