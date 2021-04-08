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
<h3> Docker Image </h3>
  <p align="justify" > This docker image contains all the required R and Python libraries, along with the code required for generating all result files and figures.</p>
   
   
```r
## to pull the docker image
docker pull bhavya2017/p53_mutant_atac:latest
```


```r
## to run the docker image
docker run --rm -p {port}:8888 -e JUPYTER_ENABLE_LAB=yes -v {path_to_your_working_directory}:/home/jovyan/work bhavya2017/p53_mutant_atac:latest
```

### <br/> Directory Structure
<img src="https://github.com/onkoslab/p53_mutant_atac/blob/main/tre.png" alt="alt text" width="150" >
<br><br>
<p>Run the notebooks in the given order as they are interdependant</p>
<p>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/1_Pre-processing.ipynb">1_Pre-processing:</a></b> Python notebook, to create input files for limma Differential Acc analysis. Raw data required can either be downloaded from gdc or taken from ./data ({BRCA/COAD}_rawcounts.tsv)
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/2_Differential_ACC.ipynb">2_Differential_ACC:</a></b> R notebook, to perform Differential Acc: requires condition and raw counts file
<br><br>
<b><a href="https://github.com/onkoslab/p53_mutant_atac/blob/main/3_Differentiall_exp.ipynb">3_Differentiall_exp:</a></b> R notebook, for samples from the above analysis which have expression data are given for differential exp analysis through tcgabiolinks
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
<br><br>
 <b>./data</b> contains all the input data for analysis of limma, jaspar, histone, homer denovo, nonBform elements, expression(RSEM), gene copy number, cancer driver genes
 <br><br>
<b>./plot</b> all the figures created using the above notebooks
<br><br>
<b>./profile</b> Files to create profile plots using Deepmap tools (plot heatmap & plot profile)
 <br><br>
<b>./Results</b> files from limma, HOMER input, upset, tcgabiolinks

</p>


#### <br/>*Required data

<p align="justify" >To obtain results for Enhancer interactions in the siginificant peaks, Genehancer dataset is required. The dataset can be obtained through the following</p>


<p> 1. Go to the the UCSC Table browser: https://genome.ucsc.edu/cgi-bin/hgTables <br> 2. Upload the significant peaks in bed format <br> 3.Select the following:<b>track</b>: Genehancer Regulatory Interaction cluster view (double elite); <b>assembly</b>:hg38; <b>output</b>:BED.
<p <div class='a' </p>  
