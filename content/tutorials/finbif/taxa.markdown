---
linktitle: 4. Taxa
title: Working with taxa
draft: no
toc: yes
type: book
weight: 5
---



The `{finbif}` package has two functions for querying the taxonomic information
in the FinBIF database.

## Taxa checking
You can use the function `finbif_check_taxa` to check whether taxa are in the
FinBIF database.

```.language-r
taxa <- finbif_check_taxa(c("Ursus arctos", "Moomin"))
taxa
```

```{.language-r}
#> [Ursus arctos] ID: MX.47348
#> [Moomin      ] Not found
```

If the taxa are present then the function returns their FinBIF ID, otherwise it
will return `NA`

```.language-r
taxa[[1]]
```

```{.language-r}
#> Ursus arctos 
#>   "MX.47348"
```

```.language-r
taxa[[2]]
```

```{.language-r}
#> Moomin 
#>     NA
```

When checking taxa, you can specify a taxonomic rank and only names with that
rank will have IDs returned if the name and rank combination is valid.

```.language-r
finbif_check_taxa(list(species = c("Ursus arctos", "Ursus"), genus = "Ursus"))
```

```{.language-r}
#> [species: Ursus arctos] ID: MX.47348
#> [species: Ursus       ] Not found
#> [genus:   Ursus       ] ID: MX.51311
```

You can check many taxa at a time. For example, if you have a list of taxa in a
file (you can download this list of [taxa](../taxa.csv) for instance) you can
check them all at once.

```.language-r
taxa_list <- readLines("taxa.csv")
finbif_check_taxa(taxa_list)
```

```{.language-r}
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
### Exact matching
More detailed taxonomic information for taxa that are in the FinBIF database can
be accessed with the `finbif_taxa` function. By default, `finbif_taxa` will use
exact matching, only returning information on taxa that exactly match the query
that was made.

```.language-r
finbif_taxa("Capreolus capreolus")
```

```{.language-r}
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
#>   .. .. .. ..$ fi: chr "Nisäkkäät"
#>   .. .. .. ..$ en: chr "Mammals"
#>   .. .. .. ..$ sv: chr "Däggdjur"
#>   ..$ type                    : chr "exactMatches"
```

### Partial matching
Searching for taxonomic information in FinBIF can also use "partial" matching.
For example, you might be interested in taxa that match a particular term, such
as 'deer'.

```.language-r
deer <- finbif_taxa("deer", type = "partial", n = 10)
sapply(deer$content, getElement, "scientificName")
```

```{.language-r}
#>  [1] "Odocoileus virginianus"     "Capreolus capreolus"       
#>  [3] "Dama dama"                  "Cervus elaphus"            
#>  [5] "Rangifer tarandus"          "Hippuriphila modeeri"      
#>  [7] "Pseudombrophila merdaria"   "Rangifer tarandus fennicus"
#>  [9] "Rangifer tarandus tarandus" "Odocoileus"
```
