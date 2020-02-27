---
title: Metadata
draft: no
toc: yes
type: docs
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
#> 3  countries                
#> 4  provinces                
#> 5  municipalities           
#> 6  bird_assoc_areas         
#> 7  finnish_occurrence_status
#> 8  habitat_types            
#> 9  habitat_qualifiers       
#> 10 life_stages              
#> 11 record_basis             
#> 12 restriction_levels       
#> 13 restriction_reasons      
#> 14 sex_categories           
#> 15 sources                  
#> 16 taxon_ranks
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
Some, more complex, metadata is accessed with other `{finbif}` functions

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
#> ...111 more groups
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

```{.language-r}
#>         collection_name            taxonomic_coverage         count  
#> HR.1227 Coll Mikko Heikkinen       Biota                           61
#> HR.1349 JYV - Fungal collections   <NA>                         13398
#> HR.1350 JYV - Lichen collections   <NA>                           398
#> HR.1351 JYV - Bryophyte collectio… <NA>                          3227
#> HR.1467 Per-Eric Grankvist´s butt… Lepidoptera                      5
#> HR.1487 JYV - Fish collections     <NA>                          1371
#> HR.1507 Lingonblad Birger och Hjö… Lepidoptera                   2797
#> HR.1592 Herbarium of The Ark Natu… <NA>                          1287
#> HR.1687 Papilionoidea of Coll. La… Papilionoidea                  525
#> HR.1688 Noctuidae I of Coll. Lauro Noctuidae                      614
#> HR.1689 Noctuidae II of Coll. Lau… Noctuidae                      839
#> HR.1690 Noctuidae III, Bombycoide… Noctuidae, Bombycoidea, G…     521
#> HR.1691 Drepanidae & Geometridae … Drepanidae, Geometridae       1408
#> HR.175  National Finnish butterfl… Lepidoptera                 349461
#> HR.200  Finnish Insect Database    Insecta                    3728982
#> HR.2049 Invasive alien species co… Invasive species                93
#> HR.206  The Finnish Nature League… biota                        82296
#> HR.2089 Håkan Lindberg collection  Hymenoptera                   2295
#> HR.209  Atlas of Finnish Macrolep… Macrolepidoptera           1217383
#> HR.2209 KUO Arachnida collection   Arachnida                        3
#> HR.2289 Specimens that lack colle… <NA>                           109
#> HR.2691 Line transect censuses of… Aves                        588124
#> HR.2692 Censuses of breeding bird… Aves                         14963
#> HR.3051 Viekas project invasive s… <NA>                           603
#> HR.3071 Observing species on milk… <NA>                           160
#> HR.3211 iNaturalist                <NA>                         15716
#> HR.39   Winter Bird Census         Aves                       1354203
#> HR.435  Löydös Open Invasive Spec… Biota                        11667
#> HR.60   Monitoring scheme of bird… Aves, Mammalia              769290
#> HR.627  Invasive mammal species o… Mammalia                       228
#> HR.808  E. Sjöholm´s butterfly co… Lepidoptera                   4952
#> HR.847  Atlas of amphibians and r… Amphibia, Reptilia            5106
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
#>        collection_name abbreviation description online_url has_children
#> HR.129 Collections of… H            Herbarium … <NA>        TRUE       
#> HR.160 Zoological col… MZH          The collec… http://ww…  TRUE       
#> HR.173 Zoological mon… <NA>         Monitoring… <NA>        TRUE       
#> HR.203 Löydös Open Fi… <NA>         A service … http://ws…  TRUE       
#> HR.447 Hatikka.fi obs… <NA>         Hatikka.fi… http://ha… FALSE       
#> HR.48  Ringing and re… TIPU         Database o… <NA>        TRUE       
#>        is_part_of data_quality methods collection_type taxonomic_coverage
#> HR.129 HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#> HR.160 HR.128     MY.dataQual… NA      MY.collectionT… Animalia          
#> HR.173 HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#> HR.203 HR.128     MY.dataQual… NA      MY.collectionT… biota             
#> HR.447 HR.128     MY.dataQual… NA      MY.collectionT… Biota             
#> HR.48  HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#>        geographic_coverage temporal_coverage secure_level count   
#> HR.129 <NA>                <NA>              <NA>             1512
#> HR.160 World               1700 to present   MX.secureLe…      957
#> HR.173 Finland             1950-             <NA>          4129953
#> HR.203 world               2013-             <NA>            14378
#> HR.447 World               <NA>              <NA>          2012956
#> HR.48  Ringing data: Finl… 1913-             <NA>         11911188
```
