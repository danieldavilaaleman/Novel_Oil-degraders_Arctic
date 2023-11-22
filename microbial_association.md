# Microbial Association analysis 
## Solving spieceasy problem of low number of samples
To remove taxa with lower number of read (e.g. <12 - two reads on average with sample saze of 6 bottles)
```
ps1_ONR7a <- prune_taxa(taxa_sums(ps0_ONR7a)>12, ps0_ONR7a)
```
However, I checked that lower number of samples generates a high number of false positives
https://github.com/zdk123/SpiecEasi/issues/30. Therefore, I need to filter also for high prevalence taxa

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
5. Subseting
```
prevdf1 = subset(prevdf, Phylum %in% get_taxa_unique(ps1, "Phylum"))
ggplot(prevdf1, aes(TotalAbundance, Prevalence / nsamples(ps0),color=Phylum)) +
  # Include a guess for parameter
  geom_hline(yintercept = 0.05, alpha = 0.5, linetype = 2) + geom_point(size = 2, alpha = 0.7) +
  scale_x_log10() +  xlab("Total Abundance") + ylab("Prevalence [Frac. Samples]") +
  facet_wrap(~Phylum) + theme(legend.position="none")
```
