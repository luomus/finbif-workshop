---
title: Metadata
draft: no
toc: yes
type: book
weight: 8
menu:
  finbif:
    name: 7. Metadata
    weight: 8
---


Much of the information in the FinBIF database consists of metadata that helps
provide context for occurrence records and other information in FinBIF.

## General metadata
You can see some of the metadata available in `{finbif}` by calling the
`finbif_metadata` function without any arguments.

```r
finbif_metadata()
```

```{.language-r}
#>    metadata_name            
#> 1  admin_status             
#> 2  red_list                 
#> 3  country                  
#> 4  province                 
#> 5  municipality             
#> 6  bird_assoc_area          
#> 7  finnish_occurrence_status
#> 8  habitat_type             
#> 9  habitat_qualifier        
#> 10 life_stage               
#> 11 record_basis             
#> 12 restriction_level        
#> 13 restriction_reason       
#> 14 sex_category             
#> 15 source                   
#> 16 taxon_rank
```

Calling `finbif_metadata()` and specifying one of the metadata categories will
display a `data.frame` with the requested metadata.

```r
finbif_metadata("red_list")
```

```{.language-r}
#>    status_name           status_code
#> 1  Critically Endangered CR         
#> 2  Data Deficient        DD         
#> 3  Endangered            EN         
#> 4  Extinct               EX         
#> 5  Extinct in the Wild   EW         
#> 6  Least Concern         LC         
#> 7  Near Threatened       NT         
#> 8  Not Applicable        NA         
#> 9  Not Evaluated         NE         
#> 10 Regionally Extinct    RE         
#> 11 Vulnerable            VU
```

## Special cases
Some more complex metadata is accessed with other `{finbif}` functions

### Informal groups
Informal taxonomic groups and their relationships can be displayed with
`finbif_informal_groups()`

```r
finbif_informal_groups(limit = 6)
```

```{.language-r}
#> Algae                                                         
#>  °--Macro algae                                               
#>      ¦--Brown algae and yellow green algae                    
#>      ¦--Green algae                                           
#>      ¦--Red algae                                             
#>      °--Stoneworts                                            
#> ...142 more groups
```

You can select a subgroup by specifying a parent informal group as a function
argument.

```r
finbif_informal_groups("Crustaceans")
```

```{.language-r}
#> Crustaceans                                                   
#>  ¦--Macrocrustaceans                                          
#>  ¦   ¦--Amphipods, isopods, opossum shrimps                   
#>  ¦   ¦--Crabs, shrimps and crayfishes                         
#>  ¦   ¦--Other macrocrustaceans                                
#>  ¦   °--Woodlice                                              
#>  °--Microcrustaceans                                          
#>      ¦--Branchiopoda                                          
#>      ¦--Copepods                                              
#>      °--Seed shrimps
```

## Collections
Another special case of metadata is `finbif_collections()`. Collections are the
highest level of record aggregation in the FinBIF database.

You can subset collection metadata by using the `filter` and `select` arguments.

```r
finbif_collections(
  filter = geographic_coverage == "Finland",
  select = c("collection_name", "taxonomic_coverage", "count")
)
```

```
#> Warning in is.na(cols) || is.null(cols): 'length(x) = 3 > 1' in coercion to
#> 'logical(1)'
```

```{.language-r}
#>         collection_name            taxonomic_coverage         count  
#> HR.1227 Coll Mikko Heikkinen       Biota                           67
#> HR.1349 JYV - Fungal collections   <NA>                         13443
#> HR.1350 JYV - Lichen collections   <NA>                           541
#> HR.1351 JYV - Bryophyte collectio… <NA>                          5760
#> HR.1467 Per-Eric Grankvist´s butt… Lepidoptera                      5
#> HR.1487 JYV - Fish collections     <NA>                          1371
#> HR.1507 Lingonblad Birger och Hjö… Lepidoptera                   2796
#> HR.157  Point counts of breeding … Birds, landbirds            384824
#> HR.1592 Herbarium of The Ark Natu… <NA>                          7864
#> HR.1687 Papilionoidea of Coll. La… Papilionoidea                  550
#> HR.1688 Noctuidae I of Coll. Lauro Noctuidae                      614
#> HR.1689 Noctuidae II of Coll. Lau… Noctuidae                      839
#> HR.1690 Noctuidae III, Bombycoide… Noctuidae, Bombycoidea, G…     521
#> HR.1691 Drepanidae & Geometridae … Drepanidae, Geometridae       1408
#> HR.175  National Finnish butterfl… Lepidoptera                 423571
#> HR.1916 Wildlife triangle          Siberian flying squirrel …   18560
#> HR.200  Finnish Insect Database    Insecta                    3725794
#> HR.2009 Fish observation data fro… invasive alien fish speci…   34396
#> HR.2049 Invasive alien species co… Invasive species              1040
#> HR.206  The Finnish Nature League… biota                       115286
#> HR.2089 Håkan Lindberg collection  Hymenoptera                   2435
#> HR.209  Atlas of Finnish Macrolep… Macrolepidoptera           1218552
#> HR.2129 Fungal atlas               fungi                       102238
#> HR.2209 KUO Arachnida collection   Arachnida                        3
#> HR.2289 Specimens that lack colle… <NA>                           109
#> HR.2691 Line transect censuses of… Aves                        608520
#> HR.2692 Censuses of breeding bird… Aves                         14963
#> HR.3051 VieKas LIFE project invas… <NA>                          1399
#> HR.3071 Observing species on milk… <NA>                           529
#> HR.3211 iNaturalist Suomi Finland  biota                       504372
#> HR.3491 LajiGIS: Aquatic species … Biota                       592897
#> HR.3553 LajiGIS: Species monitori… Biota                       696609
#> HR.3671 Bird of prey nests for pr… Aves                         10246
#> HR.3691 eBird                      Aves                        806562
#> HR.3791 Invasive species observat… Biota                         1993
#> HR.39   Winter Bird Census         Aves, Mammalia             1447328
#> HR.3911 Bumblebee census           Bumblebees                    7394
#> HR.3991 Waterbird counts, Luomus … Aves                          3068
#> HR.3992 Waterbird counts, Luke da… Aves                          2429
#> HR.4011 Salmonidae in streams      Salmonidae                   12630
#> HR.4051 LajiGIS: Species monitori… Aquila chrysaetos; Haliae…    8083
#> HR.4091 Retkikasvio                <NA>                            66
#> HR.4131 Butterflies in Finnish ag… Papilionoidea, Others       356987
#> HR.4191 Butterfly Collection by C… Lepidoptera                  10415
#> HR.4251 LajiGIS: Species surveys   Biota                       238301
#> HR.435  Löydös Open Invasive Spec… Biota                        17791
#> HR.4352 NFI rare tree species      <NA>                           997
#> HR.4412 Tiira.fi: The Fourth Bree… Aves                        140113
#> HR.4471 4th Finnish Bird Atlas, o… Aves                         74481
#> HR.4511 Finnish National Moth Mon… Bombycoidea, Noctuoidea, … 1156357
#> HR.4612 Pölyttäjäseuranta          Insecta                       1142
#> HR.60   Monitoring scheme of bird… Aves, Mammalia              851835
#> HR.627  Invasive mammal species o… Mammalia                       228
#> HR.808  E. Sjöholm´s butterfly co… Lepidoptera                   4951
#> HR.847  Atlas of amphibians and r… Amphibia, Reptilia            6415
```

By default, `finbif_collections()` only displays the lowest level collections.
Higher level, "supercollections" can be viewed by setting
`supercollections = TRUE` and you can limit the output to collections with
a minimum number of records in them with the `nmin` argument.

```r
collections <- finbif_collections(supercollections = TRUE, nmin = 10000)
View(collections)
```

The `finbif_collections()` function returns a `data.frame` where the row names
are the ID number of the collection.

```r
finbif_collections(supercollections = TRUE)["HR.128", "collection_name"]
```

```{.language-r}
#> [1] "Collections of the Finnish Museum of Natural History Luomus"
```

You can see the child collections of a supercollection by specifying the ID as
a filter. Note that the children of supercollections may also be supercollections

```r
finbif_collections(is_part_of == "HR.128", supercollections = TRUE)
```

```{.language-r}
#>         collection_name abbreviation description online_url has_children
#> HR.129  Collections of… H            Herbarium … <NA>        TRUE       
#> HR.160  Zoological col… MZH          The collec… http://ww…  TRUE       
#> HR.173  Zoological mon… <NA>         Monitoring… <NA>        TRUE       
#> HR.1849 Genomic resour… <NA>         Genomic re… <NA>        TRUE       
#> HR.203  Löydös Open Fi… <NA>         A service … https://l… FALSE       
#> HR.435  Löydös Open In… <NA>         A service … https://l… FALSE       
#> HR.447  Hatikka.fi obs… <NA>         Hatikka.fi… http://ha… FALSE       
#> HR.48   Ringing and re… TIPU         Database o… <NA>        TRUE       
#>         is_part_of data_quality methods   collection_type taxonomic_coverage
#> HR.129  HR.128     MY.dataQual… <NA>      MY.collectionT… <NA>              
#> HR.160  HR.128     MY.dataQual… <NA>      MY.collectionT… Animalia          
#> HR.173  HR.128     MY.dataQual… <NA>      MY.collectionT… <NA>              
#> HR.1849 HR.128     MY.dataQual… Sampling… MY.collectionT… Biota             
#> HR.203  HR.128     <NA>         <NA>      MY.collectionT… biota             
#> HR.435  HR.128     MY.dataQual… <NA>      MY.collectionT… Biota             
#> HR.447  HR.128     MY.dataQual… <NA>      MY.collectionT… Biota             
#> HR.48   HR.128     MY.dataQual… <NA>      MY.collectionT… <NA>              
#>         geographic_coverage temporal_coverage secure_level count   
#> HR.129  <NA>                <NA>              <NA>                2
#> HR.160  World               1700 to present   MX.secureLe…      743
#> HR.173  Finland             1950-             <NA>          4882057
#> HR.1849 World               2000-             <NA>                1
#> HR.203  world               2013-             <NA>            30508
#> HR.435  Finland             2015-             <NA>            17791
#> HR.447  World               <NA>              <NA>          2010232
#> HR.48   Ringing data: Finl… 1913-             <NA>         12642149
```
