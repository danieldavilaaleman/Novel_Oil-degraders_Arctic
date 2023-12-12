I used this Rscript for the identification of ASV with differential abundance in each nutrient condition.
The logic behind the way I ran the analysis was:
1. Create a nutrient data frame with ONR7a, PSW or RSS phyloseq object for individual analysis
2. I copy the ONR7a, PSW or RSS phyloseq object to absolute and transform the number of read to RA and the multiply that by the average number of cells in each replicate
3. I added a column named "Species" in the absolute Phyloseq object where I add the ASV number
4. I remove the low prevalence ASV (ASVs only present in less than 10% of all the bottles) before running DA analysis
```
#Remove low prevalence ASV in the whole subset (this low prevalence ASVs represents unique ASV present in only one replicate)

prevdf = apply(X = otu_table(absolute),
               MARGIN = ifelse(taxa_are_rows(absolute), yes = 1, no = 2),
               FUN = function(x){sum(x > 0)})

prevdf = data.frame(Prevalence = prevdf,
                    TotalAbundance = taxa_sums(absolute),
                    tax_table(absolute))
#Defining prevalence threshold and filter ASVs before differential abundance analysis
prevalenceThreshold = 0.1 * nsamples(absolute)
keepTaxa = rownames(prevdf)[(prevdf$Prevalence >= prevalenceThreshold)]
absolute = prune_taxa(keepTaxa, absolute)

```
I ran the DA analysis
