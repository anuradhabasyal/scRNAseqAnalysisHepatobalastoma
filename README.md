# Single-cell RNA-seq Analysis of Hepatoblastoma and PDX Samples

This repository contains the code and analysis for my final project on single-cell RNA sequencing (scRNA-seq) of hepatoblastoma, patient-derived xenograft (PDX), and background liver samples. The project covers all steps from quality control and filtering to normalization, dimensionality reduction, batch correction, clustering, marker gene discovery, cell type annotation, pseudotime trajectory inference, and cell composition analysis.

---


Anuradha Basyal  
Boston University  
Final Project for BF591, Spring 2025

---

## Project Overview

This project analyzes scRNA-seq data from seven samples: HB17_background, HB17_PDX, HB17_tumor, HB30_PDX, HB30_tumor, HB53_background, and HB53_tumor. The main goals are to:

- Identify and filter high-quality single cells
- Normalize and integrate data across samples
- Correct batch effects (Harmony)
- Cluster cells and visualize with UMAP/t-SNE
- Identify marker genes for each cluster
- Annotate cell types (SingleR and manual curation)
- Infer developmental trajectories (Slingshot pseudotime)
- Compare cell type compositions between tumor, PDX, and background

---

## Installation & Dependencies

All analyses are performed in **R (v4.4.0)**.  
Required packages (install using CRAN, Bioconductor, or GitHub as appropriate):

- `Seurat`, `ggplot2`, `dplyr`, `Matrix`, `future`, `patchwork`, `pheatmap`, `tibble`, `knitr`, `kableExtra`, `purrr`, `tidyverse`, `harmony`, `remotes`, `circlize`, `RColorBrewer`
- Bioconductor: `scDblFinder`, `SingleR`, `slingshot`, `DropletUtils`, `ComplexHeatmap`, `gplots`
- GitHub: `CellChat`


---

## Data Preprocessing

- Raw 10X Genomics matrices for each sample are loaded and converted to Seurat objects.
- Quality control performed using nFeature_RNA, nCount_RNA, and percent.mt.
- Filtering thresholds are sample-specific, based on data distributions and literature guidance.
- Doublets removed using scDblFinder.
- Summary tables report cell/gene counts before and after filtering.

---

## Normalization & Feature Selection

- All filtered objects merged into a single Seurat object.
- LogNormalize method used (scale factor 10,000).
- Highly variable genes selected (top 2,000 by "vst" method).

---

## Dimensionality Reduction & Clustering

- PCA performed on variable genes; first 10 PCs selected using elbow plot.
- Graph-based clustering (resolution = 0.2) identifies 21 initial clusters.
- UMAP and t-SNE visualizations colored by cluster and sample.

---

## Batch Correction & Integration

- Harmony used for batch correction across samples.
- Post-integration clustering yields 11 clusters.
- UMAPs show improved mixing of cells from different samples.

---

## Marker Gene Discovery & Cell Type Annotation

- Cluster-specific marker genes identified using Seurat’s `FindAllMarkers`.
- Top 5 markers per cluster visualized with heatmaps and violin plots.
- Automated annotation with SingleR (HumanPrimaryCellAtlas reference).
- Manual curation of cluster identities based on marker genes and literature.

---

## Pseudotime & Trajectory Analysis

- Slingshot used to infer developmental trajectories on UMAP embedding.
- Pseudotime ordering reveals differentiation paths among clusters.

---

## Cell Composition Analysis

- Cell proportions compared across tumor, PDX, and background samples.
- Bar plots and heatmaps visualize differences in cell type composition.
- Statistical tests (chi-square) assess enrichment differences.

---

## References

- Bondoc, A. D. et al. Cancer Res. 81, 1234–1247 (2021).
- Zhang, Q. et al. Cell 179(4), 829-845 (2019).
- Lee, S. H. et al. OncoImmunology 9, 1773746 (2020).
- Wang, M. et al. FASEB J. 32(3), 1537-1549 (2018).
- Kubes, P. & Jenne, C. Annu. Rev. Immunol. 36, 247-277 (2018).
- Wohlfahrt, T. et al. Nat. Commun. 13, 2365 (2022).
- Meraz, I. M. et al. Cancer Immunol. Res. 7(8), 1267-1279 (2019).
- Sharma, P. et al. Nat. Med. 27(10), 1848-1856 (2021).

---
