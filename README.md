# p53_mutant_atac
<h3>Differential chromatin accessibility landscape of gain-of-function mutant p53 tumours</h3>
<h4>Introduction</h4>
 <p align="justify" >Mutations in TP53 not only affect its tumour suppressor activity but also exerts oncogenic gain-of-function activity. While the genome-wide mutant p53 binding sites have been identified in cancer cell lines, the chromatin accessibility landscape driven by mutant p53 in primary tumours is unknown. Here, we leveraged the chromatin accessibility data of primary tumours from TCGA to identify differentially accessible regions in mutant p53 tumours compared to wild p53 tumours, especially in breast and colon cancers.</p>

<br>
<img src="https://github.com/onkoslab/p53_mutant_atac/blob/main/figure_readme.png" alt="alt text" width="700" height="410">

____________________________________________________

<h3> Docker Image <h3>
  <p align="justify" > This docker image contains all the required R and Python libraries, along with the code required for generating all result files and figures.</p>
   
   
```r
## to pull the docker image
docker pull bhavya2017/p53_mutant_atac:latest
```


```r
## to run the docker image
docker run --rm -p {port}:8888 -e JUPYTER_ENABLE_LAB=yes -v {path_to_your_working_directory}:/home/jovyan/work bhavya2017/p53_mutant_atac:latest
```

#### <br/>Required data

<p align="justify" >To obtain results for Enhancer interactions in the siginificant peaks, Genehancer dataset is required. The dataset can be obtained through the following</p>


<p> 1. Go to the the UCSC Table browser: https://genome.ucsc.edu/cgi-bin/hgTables <br> 2. Upload the significant peaks in bed format <br> 3.Select the following:<b>track</b>: Genehancer Regulatory Interaction cluster view (double elite); <b>assembly</b>:hg38; <b>output</b>:BED.
<p <div class='a' </p>  

#### <br/> Files and directories
<img src="https://github.com/onkoslab/p53_mutant_atac/blob/main/tre.png" alt="alt text" width="150" >
<br>
<p>Run the notebooks in the given order as they are interdependant</p>
<p>
<b>1_Pre-processing:</b> Python notebook, to create input files for limma Differential Acc analysis. Raw data required can either be downloaded from gdc or taken from ./data ({BRCA/COAD}_rawcounts.tsv)
<br>
<b>2_Differential_ACC:</b> R notebook, to perform Differential Acc: requires condition and raw counts file
<br>
<b>3_Differentiall_exp:</b> R notebook, for samples from the above analysis which have expression data are given for differential exp analysis through tcgabiolinks
<br>
 <b>4_Segment_copy_number:</b> R notebook, to fetch the segment copy number score for samples from Acc. analysis.
<br>
 <b>5_p53RE:</b> R notebook, to find the response element of significant regions found in 2_Differential_ACC. Input requires fasta seq of the region
<br>
<b>6_BRCA_analysis:</b> Python notebook, to explore and annotate significant region found in breast (Main figures)
<br>
 <b>7_COAD_analysis:</b> Python notebook, to explore and annotate significant region found in colon (Main figures)
<br>
<b>8_Upset_plot:</b> R notebook, to plot Figure1 E&F for breast and colon
<br>
 <b>./data</b> contains all the input data for analysis of limma, jaspar, histone, homer denovo, nonBform elements, expression(RSEM), gene copy number, cancer driver genes
<br>
<b>./plot</b> all the figures created using the above notebooks
<br><b>./profile</b> Files to create profile plots using Deepmap tools (plot heatmap & plot profile)
 <br>
<b>./Results</b> files from limma, HOMER input, upset, tcgabiolinks

</p>

