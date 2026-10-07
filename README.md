# CRISPR-Data-Analysis

## Introduction

CRISPR/Cas9 is a genome-editing technology in which guide RNA (gRNA) directs the Cas9 enzyme to a specific DNA sequence. Sequencing data generated from CRISPR-related experiments can be analyzed using bioinformatics tools to identify genetic variations and study their potential effects.

This project demonstrates a complete workflow for analyzing paired-end sequencing data. The analysis begins with downloading sequencing data from the NCBI SRA/ENA databases, followed by quality control using FastQC and read trimming using fastp.

The processed reads are aligned to the human reference genome (hg38/chr17) using BWA. The resulting alignment files are processed using SAMtools, followed by read-group assignment and preparation for variant calling using Picard. Genetic variants are then identified using GATK HaplotypeCaller and stored in VCF format.

Finally, the identified variants are annotated using the Ensembl Variant Effect Predictor (VEP), with functional predictions such as SIFT and PolyPhen used to help assess the potential effects of variants.

The main objective of this project is to demonstrate a complete NGS/CRISPR data analysis workflow from raw sequencing reads to variant identification and functional annotation.
