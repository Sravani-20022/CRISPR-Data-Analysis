# CRISPR-Data-Analysis
## Overview
This project demonstrates a bioinformatics workflow for the analysis of CRISPR/Cas9 sequencing data. The workflow starts with raw paired-end sequencing reads and proceeds through quality control, read trimming, reference genome preparation, read alignment, BAM file processing, variant calling, and functional variant annotation.
The analysis uses commonly used next-generation sequencing (NGS) tools including FastQC, fastp, BWA, SAMtools, Picard, GATK HaplotypeCaller, and Ensembl Variant Effect Predictor (VEP).
The final output is a set of called variants in VCF format followed by functional annotation using VEP.
## Introduction
CRISPR stands for **Clustered Regularly Interspaced Short Palindromic Repeats**. The CRISPR-Cas9 system is a genome-editing technology in which a guide RNA (gRNA) directs the Cas9 enzyme to a specific DNA sequence. Cas9 acts as a molecular nuclease and introduces a double-stranded DNA break at the target location.
Sequencing data generated from genome-editing or CRISPR-related experiments can be analyzed using bioinformatics workflows to identify sequence variations and determine their possible functional consequences.
In this project, sequencing reads were processed using a step-by-step NGS analysis workflow. Quality control and trimming were performed before aligning the reads to the human reference genome. The resulting alignment files were processed and used for variant calling with GATK HaplotypeCaller. The resulting VCF file was subsequently annotated using the Ensembl Variant Effect Predictor (VEP).
## Objectives
The main objectives of this project are:
- To download and process sequencing data.
- To perform quality control of raw sequencing reads.
- To remove low-quality sequences and adapter sequences.
- To align processed reads to a reference genome.
- To process and sort alignment files.
- To remove duplicate reads.
- To prepare alignment files for GATK analysis.
- To identify variants using GATK HaplotypeCaller.
- To generate a VCF file containing identified variants.
- To annotate variants using Ensembl VEP.
- To investigate the predicted functional consequences of identified variants.
## Dataset
### Sequencing Data
- Sample: `SRR21763320`
- Sequencing type: Paired-end
- Read files:
  - `SRR21763320_1.fastq.gz`
  - `SRR21763320_2.fastq.gz`
The sequencing data were obtained from the NCBI SRA/ENA resources.
### Reference Genome
The analysis used the human reference genome corresponding to chromosome 17.
The reference chromosome was selected because the BRCA1 gene is located on chromosome 17.
Reference file used in the analysis:
```text
genome.fa

**Work flow**
Raw FASTQ Reads
       |
       v
Quality Control
     FastQC
       |
       v
Read Trimming
      fastp
       |
       v
Post-trimming Quality Control
     FastQC
       |
       v
Reference Genome
     hg38/chr17
       |
       v
Reference Indexing
       BWA
       |
       v
Read Alignment
       BWA
       |
       v
BAM Sorting
     SAMtools
       |
       v
Duplicate Removal
     SAMtools
       |
       v
Read Group Assignment
      Picard
       |
       v
Variant Calling
GATK HaplotypeCaller
       |
       v
      VCF
       |
       v
Variant Annotation
       VEP
       |
       v
Functional Consequences
