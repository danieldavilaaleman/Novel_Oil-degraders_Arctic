# Microbial Association analysis 
I followed some steps from https://f1000research.com/articles/5-1492/v2
1. Create a table of read counts for each Phylum present in the dataset
```
# Create table, number of features for each phyla
table(tax_table(ps)[, "Phylum"], exclude = NULL)
```
