# Differential abundance analysis 
https://docs.rc.fas.harvard.edu/kb/r-packages-with-singularity/
1. Create a singularity container of bioconductor
```
singularity pull docker://
```
2. Start a shell inside the container
```
singularity shell 
```
3. Set my library directory
```
mkdir -p $HOME/apps/R_Singularity/4.1.3
export R_LIBS_USER=$HOME/apps/R_Singularity/4.1.3:$R_LIBS_USER
```
4. Start R shell
```
Apptainer> R
```
5. Install the first package by
```
install.packages('ggplot2')
```
6. To install Phyloseq and microbiomeMarker
```
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("phyloseq")
BiocManager::install("microbiomeMarker")
```
