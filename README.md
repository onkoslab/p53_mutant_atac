# p53_mutant_atac
<h3>Differential chromatin accessibility landscape of gain-of-function mutant p53 tumours</h3>

<p>doi: https://doi.org/10.1101/2020.11.24.395913</p>

This repository contains code and data used for the analysis performed in the paper.
____________________________________________________

<h3> How to use </h3>

<p>The analysis can be performed using a combination of Jupyter notebooks (using Python and R). There are two ways you can go about it:
 <br> 1. Docker Image: Includes all the Notebooks, Pre-required data* and the libraries used.
 <br> 2. Alternatively you can download all the notbooks from this repositry along with the data.tar.gz, and run them with required packages.
 </p>

All notebooks are documented, so you can check which kind of data is needed to run them (and in which folder should it be) and what is the output that is generated.


____________________________________________________
<h3> 1. Using Docker </h3>
  <p align="justify" > This docker image contains all the required R and Python libraries, along with the code required for generating all result files and figures.</p>
   
   
```r
## to pull the docker image
docker pull bhavya2017/p53_mutant_atac:latest
```


```r
## to run the docker image
docker run --rm -p {port}:8888 -e JUPYTER_ENABLE_LAB=yes -v {path_to_your_working_directory}:/home/jovyan/work bhavya2017/p53_mutant_atac:latest
```
____________________________________________________


<h3> 2. Alternative Method </h3>
<p> Make the following directories in your current path, if you are not using docker to run the notebooks.

```diff
### Extract the data folder
mkdir Results
mkdir plots
mkdir profile
mkdir Results/p53retriever
mkdir profile/TF
mkdir profile/histone
```
<p> 
 <b>./data</b> contains all the input data for analysis of limma, jaspar, histone, homer denovo, nonBform elements, expression(RSEM), gene copy number, cancer driver genes
 <br><br>
<b>./plot</b> all the figures created using the above notebooks
<br><br>
<b>./profile</b> Files to create profile plots using Deepmap tools (plot heatmap & plot profile)
 <br><br>
<b>./Results</b> files from limma, HOMER input, upset, tcgabiolinks </p>

#### Notebook Details

<p>Run the notebooks in the given order as they are interdependant</p>
<p>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/1_Pre-processing.ipynb">1_Pre-processing:</a></b> Python notebook, to create input files for limma Differential Acc analysis. Raw data required can either be downloaded from gdc or taken from ./data ({BRCA/COAD}_rawcounts.tsv)
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/2_Differential_ACC.ipynb">2_Differential_ACC:</a></b> R notebook, to perform Differential Acc: requires condition and raw counts file
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/3_Differential_exp.ipynb">3_Differential_exp:</a></b> R notebook, for samples from the above analysis which have expression data are given for differential exp analysis through tcgabiolinks
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/4_Segment_copy_number.ipynb">4_Segment_copy_number:</a></b> R notebook, to fetch the segment copy number score for samples from Acc. analysis.
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/5_p53RE.ipynb">5_p53RE:</a></b> R notebook, to find the response element of significant regions found in 2_Differential_ACC. Input requires fasta seq of the region
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/6_BRCA_analysis.ipynb">6_BRCA_analysis:</a></b> Python notebook, to explore and annotate significant region found in breast (Main figures)
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/7_COAD_analysis.ipynb">7_COAD_analysis:</a></b> Python notebook, to explore and annotate significant region found in colon (Main figures)
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/8_Upset_plot.ipynb">8_Upset_plot:</a></b> R notebook, to plot Figure1 E&F for breast and colon
</p>

#### <br/>*Required data

<p align="justify" >To obtain results for Enhancer interactions in the siginificant peaks, Genehancer dataset is required. The dataset can be obtained through the following</p>


<p> 1. Go to the the UCSC Table browser: https://genome.ucsc.edu/cgi-bin/hgTables <br> 2. Upload the significant peaks in bed format <br> 3.Select the following:<b>track</b>: Genehancer Regulatory Interaction cluster view (double elite); <b>assembly</b>:hg38; <b>output</b>:BED.
<p <div class='a' </p>  


#### <br/>Required Packages

<b>Python 3.8.6</b>

```diff
jupyter-client                6.1.7
jupyterlab                    2.2.8
matplotlib                    3.3.2
numpy                         1.19.2
scikit-image                  0.17.2
scikit-learn                  0.23.2
PyYAML                        5.3.1
scipy                         1.5.2
seaborn                       0.11.0
pandas                        1.1.3
statsmodels                   0.12.0
pybedtools                    0.8.1
```

<b>R version 3.6.3</b>

```diff
BiocManager                   1.30.10
edgeR                         3.28.1
TCGAbiolinks                  2.14.1
p53retriever                  1.2.0
UpSetR                        1.4.0
dbplyr                        1.4.4
SummarizedExperiment          1.16.1
```
