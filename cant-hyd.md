# Analysis of Lacinutrix and candidate bacterial genomes using CANT-HYD
I created a conda env for hmmer3
```
conda activate hmmer3
hmmsearch --tblout hmmsearch_metagenome.tblout CANT-HYD.hmm representative_genomes/pseudothioglobus.faa > pseudothioglobus.out

#If I want to go for Evalues. The recomendation (Srijak) e-50
hmmsearch --tblout test.tsv -E 10e-50 CANT-HYD.hmm representative_genomes/psychromonas_ingrahamii.faa
