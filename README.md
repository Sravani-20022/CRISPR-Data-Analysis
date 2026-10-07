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
Reference file used in the analysis: genome.fa
**Workflow**
Raw FASTQ files
       ↓
Quality Control using FastQC
       ↓
Read Trimming and Filtering using fastp
       ↓
Quality Control after trimming
       ↓
Reference Genome Preparation
       ↓
BWA Reference Indexing
       ↓
Read Alignment using BWA
       ↓
BAM Sorting using SAMtools
       ↓
Duplicate Removal
       ↓
Read Group Assignment using Picard
       ↓
Reference Indexing
       ↓
Variant Calling using GATK HaplotypeCaller
       ↓
VCF File
       ↓
Variant Annotation using VEP
**Tools Used**
| Tool | Purpose |
|------|---------|
| FastQC | Quality control of sequencing reads |
| fastp | Read trimming and quality filtering |
| BWA | Alignment of reads to the reference genome |
| SAMtools | BAM/SAM processing and sorting |
| Picard | Read-group assignment and BAM preparation |
| GATK | Variant calling |
| VEP | Variant annotation |

**Analysis Steps**
**1. Data Downloading**
The paired-end sequencing data was downloaded from the NCBI SRA/ENA database using the SRA accession SRR21763320.
**2. Quality Control – FastQC**
Initial quality control was performed using FastQC to check:
- Per-base sequence quality
- Adapter content
- Overrepresented sequences
**3. Read Trimming – fastp**
Low-quality bases and adapter sequences were removed using fastp. The reads were filtered using a quality threshold of Q30.
**4. Quality Control After Trimming**
FastQC was performed again on the trimmed reads to confirm improvement in sequence quality.
**5. Reference Genome Preparation**
The human chromosome 17 reference genome was downloaded from UCSC and prepared for alignment. Chromosome 17 was selected because the BRCA1 gene is located on chromosome 17. CRISPR
**6. Read Alignment – BWA**
The trimmed paired-end reads were aligned to the reference genome using BWA-MEM. CRISPR
**7. SAM/BAM Processing – SAMtools**
The aligned reads were converted/processed as BAM files and sorted using SAMtools. Duplicate reads were also removed as part of the processing workflow. CRISPR
**8. Read Group Assignment – Picard**
Picard AddOrReplaceReadGroups was used to add the required read-group information to the processed BAM file.
**9. Reference Indexing**
The reference genome was indexed using samtools faidx, and a sequence dictionary was generated using Picard. CRISPR
**10. Variant Calling – GATK**
GATK HaplotypeCaller was used to identify potential SNPs and indels from the processed BAM file. HaplotypeCaller performs local haplotype reassembly in regions showing evidence of variation. GATK
**11. VCF Generation**
The identified variants were stored in a VCF (Variant Call Format) file containing information such as chromosome, position, reference allele, alternate allele and variant quality.
**12. Variant Annotation – VEP**
The GATK-generated VCF file was used for Variant Effect Predictor (VEP) annotation to determine the potential effects of identified variants.
**Results**
**1. Quality Control Results**
The sequencing data was evaluated before and after trimming using FastQC and fastp.
| Parameter | Before Filtering | After Filtering |
|---|---:|---:|
| Total reads | 1,716,674 | 935,944 |
| Total bases | 516,718,874 | 265,203,178 |
| Mean read length | 301 bp | 283 bp |
| Q20 | 68.33% | 100% |
| Q30 | 68.33% | 100% |
| GC content | 46.85% | 48.46% |
**Filtering summary:**
- 935,944 reads (54.52%) passed the filtering step.
- 780,284 reads were removed because of low quality.
- 824,130 reads had adapter trimming.
- The mean read length decreased from 301 bp to 283 bp after trimming.
**2. Variant Calling Results**
Variant calling was performed using GATK HaplotypeCaller.
The output was generated as: GATK_output.vcf
The VCF contains variants identified on chromosome 17, including chromosome position, reference allele, alternate allele, quality score and other variant information. GATK_output
**3. Variant Annotation**
The resulting VCF file can be used with VEP (Variant Effect Predictor) to determine the predicted effects of the identified variants on genes and transcripts.
## Project Files
- `crispr_analysis.sh` – CRISPR/Cas9 analysis pipeline
- `adapter.fasta.txt` – Adapter sequences used for trimming
- `fastp.html` – Fastp quality control report
- `fastp.json` – Fastp quality control results
- `genome.fa` – Human chromosome 17 reference genome
- `GATK_output.vcf` – GATK variant calling output
- `VEP_output.txt` – VEP variant annotation results
## VEP Results
Variant annotation was performed using the Ensembl Variant Effect Predictor (VEP).
The VEP analysis processed 53 variants, with no variants filtered out. Among these, 38 variants (71.7%) were novel and 15 variants (28.3%) were previously known. The variants overlapped 9 genes and 399 transcripts, with no overlapping regulatory features.
The major predicted consequences were frameshift variants (43%), stop-gained variants (32%), inframe insertions (11%), and protein-altering variants (11%).
A notable result was identified at chromosome 17 position 43074471 in the BRCA1 gene. VEP annotated this variant as a frameshift variant with HIGH impact across multiple protein-coding BRCA1 transcripts.
## Conclusion
This project demonstrated a complete CRISPR/Cas9 sequencing data analysis workflow, starting from raw sequencing data and progressing through quality control, read trimming, reference genome alignment, BAM processing, variant calling, and variant annotation.
The analysis produced a quality-filtered dataset and identified variants on human chromosome 17. VEP annotation identified variants with different predicted consequences, including frameshift, stop-gained, inframe insertion, and protein-altering variants.
A notable high-impact frameshift variant was identified in the BRCA1 gene at chromosome 17 position 43074471.
Overall, this project provided practical experience in NGS data analysis, variant calling, and functional variant annotation using command-line bioinformatics tools.
