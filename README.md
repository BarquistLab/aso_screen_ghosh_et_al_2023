# RNA-seq analysis to Ghosh et al. 2023

- Project name: A side-by-side comparison of peptide-delivered antisense antibiotics employing different nucleotide mimics

- Experiments: Chandradhish Ghosh, Linda Popella, Dhamodharan Venugopalan

- Supervision: Lars Barquist, Claudia Höbartner, Jörg Vogel

- Data analysis: Jakob Jung

- Start: September 2022 

  

## Introduction

 This project directory contains the analysis of RNA-Seq results obtained after short term *Salmonella* SL1344 exposure to various ASO-chemistries.

## Directory structure

The project is divided in 3 main directories:

-   [data](data) : contains all raw, intermediate and final data of the project.  
-   [analysis](analysis): contains analysis files, such as figures, plots, tables, etc. 
-   [scripts](scripts): contains scripts to process and analyze data from the data directory.

Some directories have their own README.md file with information on the respective files. 



## Workflow

Here I describe the workflow, which can be followed to reproduce the RNA-Seq results & plots from the article. 



### 1. Prerequisites

For running the whole RNA-seq analysis, one needs following packages/tools/software:

For running the whole analysis, one needs following packages/tools/software:

- BBMap (v38.84) & BBDuk

- R (v.4.1.1) along with packages from Bioconductor/CRAN 

- Linux shell (we used Ubuntu 20.04) for commands & bash scripts

- featureCounts (v2.0.1) from Subread package

- bedtools (v2.26.0) 

- samtools (v1.12)



 

### 2. Mapping

All raw FastQ files are located in the folder [./data/fastq](data/fastq) and were deposited to the GEO repository under accession number: GSE232819. Details on samples and setup of the experiment can be found in the methods section of the manuscript. Navigate to [data/libs](./data/libs) to find fastQC quality statistics in HTML format of the trimmed reads. 

 To run the mapping, run the bash script [./scripts/trimm_map_BB.sh](./scripts/trimm_map_BB.sh) . The script loops through the fastq-files, trims off adapters using BBDuk, maps against the reference genome (reference fasta and gff files can be found in [./data/reference_sequences/](./data/reference_sequences/)) and counts the reads mapped to coding sequences and sRNAs using featureCounts.

Trimming, mapping and counting statistics are stored in the log file [./scripts/my.stdout](./scripts/my.stdout) . The directory [./data/rna_align](./data/rna_align) includes all bam-alignment files as well as the count table [./data/rna_align/counttable.txt](./data/rna_align/counttable.txt) . This count table was imported into R for Differential expression analysis.



### 3. Differential expression analysis

To run the differential expression analysis, run the R markdown script [./scripts/aso_screen_RNASeq.Rmd](./scripts/aso_screen_RNASeq.Rmd) . This outputs all figures of the manuscript, which are saved as PDF and/or SVG files to the [./analysis](./analysis) directory. It might take up to 3 minutes to run this script on a low-memory laptop. Some packages have to be pre-installed, such as edgeR, complexHeatmap, etc.

