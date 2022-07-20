---
linktitle: 8. Filtering
title: Filtering Occurrence Data
draft: no
toc: yes
type: book
weight: 9
---



When getting records from FinBIF it's often a good idea to filter the data at
request time rather than after you have downloaded the data. Pre-filtering the
data will save bandwidth and local post-processing time. There are many options
for filtering occurrence records, for the full list of filtering options refer
to the package documentation.

```.language-r
?filters
```

You can filter occurrence records using the `filter` argument to
`finbif_occurrence`. The filter argument takes a list (or vector for some simple
filters), where the element names are the names of the filters and the elements
themselves are the filter values. The form of the filter varies depending on the
filter being used and is outlined in the documentation. In many cases the values
a filter can take can be found using `finbif_metadata()` and associated
functions (see [section 7. Metadata](tutorials/finbif/metadata/))

## Location
### Places

A number of filters allow you to restrict records geographically by place name.
These include `country`, `province`, `municipality` and `bird_assoc_area`
(BirdLife Finland local groups).

```.language-r
finbif_occurrence(filter = c(country = "Finland"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 41580509
#> A data.frame [10 x 12]
#>    record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1      …42#3            Apus apus        NA  60.4911   22.1561 
#> 2      …41#3 Phylloscopus trochi…        NA  60.4911   22.1561 
#> 3      …39#6       Sylvia curruca  1         59.83882  19.92228
#> 4      …39#3      Sylvia communis  1         59.84056  19.91378
#> 5      …35#5      Sylvia communis  1         61.0872   23.65435
#> 6      …35#3     Saxicola rubetra  2         61.0872   23.65435
#> 7     …31#15    Charadrius dubius  4         64.83067  26.10181
#> 8     …31#11       Turdus pilaris  1         64.82108  26.01163
#> 9      …31#3   Anas platyrhynchos  14        64.82164  25.96167
#> 10     …31#7            Apus apus  30        64.80656  25.99359
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Coordinates
You can also filter geographically by specifying coordinates. The coordinates
must be supplied with at least a latitude, longitude and a valid coordinate
system.

```.language-r
finbif_occurrence(
  filter = list(
    coordinates = list(lat = c(60, 68), lon = c(20, 30), system = "wgs84")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34695990
#> A data.frame [10 x 12]
#>    record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …3        Anas penelope        NA  64.99198  25.56643
#> 2        …21          Larus canus        NA  64.99198  25.56643
#> 3        …15       Sterna hirundo        NA  64.99198  25.56643
#> 4        …11     Numenius arquata        NA  64.99198  25.56643
#> 5        …17    Sterna paradisaea        NA  64.99198  25.56643
#> 6         …7 Haematopus ostraleg…        NA  64.99198  25.56643
#> 7        …19     Larus ridibundus        NA  64.99198  25.56643
#> 8        …31      Passer montanus        NA  64.99198  25.56643
#> 9        …27       Turdus iliacus        NA  64.99198  25.56643
#> 10       …13   Actitis hypoleucos        NA  64.99198  25.56643
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

## Dates
Another common way to filter is by date using the `date_range_ymd` filter.
Specifying a single date will filter records that fall on the day or within the
month or year indicated.

```.language-r
finbif_occurrence(filter = list(date_range_ymd = c("2019-12")))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 19883
#> A data.frame [10 x 12]
#>         record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44280127_Unit       Turdus merula  2         60.41401  22.24457
#> 2  …44304840_Unit   Dendrocopos major  1         60.40432  22.18121
#> 3  …44280136_Unit Emberiza citrinella  2         60.41401  22.24457
#> 4  …54619078_Unit       Turdus merula  3         60.27095  24.83408
#> 5  …44317394_Unit    Larus argentatus  1         64.66585  24.40813
#> 6  …54625618_Unit         Parus major  6         60.27448  24.86076
#> 7  …44308453_Unit        Corvus corax  1         61.97913  21.42103
#> 8  …44300432_Unit    Carduelis spinus  2         60.42983  22.21151
#> 9  …44286929_Unit   Fringilla coelebs  2         60.25655  21.38695
#> 10 …44304839_Unit    Carduelis spinus  10        60.40432  22.18121
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can further customize the date range filter by specifying an end date
allowing an arbitrary range of dates.

```.language-r
finbif_occurrence(
  filter = list(date_range_ymd = c("2019-06-01", "2019-12-31"))
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 835439
#> A data.frame [10 x 12]
#>         record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44280127_Unit       Turdus merula  2         60.41401  22.24457
#> 2  …44304840_Unit   Dendrocopos major  1         60.40432  22.18121
#> 3  …44280136_Unit Emberiza citrinella  2         60.41401  22.24457
#> 4  …54619078_Unit       Turdus merula  3         60.27095  24.83408
#> 5  …44317394_Unit    Larus argentatus  1         64.66585  24.40813
#> 6  …54625618_Unit         Parus major  6         60.27448  24.86076
#> 7  …44308453_Unit        Corvus corax  1         61.97913  21.42103
#> 8  …44300432_Unit    Carduelis spinus  2         60.42983  22.21151
#> 9  …44286929_Unit   Fringilla coelebs  2         60.25655  21.38695
#> 10 …44304839_Unit    Carduelis spinus  10        60.40432  22.18121
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also filter by time of year (i.e., a date range across all years) using
the `date_range_md` filter (note `_md` rather than `_ymd`). To filter a range of
dates that overlaps with the end of the year (e.g., winter) you'll need to
supply two date ranges: one for the end of the year and one for the start.

```.language-r
finbif_occurrence(
  filter = list(
    date_range_md = c(begin = "12-21", end = "12-31"),
    date_range_md = c(begin = "01-01", end = "02-20")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1699183
#> A data.frame [10 x 12]
#>    record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1       …132   Castor canadensis        NA  62.20497  23.44074
#> 2        …66 Phellinus igniarius  1         62.20497  23.44074
#> 3        …30         Alces alces  2         62.20497  23.44074
#> 4        …24         Alces alces  1         62.20497  23.44074
#> 5        …27    Poecile montanus  1         62.20497  23.44074
#> 6         …3       Vulpes vulpes  1         62.20497  23.44074
#> 7        …75       Vulpes vulpes  1         62.20497  23.44074
#> 8       …126       Vulpes vulpes  1         62.20497  23.44074
#> 9        …93       Vulpes vulpes  1         62.20497  23.44074
#> 10       …33       Vulpes vulpes  1         62.20497  23.44074
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

## Data quality
Not all data in FinBIF is created equal. Often it will be desirable to use
`{finbif}`'s data quality filters. The package documentation outlines each
quality filter in detail.

To restrict occurrence records to the highest quality level you can use the
following set of filters.

```.language-r
strict <- list(
  collection_quality = "professional",
  coordinates_uncertainty_max = 1,
  record_quality = "expert_verified"
)
```
These filters will limit the occurrence records to those belonging to the most
reliable collections, have the least coordinate uncertainty (most precise
location data), and have reliable taxonomic identifications.

At the other end of the spectrum, you can also allow all records regardless of
quality with the following filter.

```.language-r
permissive <- list(
  quality_issues = "both",
  record_reliability = c(
    "reliable", "unassessed", "unreliable"),
  record_quality = c(
    "expert_verified", "community_verified", 
    "unassessed", "uncertain", "erroneous"
  )
)
```
This will include all records, both with and without, quality issues.

The highest quality records are only a small fraction of all the records that
are available.

```.language-r
finbif_occurrence(filter = list(strict, permissive), count_only = TRUE)
```

```{.language-r}
#> [[1]]
#> [1] 51
#> 
#> [[2]]
#> [1] 44002863
```

## Collections
You can filter by collection using the collection ID, the collection name or
the abbreviated collection name (if available).

```.language-r
finbif_occurrence(
  filter = c(collection = "iNaturalist Suomi Finland"), count_only = TRUE
)
```

```{.language-r}
#> [1] 504372
```

You can also use the results of a call to the `finbif_collections` function as
filter directly.

```.language-r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland",
  nmin   = 10000
)

finbif_occurrence(filter = list(collection = collections), count_only = TRUE)
```

```{.language-r}
#> [1] 13577108
```

## Informal groups
Many informal taxonomic groups align with formal taxonomic groups (e.g., birds)
but some, such as "Reptiles & amphibians" do not, making the `informal_group`
potential useful in some circumstances.

```.language-r
finbif_occurrence(filter = list(informal_group = "Reptiles and amphibians"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 44950
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62bbcbcdd5d…      Anguis fragilis  1         61.10221  22.88537
#> 2  …KE.176/62bbd8e9d5d… Pelophylax esculent…  3         60.61041  21.5252 
#> 3  …KE.176/62bb6a86d5d…      Anguis fragilis  1         59.98272  23.99422
#> 4  …KE.176/62bb617fd5d…      Anguis fragilis  1         60.14724  24.36741
#> 5  …HR.3211/123833894-U     Zootoca vivipara        NA  63.64611  27.17139
#> 6  …HR.3211/123838182-U      Rana temporaria        NA        NA        NA
#> 7  …KE.176/62baf319d5d…      Anguis fragilis  1         61.98459  24.06683
#> 8  …KE.176/62baeaffd5d…      Anguis fragilis  1         60.04463  24.55186
#> 9  …HR.3211/123804109-U     Zootoca vivipara        NA  61.03338  25.88673
#> 10 …KE.176/62baa39cd5d…      Anguis fragilis  1         61.47152  24.43033
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

## Taxon status
Other useful filters include those associated with the status of taxa or their
presence on various checklists. The function `finbif_metadata` can be used to
see what the allowable values are for these filters.

### Administrative status
Many taxa appear on various lists such as the EU's invasive species list. The
`adminstrative_status` filter makes it easy to search for records of birds
considered invasive in the EU.

```.language-r
finbif_occurrence("birds", filter = list(administrative_status = "EU_INVSV"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 469
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62b1ad90d5d…   Oxyura jamaicensis  7         61.66207  23.57706
#> 2        …JX.1045316#34 Alopochen aegyptiaca  3         52.16081  4.485534
#> 3        …JX.138840#123 Alopochen aegyptiaca  4         53.36759  6.191796
#> 4        …JX.139978#214 Alopochen aegyptiaca  6         53.37574  6.207861
#> 5         …JX.139710#17 Alopochen aegyptiaca  30        52.3399   5.069133
#> 6         …JX.139645#57 Alopochen aegyptiaca  36        51.74641  4.535283
#> 7         …JX.139645#10 Alopochen aegyptiaca  3         51.74641  4.535283
#> 8         …JX.139442#16 Alopochen aegyptiaca  2         51.90871  4.53258 
#> 9      …KE.8_1208123#15 Alopochen aegyptiaca  2         53.19242  5.437417
#> 10    …KE.8_1208068#101 Alopochen aegyptiaca  20        53.32081  6.192341
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Red list
Using the `red_list` filter you can search for records of near threatened
mammals.

```.language-r
finbif_occurrence("mammals", filter = list(red_list_status = "NT"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 2457
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62bab390d5d…         Castor fiber  1         62.24068  28.8834 
#> 2         …JX.1408115#3 Rangifer tarandus f…  1         63.21216  24.31222
#> 3        …JX.1397132#39 Rangifer tarandus f…  2         64.13285  26.27761
#> 4       …JX.1396580#493 Rangifer tarandus f…  1         64.32912  28.7958 
#> 5  …HR.3211/121755178-U Rangifer tarandus f…        NA  63.5      24.3    
#> 6  …HR.3211/121759281-U Rangifer tarandus f…        NA  63.5      24.3    
#> 7  …HR.3211/121755627-U Rangifer tarandus f…        NA  63.9      24.7    
#> 8        …JX.1392113#15 Rangifer tarandus f…  1         64.0517   28.32895
#> 9  …KE.176/62a04ad6d5d… Pusa hispida botnica  1         60.21181  25.37497
#> 10       …JX.1390384#11 Rangifer tarandus f…  1         64.33209  25.73386
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Finnish occurrence
Many taxa in the FinBIF database have been given an "Finnish occurrence status"
and this status can be used to filter records.

```.language-r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 357479
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1411601#9     Stegania cararia  3         61.48089  29.45853
#> 2         …JX.1411614#3 Habrosyne pyritoides  1         61.71285  29.39905
#> 3        …JX.1411450#36      Ancylis upupana  1         61.51447  24.0233 
#> 4        …JX.1411450#15  Eupithecia selinata  1         61.51447  24.0233 
#> 5        …JX.1411579#17        Pyrgus alveus  2         60.24476  22.30047
#> 6  …HR.3211/123829199-U Korscheltellus lupu…        NA  60.98495  25.54631
#> 7         …JX.1411456#6         Colias tyche  1         69.06191  20.82332
#> 8         …JX.1411456#3     Euphydryas iduna  6         69.06191  20.82332
#> 9  …HR.3211/123811818-U Ypsolopha chazariel…        NA  60.31112  25.03602
#> 10        …JX.1411418#3      Eucosma fulvana  2         61.71372  29.39204
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also use the negation of the `finnish_occurrence_status` to filter out
records of that have a given occurrence status. For example, you can get
records of bird species that are not considered to have stable populations in
Finland with the following filter.

```.language-r
finbif_occurrence(
  "Birds",
  filter = c(finnish_occurrence_status_neg = "stable", taxon_rank = "species")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 87286
#> A data.frame [10 x 12]
#>               record_id    scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1411170#15    Cuculus optatus  1         65.49352  28.49518
#> 2  …HR.3211/123944572-U Larus delawarensis        NA  60.16689  24.95329
#> 3         …JX.1411012#9      Anser indicus  2         66.14103  23.9269 
#> 4        …JX.1411227#42  Emberiza calandra        NA  41.8644   41.78842
#> 5  …HR.4412/62bb91c8a5…      Porzana parva        NA  61.07488  25.42196
#> 6  …HR.4412/62b8eeba6b…    Ciconia ciconia        NA  60.25712  24.73883
#> 7  …HR.4412/62ba404d95…  Coturnix coturnix        NA  60.90381  26.53609
#> 8  …HR.4412/62b8eea0c3…  Coturnix coturnix        NA  60.76706  23.41777
#> 9  …HR.4412/62b8ee7f2a…  Coturnix coturnix        NA  59.95088  23.14806
#> 10 …HR.4412/62b79ca842…  Coturnix coturnix        NA  65.01496  24.76885
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```
