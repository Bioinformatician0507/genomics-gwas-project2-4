# genomics-gwas-project2-4
# Project 2 — Variant Calling Pipeline

## Overview
End-to-end variant calling pipeline using samtools and bcftools on 
synthetic sequencing data.

## Tools
- samtools v1.x
- bcftools v1.13
- Python (matplotlib)

## Pipeline Steps
1. Generated synthetic reference genome (1000bp, chr1)
2. Simulated 800 paired-end reads with 10 planted SNPs at known positions
3. Converted SAM → sorted BAM → indexed
4. Ran bcftools mpileup for read pileup at each position
5. Called variants with bcftools call (multiallelic model)
6. Filtered variants: QUAL≥20, FORMAT/DP≥5
7. Visualized quality scores, variant types, and genomic positions

## Results
- 10/10 planted SNPs recovered (100% sensitivity)
- All variants PASS quality filters
- Mean QUAL = 149.4 (well above threshold)
- Mean read depth = 41.2x
- SNP/INDEL ratio = 10:0 (SNP-only synthetic dataset)

# Project 3 — Population Stratification & PCA

## Overview
Principal Component Analysis (PCA) to detect and visualize population 
structure in genomic data — a standard step in every GWAS pipeline.

## Tools
- PLINK2 (--pca flag)
- Python (pandas, matplotlib)

## Pipeline Steps
1. Ran --pca 10 on QC-passed dataset (500 samples, 48,039 SNPs)
2. Extracted top 10 eigenvectors and eigenvalues
3. Plotted PC1 vs PC2 colored by case/control status
4. Generated scree plot showing variance explained per PC

## Results
- PC1 explains 10.18% of variance
- PC2 explains 10.12% of variance
- All 10 PCs explain roughly equal variance (~10% each)
- Cases and controls overlap completely in PC space
- No population stratification detected (expected for synthetic null data)

## Key concepts demonstrated
- GRM (Genomic Relationship Matrix) construction
- Eigenvector decomposition for population structure
- Why flat scree plots indicate no stratification
- PCs as covariates to correct for stratification in GWAS

## Key concepts demonstrated
- SAM/BAM format handling
- mpileup-based variant calling
- QUAL and DP filtering thresholds
- VCF format parsing and visualization

# Project 4 — Polygenic Risk Score (PRS)

## Overview
Computed polygenic risk scores from GWAS summary statistics and 
demonstrated the impact of data leakage on PRS evaluation — a 
critical methodological consideration in genomic prediction.

## Tools
- PLINK2 (--score)
- Python (pandas, sklearn, matplotlib)

## Pipeline Steps
1. Used GWAS summary statistics (log-OR effect sizes) as PRS weights
2. Computed individual-level PRS with PLINK2 --score across 48,038 SNPs
3. Demonstrated data leakage: scored same dataset used for GWAS discovery
4. Corrected methodology: 70/30 train/test split (350 discovery, 150 target)
5. Compared AUC between leakage and proper independent evaluation

## Results
- AUC with data leakage (same dataset): 0.913
- AUC with independent target cohort: 0.869
- Leakage inflation: +0.044 AUC units
- Effect size distribution: mean β = 0.0008 (near-null, expected)

## Key finding
Data leakage in PRS evaluation artificially inflates predictive 
performance. Discovery and target cohorts must always be independent. 
This is a common methodological pitfall in genomic prediction studies.

## Run it yourself

## Run it yourself

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1NLbwYfiDb3fhgKETGzeIeD7tlrdCrwUd#scrollTo=pOy1ewSfH8up)



## Key concepts demonstrated
- Effect size weighting for polygenic scoring
- ROC curve and AUC interpretation
- Data leakage detection and correction
- Discovery vs target cohort separation
