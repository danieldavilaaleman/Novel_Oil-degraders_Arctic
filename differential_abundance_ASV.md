# Differential abundance analysis 
https://docs.rc.fas.harvard.edu/kb/r-packages-with-singularity/
1. Create a singularity container of bioconductor
```
singularity pull docker://bioconductor_docker_devel.sif
```
2. Start a shell inside the container
```
singularity shell bioconductor_docker_devel.sif
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

7. To run within a Singularity container with SLURM, I run `run_figure3_asv.sbatch`
```
#!/bin/bash
####### Reserve computing resources #############
#SBATCH --nodes=1
#SBATCH --ntasks=2
#SBATCH --cpus-per-task=10
#SBATCH --partition=cpu2022
#SBATCH --time=012:00:00
#SBATCH --mem=30gb

####### Set environment variables ###############

###### Run your script #########################
singularity exec ~/Singularity_containers/bioconductor_docker_devel.sif R CMD BATCH \
figure3_asv.R test.out

```
