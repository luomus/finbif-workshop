---
title: Working with taxa
draft: no
toc: yes
type: book
weight: 5
menu:
  finbif:
    name: 4. Taxa
    weight: 5
---



The `{finbif}` package has two functions for querying the taxonomic information
in the FinBIF database.

## Taxa checking
You can use the function `finbif_check_taxa` to check whether taxa are in the
FinBIF database.

```r
(taxa <- finbif_check_taxa(c("Ursus arctos", "Moomin")))
```

```{.language-r}
#> [Ursus arctos] ID: MX.47348
#> [Moomin      ] Not found
```

If the taxa are present then the function returns their FinBIF ID, otherwise it
will return `NA`

```r
taxa[[1]]
```

```{.language-r}
#> Ursus arctos 
#>   "MX.47348"
```

```r
taxa[[2]]
```

```{.language-r}
#> Moomin 
#>     NA
```

When checking taxa, you can specify a taxonomic rank and only names with that
rank will have IDs returned if the name and rank combination is valid.

```r
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

```r
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

```r
finbif_taxa("Capreolus capreolus")
```

```{.language-r}
#> [content:                                                      ] ID: list(matchingName = "Capreolus capreolus", nameType = "MX.scientificName", id = "MX.47507", scientificName = "Capreolus capreolus", scientificNameAuthorship = "(Linnaeus, 1758)", taxonRank = "MX.species", cursiveName = TRUE, finnish = TRUE, species = TRUE, vernacularName = list(fi = "metsäkauris", en = "Roe Deer", sv = "rådjur"), informalGroups = list(list(id = "MVL.2", name = list(fi = "Nisäkkäät", en = "Mammals", sv = "Däggdjur"))), type = "exactMatches")
#> [path:                                                         ] ID: taxa/search
#> [response: url                                                 ] ID: https://api.laji.fi/v0/taxa/search?query=Capreolus%20capreolus&matchType=exact&limit=1
#> [response: status_code                                         ] ID: 200
#> [response: headers                                             ] ID: list(date = "Wed, 29 Jun 2022 06:48:42 GMT", `content-type` = "application/json; charset=utf-8", `content-length` = "433", `access-control-allow-origin` = "*", `access-control-allow-credentials` = "true", `x-frame-options` = "SAMEORIGIN", `x-download-options` = "noopen", etag = "W/\"1b1-Q/E3AqDTyjtsfdjfmS/H+yFWS54\"", vary = "Accept-Encoding", `cache-control` = "public", `x-xss-protection` = "1;mode=block", `x-content-type-options` = "nosniff", `strict-transport-security` = "max-age=31536000;includeSubDomains;preload", 
#>     `referrer-policy` = "no-referrer-when-downgrade")
#> [response: all_headers                                         ] ID: list(list(status = 200, version = "HTTP/1.1", headers = list(date = "Wed, 29 Jun 2022 06:48:42 GMT", `content-type` = "application/json; charset=utf-8", `content-length` = "433", `access-control-allow-origin` = "*", `access-control-allow-credentials` = "true", `x-frame-options` = "SAMEORIGIN", `x-download-options` = "noopen", etag = "W/\"1b1-Q/E3AqDTyjtsfdjfmS/H+yFWS54\"", vary = "Accept-Encoding", `cache-control` = "public", `x-xss-protection` = "1;mode=block", `x-content-type-options` = "nosniff", 
#>     `strict-transport-security` = "max-age=31536000;includeSubDomains;preload", `referrer-policy` = "no-referrer-when-downgrade")))
#> [response: cookies                                             ] ID: list(domain = logical(0), flag = logical(0), path = logical(0), secure = logical(0), expiration = numeric(0), name = logical(0), value = logical(0))
#> [response: content                                             ] ID: as.raw(c(0x5b, 0x7b, 0x22, 0x6d, 0x61, 0x74, 0x63, 0x68, 0x69, 0x6e, 0x67, 0x4e, 0x61, 0x6d, 0x65, 0x22, 0x3a, 0x22, 0x43, 0x61, 0x70, 0x72, 0x65, 0x6f, 0x6c, 0x75, 0x73, 0x20, 0x63, 0x61, 0x70, 0x72, 0x65, 0x6f, 0x6c, 0x75, 0x73, 0x22, 0x2c, 0x22, 0x6e, 0x61, 0x6d, 0x65, 0x54, 0x79, 0x70, 0x65, 0x22, 0x3a, 0x22, 0x4d, 0x58, 0x2e, 0x73, 0x63, 0x69, 0x65, 0x6e, 0x74, 0x69, 0x66, 0x69, 0x63, 0x4e, 0x61, 0x6d, 0x65, 0x22, 0x2c, 0x22, 0x69, 0x64, 0x22, 0x3a, 0x22, 0x4d, 0x58, 0x2e, 0x34, 0x37, 0x35, 
#> 0x30, 0x37, 0x22, 0x2c, 0x22, 0x73, 0x63, 0x69, 0x65, 0x6e, 0x74, 0x69, 0x66, 0x69, 0x63, 0x4e, 0x61, 0x6d, 0x65, 0x22, 0x3a, 0x22, 0x43, 0x61, 0x70, 0x72, 0x65, 0x6f, 0x6c, 0x75, 0x73, 0x20, 0x63, 0x61, 0x70, 0x72, 0x65, 0x6f, 0x6c, 0x75, 0x73, 0x22, 0x2c, 0x22, 0x73, 0x63, 0x69, 0x65, 0x6e, 0x74, 0x69, 0x66, 0x69, 0x63, 0x4e, 0x61, 0x6d, 0x65, 0x41, 0x75, 0x74, 0x68, 0x6f, 0x72, 0x73, 0x68, 0x69, 0x70, 0x22, 0x3a, 0x22, 0x28, 0x4c, 0x69, 0x6e, 0x6e, 0x61, 0x65, 0x75, 0x73, 0x2c, 0x20, 0x31, 0x37, 
#> 0x35, 0x38, 0x29, 0x22, 0x2c, 0x22, 0x74, 0x61, 0x78, 0x6f, 0x6e, 0x52, 0x61, 0x6e, 0x6b, 0x22, 0x3a, 0x22, 0x4d, 0x58, 0x2e, 0x73, 0x70, 0x65, 0x63, 0x69, 0x65, 0x73, 0x22, 0x2c, 0x22, 0x63, 0x75, 0x72, 0x73, 0x69, 0x76, 0x65, 0x4e, 0x61, 0x6d, 0x65, 0x22, 0x3a, 0x74, 0x72, 0x75, 0x65, 0x2c, 0x22, 0x66, 0x69, 0x6e, 0x6e, 0x69, 0x73, 0x68, 0x22, 0x3a, 0x74, 0x72, 0x75, 0x65, 0x2c, 0x22, 0x73, 0x70, 0x65, 0x63, 0x69, 0x65, 0x73, 0x22, 0x3a, 0x74, 0x72, 0x75, 0x65, 0x2c, 0x22, 0x76, 0x65, 0x72, 0x6e, 
#> 0x61, 0x63, 0x75, 0x6c, 0x61, 0x72, 0x4e, 0x61, 0x6d, 0x65, 0x22, 0x3a, 0x7b, 0x22, 0x66, 0x69, 0x22, 0x3a, 0x22, 0x6d, 0x65, 0x74, 0x73, 0xc3, 0xa4, 0x6b, 0x61, 0x75, 0x72, 0x69, 0x73, 0x22, 0x2c, 0x22, 0x65, 0x6e, 0x22, 0x3a, 0x22, 0x52, 0x6f, 0x65, 0x20, 0x44, 0x65, 0x65, 0x72, 0x22, 0x2c, 0x22, 0x73, 0x76, 0x22, 0x3a, 0x22, 0x72, 0xc3, 0xa5, 0x64, 0x6a, 0x75, 0x72, 0x22, 0x7d, 0x2c, 0x22, 0x69, 0x6e, 0x66, 0x6f, 0x72, 0x6d, 0x61, 0x6c, 0x47, 0x72, 0x6f, 0x75, 0x70, 0x73, 0x22, 0x3a, 0x5b, 0x7b, 
#> 0x22, 0x69, 0x64, 0x22, 0x3a, 0x22, 0x4d, 0x56, 0x4c, 0x2e, 0x32, 0x22, 0x2c, 0x22, 0x6e, 0x61, 0x6d, 0x65, 0x22, 0x3a, 0x7b, 0x22, 0x66, 0x69, 0x22, 0x3a, 0x22, 0x4e, 0x69, 0x73, 0xc3, 0xa4, 0x6b, 0x6b, 0xc3, 0xa4, 0xc3, 0xa4, 0x74, 0x22, 0x2c, 0x22, 0x65, 0x6e, 0x22, 0x3a, 0x22, 0x4d, 0x61, 0x6d, 0x6d, 0x61, 0x6c, 0x73, 0x22, 0x2c, 0x22, 0x73, 0x76, 0x22, 0x3a, 0x22, 0x44, 0xc3, 0xa4, 0x67, 0x67, 0x64, 0x6a, 0x75, 0x72, 0x22, 0x7d, 0x7d, 0x5d, 0x2c, 0x22, 0x74, 0x79, 0x70, 0x65, 0x22, 0x3a, 0x22, 
#> 0x65, 0x78, 0x61, 0x63, 0x74, 0x4d, 0x61, 0x74, 0x63, 0x68, 0x65, 0x73, 0x22, 0x7d, 0x5d))
#> [response: date                                                ] ID: 1656485322
#> [response: times                                               ] ID: c(redirect = 0, namelookup = 3.6e-05, connect = 3.6e-05, pretransfer = 0.00011, starttransfer = 0.217837, total = 0.217879)
#> [response: request                                             ] ID: list(method = "GET", url = "https://api.laji.fi/v0/taxa/search?query=Capreolus%20capreolus&matchType=exact&limit=1", headers = c(`Content-Type` = "", Accept = "application/json"), fields = NULL, options = list(post = TRUE, postfieldsize = 0, useragent = "https://github.com/luomus/finbif#0.6.5.9000:finbif_taxa()", httpget = TRUE), auth_token = NULL, output = list())
#> [response: handle                                              ] ID: <pointer: (nil)>
#> [hash:                                                         ] ID: 21cd8ef127e966d2e7c42a9e2a0d4d7d
```

### Partial matching
Searching for taxonomic information in FinBIF can also use "partial" matching.
For example, you might be interested in taxa that match a particular term, such
as 'deer'.

```r
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
