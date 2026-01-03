# PBMC-scRNA-seq-Analysis-Pipeline

## Project Overview

This project performs comprehensive single-cell RNA-seq (scRNA-seq) analysis of human peripheral blood mononuclear cells (PBMCs) across multiple disease states (healthy, exposed, hospitalized, infected). The pipeline integrates quality control, normalization, batch correction, clustering, cell-type annotation, differential expression, and visualization.

The workflow is implemented in **R** using **Seurat**, **SingleCellExperiment**, **SingleR**, **celldex**, **DecontX**, **Harmony**, and other specialized scRNA-seq packages.

---

## Analysis Workflow

### 1. Data Import & Sample Processing

* Load raw 10x Genomics matrices for each sample.
* Detect real cells using **barcodeRanks** and **emptyDrops**.
* Correct for ambient RNA contamination using **DecontX**.
* Create Seurat objects and merge all samples.

### 2. Quality Control (QC)

* Calculate **nFeature_RNA**, **nCount_RNA**, and **percent.mt** (mitochondrial content).
* Visualize QC metrics with violin and box plots.
* Filter low-quality cells (e.g., `nFeature_RNA < 200 | nFeature_RNA > 2500 | percent.mt > 5%`).

### 3. Normalization & Feature Selection

* Log-normalization.
* Identification of highly variable features.
* Scaling, PCA, and dimensionality reduction.

### 4. Batch Correction & Integration

* LogNormalization and **Harmony** for batch correction.
* UMAP visualization and clustering.

### 5. Cell Cycle Scoring

* Calculate **S- and G2M-phase scores** using canonical gene lists.
* Assign cell cycle phase to each cell.

### 6. Doublet Detection

* Detect doublets per patient using **scDblFinder**.
* Generate UMAP highlighting doublets.
* Subset singlets for downstream analysis.

### 7. Differential Expression (DE)

* Identify **cluster-specific markers** with `FindAllMarkers`.
* Perform **disease-state DE** (e.g., hospitalized vs healthy).
* Visualize DE results with **volcano plots**, **heatmaps**, and **DotPlots**.

### 8. Cell-Type Annotation

* Annotate clusters with **SingleR** using **MonacoImmuneData** reference.
* Validate annotations with canonical immune markers.
* Subset specific cell types (e.g., T cells, monocytes) for focused analysis.

### 9. Visualization

* UMAP plots colored by sample, disease state, cell type, sex.
* Feature plots for key genes.
* Heatmaps of top markers per cluster or per cell type.

---

## Requirements

* **R ≥ 4.2**
* **Packages**:

  * `Seurat`, `SeuratDisk`, `SeuratObject`, `SingleCellExperiment`, `celldex`, `SingleR`
  * `DropletUtils`, `scran`, `scDblFinder`, `DoubletFinder`, `DecontX`, `celda`
  * `ggplot2`, `patchwork`, `pheatmap`, `EnhancedVolcano`, `tidyverse`, `dplyr`, `readxl`
  * `glmGamPoi`, `harmony`, `future`
