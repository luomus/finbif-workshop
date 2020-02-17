---
title: Working with taxa
draft: no
toc: yes
type: docs
weight: 5
menu:
  finbif:
    name: 4. Taxa
    weight: 5
---



The `{finbif}` package has two functions for querying the taxonomic information
in the FinBIF database.

## Checking taxa
You can use the function `finbif_check_taxa` to check whether taxa are in
the FinBIF database.

```r
(taxa <- finbif_check_taxa(c("Ursus arctos", "Moomin")))
```

```
#> [Ursus arctos] ID: MX.47348
#> [Moomin      ] Not found
```

If the taxa are present then the function returns their FinBIF ID, otherwise it
will return `NA`

```r
taxa[[1]]
```

```
#> Ursus arctos 
#>   "MX.47348"
```

```r
taxa[[2]]
```

```
#> Moomin 
#>     NA
```

When checking taxa, you can specify a taxonomic rank and only names with that
rank will have valid IDs returned.

```r
finbif_check_taxa(list(species = c("Ursus arctos", "Ursus"), genus = "Ursus"))
```

```
#> [species: Ursus arctos] ID: MX.47348
#> [species: Ursus       ] Not found
#> [genus:   Ursus       ] ID: MX.51311
```

You can check a number of taxa at a time. For example if you have a list of taxa
in a file (you can dowload this list of [taxa](../taxa.csv) for instance) you
can easily check them all at once.


```r
taxa_list <- readLines("taxa.csv")
finbif_check_taxa(taxa_list)
```

```
#> [Bombina variegata     ] ID: MX.200974
#> [Bufo bufo             ] ID: MX.37626
#> [Rana arvalis          ] ID: MX.37621
#> [Rana temporaria       ] ID: MX.37623
#> [Pelophylax esculentus ] ID: MX.201015
#> [Pelophylax lessonae   ] ID: MX.201018
#> [Pelophylax ridibundus ] ID: MX.37622
#> [Triturus cristatus    ] ID: MX.37628
#> [Ichthyosaura alpestris] ID: MX.200927
#> [Lissotriton vulgaris  ] ID: MX.37630
#> [Coronella austriaca   ] ID: MX.37637
#> [Natrix natrix         ] ID: MX.37639
#> [Vipera berus          ] ID: MX.37641
#> [Anguis fragilis       ] ID: MX.37632
#> [Lacerta agilis        ] ID: MX.201133
#> [Zootoca vivipara      ] ID: MX.37635
```
## Taxa search


```r
finbif_taxa("Capreolus capreolus")
```

```
#> <FinBIF taxa/search>
#> List of 1
#>  $ :List of 12
#>   ..$ matchingName            : chr "Capreolus capreolus"
#>   ..$ nameType                : chr "MX.scientificName"
#>   ..$ id                      : chr "MX.47507"
#>   ..$ scientificName          : chr "Capreolus capreolus"
#>   ..$ scientificNameAuthorship: chr "(Linnaeus, 1758)"
#>   ..$ taxonRank               : chr "MX.species"
#>   ..$ cursiveName             : logi TRUE
#>   ..$ finnish                 : logi TRUE
#>   ..$ species                 : logi TRUE
#>   ..$ vernacularName          :List of 3
#>   .. ..$ fi: chr "metsäkauris"
#>   .. ..$ en: chr "Roe Deer"
#>   .. ..$ sv: chr "rådjur"
#>   ..$ informalGroups          :List of 1
#>   .. ..$ :List of 2
#>   .. .. ..$ id  : chr "MVL.2"
#>   .. .. ..$ name:List of 3
#>   .. .. .. ..$ sv: chr "Däggdjur"
#>   .. .. .. ..$ fi: chr "Nisäkkäät"
#>   .. .. .. ..$ en: chr "Mammals"
#>   ..$ type                    : chr "exactMatches"
```


```r
deer <- finbif_taxa("deer", type = "partial", n = 10)
sapply(deer$content, getElement, "scientificName")
```

```
#>  [1] "Dama dama"                "Capreolus capreolus"     
#>  [3] "Odocoileus virginianus"   "Rangifer tarandus"       
#>  [5] "Hippuriphila modeeri"     "Pseudombrophila merdaria"
#>  [7] "Odocoileus"               "Cervidae"                
#>  [9] "Dama"                     "Capreolus"
```