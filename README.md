# Acute Myeloid Leukemia (AML) Heatmap Analysis

This repository contains an R Markdown analysis that performs hierarchical clustering on RNA-seq data from AML mouse models. It visualizes gene expression patterns associated with `IDH2` and `TET2` mutations and their respective treatments.

**Original Study:** [Shih et al. (2017)](https://pubmed.ncbi.nlm.nih.gov/28193779/)
**Data Source:** [refine.bio (SRP070849)](https://www.refine.bio/experiments/SRP070849)

## Workflow

1. **Ingest:** Loads pre-processed, quantile-normalized RNA-seq data.
2. **Filter:** Retains the upper quartile (top 25%) of genes based on variance.
3. **Annotate:** Labels samples based on mutation status (`IDH2`, `TET2`, `WT`) and treatment (e.g., AG-221, 5-Azacytidine).
4. **Visualize:** Generates a hierarchical clustering heatmap.

## Dependencies

This analysis requires **R** (>= 4.0 recommended) and the following packages:

```r
install.packages(c("dplyr", "pheatmap", "readr", "magrittr", "sessioninfo"))

```

## Setup & Usage

Ensure your data is located in `data/SRP070849/`.

To run the analysis:

1. Open the `.Rmd` file in RStudio.
2. Click **Knit** (or run `rmarkdown::render("make_heatmap.Rmd")`).

## Outputs

Upon successful execution, the script generates the following:

| File | Location | Description |
| --- | --- | --- |
| **Heatmap** | `plots/aml_heatmap.png` | Clustering heatmap of high-variance genes. |
| **Gene List** | `results/top_75_var_genes.tsv`* | TSV file containing the subset of genes used for the heatmap. |
| **Report** | `*.html` or `*.pdf` | The rendered analysis notebook. |
