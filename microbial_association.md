# Microbial Association analysis 
I followed some steps from https://f1000research.com/articles/5-1492/v2
1. Create a table for each Phylum present in the dataset

```
# Create table, number of features for each phyla
table(tax_table(ps)[, "Phylum"], exclude = NULL)
```

2. This shows phyla with the number of features observed. Features (ASVs) annotated with a Phylum of NA are probably artifacts in a dataset and should be removed.

```
ps0_ONR7a <- subset_taxa(ps_raw_micro_CRD_ONR7a, !is.na(Phylum))
```

3. Next step is to explore prevalence (the number of samples in which a taxa appears at least once)

```
# Compute prevalence of each feature, store as data.frame
prevdf = apply(X = otu_table(ps0_ONR7a),
                 MARGIN = ifelse(taxa_are_rows(ps0_ONR7a), yes = 1, no = 2),
                 FUN = function(x){sum(x > 0)})
# Add taxonomy and total read counts to this data.frame
prevdf = data.frame(Prevalence = prevdf,
                      TotalAbundance = taxa_sums(ps0_ONR7a),
                      tax_table(ps0_ONR7a))
```
4. Compute total prevalences of the features in each phylum
```
plyr::ddply(prevdf, "Phylum", function(df1){cbind(mean(df1$Prevalence),sum(df1$Prevalence))})
```
