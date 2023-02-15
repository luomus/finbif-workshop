---
linktitle: 7. Metadata
title: Metadata
draft: no
toc: yes
type: book
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

```
#>    metadata_name            
#> 1  regulatory_status        
#> 2  red_list                 
#> 3  country                  
#> 4  region                   
#> 5  bio_province             
#> 6  municipality             
#> 7  bird_assoc_area          
#> 8  finnish_occurrence_status
#> 9  habitat_type             
#> 10 habitat_qualifier        
#> 11 life_stage               
#> 12 record_basis             
#> 13 restriction_level        
#> 14 restriction_reason       
#> 15 sex_category             
#> 16 source                   
#> 17 taxon_rank
```

Calling `finbif_metadata()` and specifying one of the metadata categories will
display a `data.frame` with the requested metadata.

```r
finbif_metadata("red_list")
```

```
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

```
#> Algae                                                         
#>  ¦--Macro algae                                               
#>      ¦--Brown algae and yellow green algae                    
#>      ¦--Green algae                                           
#>      ¦--Red algae                                             
#>      ¦--Stoneworts                                            
#> ...142 more groups
```

You can select a subgroup by specifying a parent informal group as a function
argument.

```r
finbif_informal_groups("Crustaceans")
```

```
#> Crustaceans                                                   
#>  ¦--Macrocrustaceans                                          
#>  ¦   ¦--Amphipods, isopods, opossum shrimps                   
#>  ¦   ¦--Crabs, shrimps and crayfishes                         
#>  ¦   ¦--Other macrocrustaceans                                
#>  ¦   ¦--Woodlice                                              
#>  ¦--Microcrustaceans                                          
#>      ¦--Branchiopoda                                          
#>      ¦--Copepods                                              
#>      ¦--Seed shrimps
```

## Collections
Another special case of metadata is `finbif_collections()`. Collections are the
highest level of record aggregation in the FinBIF database.

You can subset collection metadata by using the `filter` and `select` arguments.

```r
finbif_collections(
  filter = taxonomic_coverage == "fungi",
  select = c("collection_name", "geographic_coverage", "count")
)
```

```
#> [1] collection_name     geographic_coverage count              
#> <0 rows> (or 0-length row.names)
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
are the ID of the collection.

```r
collections <- finbif_collections(
  supercollections = TRUE
)

collections["HR.128", "collection_name"]
```

```
#> [1] "Collections of the Finnish Museum of Natural History Luomus"
```

You can see the child collections of a supercollection by specifying the ID as
a filter. Note that the children of supercollections may also be supercollections

```r
finbif_collections(
  is_part_of == "HR.128", "collection_name", supercollections = TRUE
)
```

```
#>         collection_name                          
#> HR.129  Collections of the Botanical Museum      
#> HR.160  Zoological collections                   
#> HR.173  Zoological monitoring schemes            
#> HR.1849 Genomic resources collection samples     
#> HR.203  Löydös Open Finnish Observation Database 
#> HR.435  Löydös Open Invasive Species Observations
#> HR.447  Hatikka.fi observations                  
#> HR.48   Ringing and recovery database of birds
```
