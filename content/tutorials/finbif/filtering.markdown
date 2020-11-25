---
title: Filtering Occurrence Data
draft: no
toc: yes
type: docs
weight: 9
menu:
  finbif:
    name: 8. Filtering
    weight: 9
---



When getting records from FinBIF it's often a good idea to filter the data at
request time rather than after you have downloaded the data. Pre-filtering the
data will save bandwidth and local post-processing time. There are many options
for filtering occurrence records, for the full list of filtering options refer
to the package documentation.

```r
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

```r
finbif_occurrence(filter = c(country = "Finland"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 36008265
#> A data.frame [10 x 12]
#>               record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1          JX.1176642#4    Poecile montanus  4         61.00708  26.43348
#> 2          JX.1176641#4         Parus major  10        61.01079  26.44975
#> 3          JX.1176640#4 Cyanistes caeruleus  12        61.01079  26.44975
#> 4  KE.176/5fbe1425d5de…      Sitta europaea  1         65.39619  27.31273
#> 5          JX.1176602#4 Chelifer cancroides  1         60.43392  22.38267
#> 6         JX.1176634#10           Pica pica  1         68.41036  27.41244
#> 7          JX.1176634#7    Poecile montanus  2         68.41036  27.41244
#> 8          JX.1176634#4         Parus major  6         68.41036  27.41244
#> 9         JX.1176537#13            Anatidae  4         60.17956  24.66378
#> 10        JX.1176537#16                Aves  3         60.17956  24.66378
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Coordinates
You can also filter geographically by specifying coordinates. The coordinates
must be supplied with at least a latitude, longitude and a valid coordinate
system.

```r
finbif_occurrence(
  filter = list(
    coordinates = list(lat = c(60, 68), lon = c(20, 30), system = "wgs84")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 29884902
#> A data.frame [10 x 12]
#>               record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1          JX.1176642#4    Poecile montanus  4         61.00708  26.43348
#> 2          JX.1176641#4         Parus major  10        61.01079  26.44975
#> 3          JX.1176640#4 Cyanistes caeruleus  12        61.01079  26.44975
#> 4  KE.176/5fbe1425d5de…      Sitta europaea  1         65.39619  27.31273
#> 5          JX.1176602#4 Chelifer cancroides  1         60.43392  22.38267
#> 6         JX.1176537#13            Anatidae  4         60.17956  24.66378
#> 7         JX.1176537#16                Aves  3         60.17956  24.66378
#> 8         JX.1176537#19             Insecta  5         60.17956  24.66378
#> 9          JX.1176537#7                Aves  23        60.17956  24.66378
#> 10         JX.1176537#4         Parus major  1         60.17956  24.66378
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

## Dates
Another common way to filter is by date using the `date_range_ymd` filter.
Specifying a single date will filter records that fall on the day or within the
month or year indicated.

```r
finbif_occurrence(filter = list(date_range_ymd = c("2019-12")))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 19083
#> A data.frame [10 x 12]
#>               record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  tun.fi/HR.3211/6524…    Pinus sylvestris  1         68.84709  28.33712
#> 2  mus.utu.fi/MY.72933…        Viscum album  1         60.4638   22.3343 
#> 3  mus.utu.fi/MY.73114… Nowellia curvifolia  1         60.38972  22.52086
#> 4  tun.fi/HR.3211/3712… Bombycilla garrulus  1         60.16761  24.94694
#> 5  tun.fi/KE.921/LGE.6…     Pteromys volans  1         61.81362  25.75756
#> 6  tun.fi/HR.3211/3712…           Pica pica  1         60.16964  24.95628
#> 7  tun.fi/HR.3691/OBS8… Emberiza citrinella  10        60.4811   22.1214 
#> 8  tun.fi/HR.3691/OBS8…     Chloris chloris  1         60.414    22.2446 
#> 9  tun.fi/HR.3691/OBS8…        Corvus corax  2         60.3753   23.7216 
#> 10 tun.fi/HR.3691/OBS8… Carduelis carduelis  1         60.177    24.7949 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can further customize the date range filter by specifying an end date
allowing an arbitrary range of dates.

```r
finbif_occurrence(
  filter = list(date_range_ymd = c("2019-06-01", "2019-12-31"))
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 587345
#> A data.frame [10 x 12]
#>               record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  tun.fi/HR.3211/6524…    Pinus sylvestris  1         68.84709  28.33712
#> 2  mus.utu.fi/MY.72933…        Viscum album  1         60.4638   22.3343 
#> 3  mus.utu.fi/MY.73114… Nowellia curvifolia  1         60.38972  22.52086
#> 4  tun.fi/HR.3211/3712… Bombycilla garrulus  1         60.16761  24.94694
#> 5  tun.fi/KE.921/LGE.6…     Pteromys volans  1         61.81362  25.75756
#> 6  tun.fi/HR.3211/3712…           Pica pica  1         60.16964  24.95628
#> 7  tun.fi/HR.3691/OBS8… Emberiza citrinella  10        60.4811   22.1214 
#> 8  tun.fi/HR.3691/OBS8…     Chloris chloris  1         60.414    22.2446 
#> 9  tun.fi/HR.3691/OBS8…        Corvus corax  2         60.3753   23.7216 
#> 10 tun.fi/HR.3691/OBS8… Carduelis carduelis  1         60.177    24.7949 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also filter by time of year (i.e, a date range across all years) using
the `date_range_md` filter (note `_md` rather than `_ymd`). To filter a range of
dates that overlaps with the end of the year (e.g., winter) you'll need to
supply two date ranges: one for the end of the year and one for the start.

```r
finbif_occurrence(
  filter = list(
    date_range_md = c(begin = "12-21", end = "12-31"),
    date_range_md = c(begin = "01-01", end = "02-20")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1555025
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  tun.fi/KE.921/LGE.6…   Bazzania trilobata  1         60.06576  23.77395
#> 2  tun.fi/KE.921/LGE.6…   Calypogeia suecica  1         60.06707  23.77198
#> 3  tun.fi/KE.921/LGE.6…     Scapania nemorea  1         60.06576  23.77395
#> 4  tun.fi/KE.921/LGE.6…  Bazzania tricrenata  1         60.06576  23.77395
#> 5   tun.fi/JX.1099335#4   Rhizocybe pruinosa  7         61.47031  23.37529
#> 6  mus.utu.fi/MY.94320…  Bazzania tricrenata  1         60.06577  23.77395
#> 7  mus.utu.fi/MY.94319…   Bazzania trilobata  1         60.06577  23.77395
#> 8  mus.utu.fi/MY.94319…   Calypogeia suecica  1         60.06708  23.77197
#> 9  mus.utu.fi/MY.94320… Herzogiella striate…  1         60.06577  23.77395
#> 10 mus.utu.fi/MY.94320…      Hypnum imponens  1         60.06577  23.77395
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

```r
strict <- c(
  collection_quality = "professional", coordinates_uncertainty_max = 1,
  record_quality = "expert_verified"
)
```
These filters will limit the occurrence records to those belonging to the most
reliable collections, have the least coordinate uncertainty (most precise
location data), and have reliable taxonomic identifications.

At the other end of the spectrum, you can also allow all records regardless of
quality with the following filter.

```r
permissive <- list(
  quality_issues = "both",
  record_reliability = c("reliable", "unassessed", "unreliable"),
  record_quality = c(
    "expert_verified", "community_verified", "unassessed", "uncertain",
    "erroneous"
  )
)
```
This will include all records, both with and without, quality issues.

The highest quality records are only a small fraction of all the records that
are available.

```r
c(
  strict     = finbif_occurrence(filter = strict,     count_only = TRUE),
  permissive = finbif_occurrence(filter = permissive, count_only = TRUE)
)
```

```{.language-r}
#>     strict permissive 
#>         16   38304202
```

## Collections
You can filter by collection using the collection ID, the collection name or
the abbreviated collection name (if available).

```r
finbif_occurrence(
  filter = c(collection = "iNaturalist Suomi Finland"), count_only = TRUE
)
```

```{.language-r}
#> [1] 238719
```

You can also use the results of a call to the `finbif_collections` function as
filter directly.

```r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland",
  nmin   = 10000
)

finbif_occurrence(filter = list(collection = collections), count_only = TRUE)
```

```{.language-r}
#> [1] 10508335
```

## Informal groups
Many informal taxonomic groups align with formal taxonomic groups (e.g., birds)
but some, such as "Reptiles & amphibians" do not, making the `informal_group`
potential useful in some circumstances.

```r
finbif_occurrence(filter = list(informal_group = "Reptiles and amphibians"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 37632
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  KE.176/5fb7ba4bd5de…      Anguis fragilis  1         60.5007   25.05817
#> 2    HR.3211/65137611-U      Rana temporaria  1         60.45358  22.40777
#> 3  KE.176/5fa6c8e9d5de…            Bufo bufo  10        60.39596  25.1878 
#> 4    HR.3211/63305915-U              Ranidae  1         60.48971  22.43561
#> 5    HR.3211/62991435-U      Rana temporaria  1         62.65     23.15   
#> 6    HR.3211/63876686-U     Zootoca vivipara  1         61.79251  23.63291
#> 7    HR.3211/62890648-U      Rana temporaria  1         60.25     23.65   
#> 8    HR.3211/62781862-U     Zootoca vivipara  1         62.25     26.35   
#> 9  KE.176/5f8c62d0d5de… Pelophylax esculent…  1         65.20437  25.44325
#> 10 KE.176/5f86d744d5de…      Anguis fragilis  1         60.15856  24.18494
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

```r
finbif_occurrence("birds", filter = list(administrative_status = "EU_INVSV"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 454
#> A data.frame [10 x 12]
#>           record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1     JX.1045316#34 Alopochen aegyptiaca  3         52.16081  4.485534
#> 2     JX.138840#123 Alopochen aegyptiaca  4         53.36759  6.191796
#> 3     JX.139978#214 Alopochen aegyptiaca  6         53.37574  6.207861
#> 4      JX.139710#17 Alopochen aegyptiaca  30        52.3399   5.069133
#> 5      JX.139645#57 Alopochen aegyptiaca  36        51.74641  4.535283
#> 6      JX.139645#10 Alopochen aegyptiaca  3         51.74641  4.535283
#> 7      JX.139442#16 Alopochen aegyptiaca  2         51.90871  4.53258 
#> 8   KE.8_1208123#15 Alopochen aegyptiaca  2         53.19242  5.437417
#> 9  KE.8_1208068#101 Alopochen aegyptiaca  20        53.32081  6.192341
#> 10  KE.8_1208068#89 Alopochen aegyptiaca  5         53.32081  6.192341
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Red list
Using the `red_list` filter you can search for records of near threatened
mammals.

```r
finbif_occurrence("mammals", filter = list(red_list_status = "NT"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1883
#> A data.frame [10 x 12]
#>             record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1      JX.1172081#680 Rangifer tarandus f…  5         64.28951  29.15453
#> 2  HR.3211/65002184-U Rangifer tarandus f…  1         63.1      23.9    
#> 3      JX.1172081#134 Rangifer tarandus f…  3         64.10893  29.48419
#> 4       JX.1161996#91 Rangifer tarandus f…  4         64.33462  30.10569
#> 5        JX.1168245#4 Rangifer tarandus f…  5         63.31715  25.30074
#> 6  HR.3211/61379553-U Rangifer tarandus f…  1         63.55     23.75   
#> 7  HR.3211/58578975-U                 <NA>  1         65.83274  30.05538
#> 8  HR.3211/56410884-U Rangifer tarandus f…  1         61.85     23.55   
#> 9  HR.3211/56416254-U Rangifer tarandus f…  1               NA        NA
#> 10 HR.3211/56742224-U Rangifer tarandus f…  1         63.25     24.75   
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Finnish occurrence
Many taxa in the FinBIF database have been given an "Finnish occurrence status"
and this status can be used to filter records.

```r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 291233
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1    HR.3211/65472829-U Dromius quadrimacul…  1         60.15249  24.95254
#> 2         JX.1176173#10  Conistra rubiginosa  19        60.45842  22.17823
#> 3         JX.1175000#23 Subcoccinella vigin…  1         61.35822  28.47772
#> 4    HR.3211/64917225-U     Anthocomus rufus  1         60.20888  24.99462
#> 5         JX.1175007#13  Conistra rubiginosa  78        60.45842  22.17823
#> 6         JX.1175223#10      Acleris umbrana  1         62.80743  30.06103
#> 7         JX.1173580#10 Lithophane ornitopus  1         60.05748  22.49088
#> 8  KE.176/5fa43d58d5de… Cleorodes lichenari…  1         60.11788  20.256  
#> 9          JX.1172678#4 Ectoedemia intimella  1         62.54624  28.92781
#> 10        JX.1173664#16  Conistra rubiginosa  62        60.45842  22.17823
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also us the negation of the `finnish_occurrence_status` to filter out
records of that have a given occurrence status. For example, you can get
records of bird species that are not considered to have stable populations in
Finland with the following filter.

```r
finbif_occurrence(
  "Birds",
  filter = c(finnish_occurrence_status_neg = "stable", taxon_rank = "species")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 115183
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1          JX.1176146#4      Anser albifrons  1         60.6286   26.19815
#> 2        JX.1175321#165   Cygnus columbianus  1         60.90204  26.16786
#> 3    HR.3211/64595796-U          Upupa epops  1         60.5      26.7    
#> 4          JX.1174384#4           Aix sponsa  1         60.18447  23.93021
#> 5          JX.1174062#7   Cygnus columbianus  1         60.71324  25.94479
#> 6        JX.1173669#191 Phalaropus fulicari…  1         61.99952  21.3029 
#> 7    HR.3211/64298655-U          Upupa epops  1         60.41978  21.83083
#> 8  KE.176/5fa2dd70d5de…          Upupa epops  1         62.73651  22.51383
#> 9         JX.1172250#11     Aix galericulata  1         60.37831  23.56202
#> 10         JX.1172182#4      Anser albifrons  2         60.94112  26.51525
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```
