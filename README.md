# Acute Myeloid Leukemia Heatmap Analysis

The overall goal of this analysis is to examine gene expression patterns in Acute Myeloid Leukemia (AML) mouse models. By filtering for the most variable genes and performing hierarchical clustering, we aim to visualize how samples group according to their specific mutations (`IDH2`, `TET2`) and treatments.

*This example analysis will:*

* Download pre-processed RNA-seq data from [refine.bio](https://www.refine.bio/).
* Filter the dataset to retain only the genes with the highest variance across samples.
* Perform hierarchical clustering on both genes and samples.
* Generate an annotated heatmap to visualize expression differences relative to metadata (mutation and treatment).

## Requirements

To run this analysis, you will need **R** and **Python** installed.

You will need the following R libraries:

* `pheatmap`
* `magrittr`
* `readr`
* `dplyr`
* `tibble`
* `rmarkdown` (to render the notebook)

You will also need the `refinebio-py` package to run the download script:

```bash
pip install refinebio-py

```

## How to run the analysis/Usage

To re-run this analysis, here are the exact commands you need to run in your terminal, ensuring the top of this repository is your current working directory.

1. **Download the data**
This script will download the SRP070849 dataset from refine.bio into a `data/` directory.

```bash
python3 00-download-data.py

```

2. **Run the analysis notebook**
This command renders the R Markdown notebook, running all code blocks to process the data and generate plots.

```bash
Rscript -e "rmarkdown::render('make_heatmap.Rmd')"

```

## About the scripts

* `00-download-data.py` - This Python script utilizes the refine.bio API to download the specific AML dataset (SRP070849) required for the analysis. It ensures the data is downloaded, unzipped, and ready in the `data/` folder.
* `make_heatmap.Rmd` - This Rmd notebook takes the data that is downloaded from refine.bio, filters for high-variance genes, and creates a heatmap that is saved to `plots/aml_heatmap.png`.

### Input

The data used by this analysis is [SRP070849](https://www.refine.bio/experiments/SRP070849), which is downloaded [processed and quantile normalized](http://docs.refine.bio/en/latest/main_text.html#refine-bio-processed-refinebio-processedibadge) from refine.bio using the python script included in this repo.

It contains RNA-seq data from 19 mice with Acute Myeloid Leukemia (AML) under controlled treatment conditions.

### Output

Two directories are created by this analysis to hold the output:

`plots/` - contains the heatmap image:

* `aml_heatmap.png`: A hierarchically clustered heatmap showing the expression of the most variable genes.
* **Interpretation:** Yellow indicates high expression (up-regulation), blue indicates low expression (down-regulation), and black represents average expression. The side bars indicate the mutation status and treatment type for each sample.


`results/` - contains the data file:

* `top_75_var_genes.tsv`: A TSV file containing the subset of the gene expression matrix used to generate the heatmap (genes in the upper 75th percentile of variance).

### Additional info

This analysis is adapted from the [refine.bio-examples](https://alexslemonade.github.io/refinebio-examples/) repository.
