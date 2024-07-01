To get the stats from the Figure1
```
compare_means(value ~ Time, cells, group_by=c("Media","Condition"))
```
Figure4
```
write.csv(compare_means(genome_size.mean ~ Time, paprica, group.by = "Media"), "stats_fig4a.csv")
```
