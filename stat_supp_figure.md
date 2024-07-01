<img width="489" alt="image" src="https://github.com/danieldavilaaleman/16S_nutrient_addition/assets/116775663/43076688-d891-46c4-96cf-6ebecffac496">To get the stats from the Figure1
```
compare_means(value ~ Time, cells, group_by=c("Media","Condition"))
```
Figure4
```
write.csv(compare_means(genome_size.mean ~ Time, paprica, group.by = "Media"), "stats_fig4a.csv")
```
