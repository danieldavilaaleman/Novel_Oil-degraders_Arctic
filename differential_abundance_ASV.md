# Differential abundance analysis 
1. Create a singularity container of bioconductor
```
singularity pull docker://bioconductor/bioconductor_docker
```
2. Start a shell inside the container
```
singularity shell bioconductor_docker_latest.sif
```
3. Set my library directory
```
mkdir ~/Singularity_containers/R_singularity/4.3.0
export R_LIBS_USER=$HOME/Singularity_containers/R_Singularity/4.3.0:$R_LIBS_USER
```
4. Start R shell
```
Apptainer> R
```
5. Install the first package by
```
install.packages('ggplot2', lib = '~/apps/R_Singularity/4.3.0')
```