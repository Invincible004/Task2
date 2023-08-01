# Task2
Bash script to count the average length of proteins from the compressed FASTA file NC_000913.faa.gz.

#!/bin/bash

# Download the compressed fasta file
wget -O NC_000913.faa.gz ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/005/845/GCA_000005845.2_ASM584v2/GCA_000005845.2_ASM584v2_protein.faa.gz

# Count the number of protein sequences in the fasta file
num_sequences=$(zcat NC_000913.faa.gz | grep -c "^>")

# Count the total number of amino acids in all protein sequences
total_amino_acids=$(zcat NC_000913.faa.gz | grep -v "^>" | tr -d "\n" | wc -m)

# Calculate the average length of proteins
average_length=$(echo "scale=2; $total_amino_acids / $num_sequences" | bc)

# Print the result
echo "The average length of proteins in E. coli MG1655 is $average_length amino acids."

# Remove the downloaded file
rm NC_000913.faa.gz
