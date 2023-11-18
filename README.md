# AvianEvolutionCytochromeB
Bionformatics final project

## Overview
This project explores the evolutionary relationships among different bird species based on the Cytochrome b gene.

## Progress
- **Data Collection:** Collected Cytochrome b gene sequences for various bird species. 
- **Alignment:** Used `mafft` for aligning the sequences. 
- **Phylogenetic Tree Construction:** Utilized the `ape` package in R to construct a family tree.

## Scripts
- `download_data.sh`: Script to download Cytochrome b gene sequences.
```  
#!/bin/bash

accession_numbers=("AF090338.1" "GU908131.1" "AF197835.1" "KT946691.1" "EU009397.1" "EF532935.1" "KT340631.1" "JQ864490.1" "MN356192.1" "KJ909190.1")

output_dir="data"
mkdir -p $output_dir
for accession in "${accession_numbers[@]}"
do
    echo "Downloading $accession..."
    efetch -db nucleotide -id $accession -format fasta > "$output_dir/$accession.fasta"
    echo "Downloaded $accession"
done

echo "Data download complete!"
```
- alignment: # Multiple Sequence Alignment (MSA)

To align the Cytochrome b gene sequences, the MAFFT tool was used. The following command was executed in the terminal:

```bash
mafft --auto data/*.fasta > alignment.fasta
```

- `phylogenetic_tree.R`: R script for constructing the phylogenetic tree.

  
## Dataset Commands
- To download Cytochrome b gene sequences: `./download_data.sh`

## Final Products

