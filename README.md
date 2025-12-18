# Expression pattern analysis of understudied genes— Seurat workflow

This repository contains an R Markdown workflow (`ExpressionPattern.Rmd`) that:
- loads a large 10x Genomics `.mtx` RNA count matrix (blood),
- randomly samples 5,000 cells to stay within memory limits,
- builds a Seurat object for blood (sampled) and for a testis UMI table,
- runs standard preprocessing (normalization, variable features, scaling, PCA, UMAP),
- visualizes expression of a defined candidate gene list in each dataset,
- integrates blood + testis using Seurat anchors and plots candidate genes on the integrated UMAP.

## Data sources

### Testis scRNA-seq
- Source: NCBI Gene Expression Omnibus (GEO), Series **GSE112013** (“The Human Testis Cell Atlas via Single-cell RNA-seq”).
- In this repo, the testis input corresponds to the processed UMI count table used in the workflow: `GSE112013_Combined_UMI_table.txt`. 
- Associated publication: Guo J. et al. **“The adult human testis transcriptional cell atlas.”** (PMID: 30315278). 

### Blood scRNA-seq
- The blood input is provided as 10x Genomics / Cell Ranger–style matrix files:
  `10x_v2_RNA_matrix.mtx`, `10x_v2_RNA_features.tsv`, `10x_v2_barcodes.tsv`.

## Candidate genes
Defined in the Rmd as:
- C1orf174
- LOC124903857
- TMEM161B
- ZNF808
- C16orf54
- CNFN
- C8orf88
- PQLC2L

## Requirements
- R
- R packages:
  - Seurat
  - patchwork
  - dplyr
  - data.table
  - Matrix

## Input files (expected by the Rmd)
Blood (10x-style files):
- `10x_v2_RNA_matrix.mtx`
- `10x_v2_RNA_features.tsv`
- `10x_v2_barcodes.tsv`

Testis:
- `GSE112013_Combined_UMI_table.txt`

## Intermediate file created by the workflow
The workflow creates a filtered matrix file during sampling:
- `10x_v2_RNA_matrix_filtered.mtx`

## What the workflow produces
Outputs are generated as plots inside the rendered R Markdown document:
- UMAP + FeaturePlot panels for candidate genes in blood
- UMAP + FeaturePlot panels for candidate genes in testis
- Integrated UMAP (blood + testis) with FeaturePlot panels for the candidate genes

No plot/image files are written to disk by the current Rmd.

## How to run
Option 1 (RStudio):
1. Open `ExpressionPattern.Rmd`
2. Ensure the input files are present in the working directory (or update paths in the Rmd)
3. Click **Knit** (HTML or PDF)

Option 2 (R console):
```r
rmarkdown::render("ExpressionPattern.Rmd")
