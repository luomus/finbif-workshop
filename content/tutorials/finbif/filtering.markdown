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

```
#> Records downloaded: 10
#> Records available: 43524543
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.3211/148814912-U            Betula L.        NA  66.5783   26.01684
#> 2  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 3  …HR.3211/148815015-U Carduelis spinus (L…        NA  61.21254  21.74742
#> 4  …HR.3211/148814252-U Parus major Linnaeu…        NA  60.17131  24.93085
#> 5  …HR.3211/148814253-U Passer domesticus (…        NA  60.17131  24.93085
#> 6  …HR.3211/148812940-U Sphagnum capillifol…        NA  60.43821  22.37334
#> 7  …HR.3211/148813130-U Trichaptum abietinu…        NA  60.43727  22.37443
#> 8  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 9  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 10        …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> ...with 0 more record and 7 more variables:
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

```
#> Records downloaded: 10
#> Records available: 22
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …tun.fi/KE.67/99796… Alca torda Linnaeus…  1         60        20      
#> 2  …id.luomus.fi/MY.13… Turdus merula Linna…        NA  60        20      
#> 3  …tun.fi/KE.67/90463… Somateria mollissim…  1         60        20      
#> 4  …tun.fi/KE.67/90840… Larus argentatus Po…  1         60        20      
#> 5  …tun.fi/KE.67/90231… Larus marinus Linna…  1         60        20      
#> 6  …tun.fi/KE.67/90224… Larus marinus Linna…  1         60        20      
#> 7  …tun.fi/KE.67/90842… Larus argentatus Po…  1         60        20      
#> 8  …tun.fi/KE.67/93902… Larus ridibundus (L…  1         60        20      
#> 9  …tun.fi/KE.67/23051… Alca torda Linnaeus…  1         60        20      
#> 10 …tun.fi/KE.67/77435… Cepphus grylle (Lin…  1         60        20      
#> ...with 0 more record and 7 more variables:
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

```
#> Records downloaded: 10
#> Records available: 20092
#> A data.frame [10 x 12]
#>         record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44286930_Unit Cyanistes caeruleus…  6         60.25655  21.38695
#> 2  …44309720_Unit Corvus monedula Lin…        NA  61.25934  22.36198
#> 3  …54618625_Unit Turdus merula Linna…  12        60.27545  24.83069
#> 4  …44368562_Unit Buteo buteo (Linnae…  1         60.39103  23.57326
#> 5  …45418881_Unit Pica pica (Linnaeus…  1         60.2301   24.01585
#> 6  …54624981_Unit Turdus merula Linna…  2         60.26978  24.86533
#> 7  …44304786_Unit Bucephala clangula …  1         61.58844  21.46563
#> 8  …44304775_Unit Larus marinus Linna…  3         61.58844  21.46563
#> 9  …44317298_Unit Larus canus Linnaeu…  1         64.69889  24.46876
#> 10 …44319650_Unit Cyanistes caeruleus…  1         61.25854  22.34658
#> ...with 0 more record and 7 more variables:
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

```
#> Records downloaded: 10
#> Records available: 853743
#> A data.frame [10 x 12]
#>         record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44286930_Unit Cyanistes caeruleus…  6         60.25655  21.38695
#> 2  …44309720_Unit Corvus monedula Lin…        NA  61.25934  22.36198
#> 3  …54618625_Unit Turdus merula Linna…  12        60.27545  24.83069
#> 4  …44368562_Unit Buteo buteo (Linnae…  1         60.39103  23.57326
#> 5  …45418881_Unit Pica pica (Linnaeus…  1         60.2301   24.01585
#> 6  …54624981_Unit Turdus merula Linna…  2         60.26978  24.86533
#> 7  …44304786_Unit Bucephala clangula …  1         61.58844  21.46563
#> 8  …44304775_Unit Larus marinus Linna…  3         61.58844  21.46563
#> 9  …44317298_Unit Larus canus Linnaeu…  1         64.69889  24.46876
#> 10 …44319650_Unit Cyanistes caeruleus…  1         61.25854  22.34658
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also filter by time of year (i.e., a date range across all years) using
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

```
#> Records downloaded: 10
#> Records available: 1476175
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.3211/148814912-U            Betula L.        NA  66.5783   26.01684
#> 2  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 3  …HR.3211/148815015-U Carduelis spinus (L…        NA  61.21254  21.74742
#> 4  …HR.3211/148814252-U Parus major Linnaeu…        NA  60.17131  24.93085
#> 5  …HR.3211/148814253-U Passer domesticus (…        NA  60.17131  24.93085
#> 6  …HR.3211/148812940-U Sphagnum capillifol…        NA  60.43821  22.37334
#> 7  …HR.3211/148813130-U Trichaptum abietinu…        NA  60.43727  22.37443
#> 8  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 9  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 10        …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> ...with 0 more record and 7 more variables:
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

```r
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

```r
finbif_occurrence(filter = list(strict, permissive), count_only = TRUE)
```

```
#> [[1]]
#> [1] 121
#> 
#> [[2]]
#> [1] 46086500
```

## Collections
You can filter by collection using the collection ID, the collection name or
the abbreviated collection name (if available).

```r
finbif_occurrence(
  filter = c(collection = "iNaturalist Suomi Finland"), count_only = TRUE
)
```

```
#> [1] 504372
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

```
#> [1] 45893880
```

## Informal groups
Many informal taxonomic groups align with formal taxonomic groups (e.g., birds)
but some, such as "Reptiles & amphibians" do not, making the `informal_group`
potential useful in some circumstances.

```r
finbif_occurrence(filter = list(informal_groups = "Reptiles and amphibians"))
```

```
#> Records downloaded: 10
#> Records available: 46918
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.3211/146607558-U Bufo bufo (Linnaeus…        NA  60.29014  24.60482
#> 2  …HR.3211/146520576-U Bufo bufo (Linnaeus…        NA  60.61056  25.22402
#> 3  …HR.3211/141883071-U Lissotriton vulgari…        NA  60.39002  23.11718
#> 4  …HR.3211/141783787-U Bufo bufo (Linnaeus…        NA  61.05236  25.04516
#> 5  …HR.3211/141784215-U Rana temporaria Lin…        NA  61.05141  25.04307
#> 6  …KE.176/63714108d5d… Anguis colchica (No…  1         61.3986   21.99607
#> 7  …KE.176/636e7ca7d5d… Anguis colchica (No…  1         61.29448  27.58093
#> 8  …HR.3211/141648529-U Rana temporaria Lin…        NA  60.22848  24.91664
#> 9  …HR.3211/141598361-U Anguis colchica (No…        NA  60.64372  24.88825
#> 10 …HR.3211/142675274-U Lissotriton vulgari…        NA  63.6829   22.78389
#> ...with 0 more record and 7 more variables:
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
finbif_occurrence("birds", filter = list(regulatory_status = "EU_INVSV"))
```

```
#> Records downloaded: 10
#> Records available: 469
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62b1ad90d5d… Oxyura jamaicensis …  7         61.66207  23.57706
#> 2        …JX.1045316#34 Alopochen aegyptiac…  3         52.16081  4.485534
#> 3        …JX.138840#123 Alopochen aegyptiac…  4         53.36759  6.191796
#> 4        …JX.139978#214 Alopochen aegyptiac…  6         53.37574  6.207861
#> 5         …JX.139710#17 Alopochen aegyptiac…  30        52.3399   5.069133
#> 6         …JX.139645#57 Alopochen aegyptiac…  36        51.74641  4.535283
#> 7         …JX.139645#10 Alopochen aegyptiac…  3         51.74641  4.535283
#> 8         …JX.139442#16 Alopochen aegyptiac…  2         51.90871  4.53258 
#> 9      …KE.8_1208123#15 Alopochen aegyptiac…  2         53.19242  5.437417
#> 10     …KE.8_1208068#89 Alopochen aegyptiac…  5         53.32081  6.192341
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Red list
Using the `red_list` filter you can search for records of near threatened
mammals.

```r
finbif_occurrence("mammals", filter = list(red_list_status = "NT"))
```

```
#> Records downloaded: 10
#> Records available: 42448
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1515508#39 Rangifer tarandus f…        NA  64.22363  28.96249
#> 2  …HR.3211/145844443-U Rangifer tarandus f…        NA  64.1      28.5    
#> 3        …JX.1509526#13 Rangifer tarandus f…  9         64.28961  29.15437
#> 4        …JX.1509526#16 Rangifer tarandus f…  17        64.18418  29.21215
#> 5         …JX.1509182#3 Rangifer tarandus f…  4         64.13615  26.24839
#> 6  …HR.3211/142946329-U Rangifer tarandus f…        NA  63.5      23.9    
#> 7       …JX.1503045#165 Rangifer tarandus f…  5         62.13633  22.14217
#> 8         …JX.1505392#3 Rangifer tarandus f…  4         63.40215  24.27285
#> 9  …HR.3211/140674988-U Pusa hispida botnic…        NA  60.03843  24.68483
#> 10        …JX.1501060#3 Rangifer tarandus f…  3         64.09919  29.40356
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Finnish occurrence
Many taxa in the FinBIF database have been given an "Finnish occurrence status"
and this status can be used to filter records.

```r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```
#> Records downloaded: 10
#> Records available: 381879
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1529644#5 Acrocercops brongni…  1         60.44273  22.19863
#> 2         …JX.1529635#7 Conistra rubiginosa…  14        60.45842  22.17798
#> 3  …HR.3211/148388028-U Hypena rostralis (L…        NA  63.02717  27.25028
#> 4         …JX.1528876#3 Conistra rubiginosa…  2         60.45842  22.17798
#> 5         …JX.1525457#3 Agonopterix hyperic…  1         61.87891  28.85772
#> 6  …HR.3211/147770103-U Acrocercops brongni…        NA  60.45174  22.26663
#> 7  …KE.176/63d84820d5d… Semanotus undatus (…  1         60.47044  22.17258
#> 8         …JX.1521830#3 Conistra rubiginosa…  3         60.45842  22.17798
#> 9  …KE.176/63c6f5e2d5d… Anthrenus scrophula…  2         61.1886   28.76845
#> 10 …KE.176/63c6f5ded5d… Anthrenus scrophula…  2         61.1818   28.84525
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also use the negation of the `finnish_occurrence_status` to filter out
records of that have a given occurrence status. For example, you can get
records of bird species that are not considered to have stable populations in
Finland with the following filter.

```r
finbif_occurrence(
  "Birds",
  filter = c(finnish_occurrence_status_neg = "stable", taxon_rank = "species")
)
```

```
#> Records downloaded: 10
#> Records available: 91637
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.4412/63d719d025… Eremophila alpestri…        NA  60.3468   24.73263
#> 2       …JX.1518212#171 Rissa tridactyla (L…  1         60.03829  20.04897
#> 3       …JX.1515660#173 Larus cachinnans Pa…  1         60.4916   22.33665
#> 4        …JX.1515115#18 Regulus ignicapilla…  1         60.42676  22.20634
#> 5  …HR.3211/142139077-U Branta bernicla (Li…        NA  60.2711   24.9525 
#> 6         …JX.1505366#3 Oenanthe deserti (T…  1         59.82661  23.12009
#> 7         …JX.1505318#3 Oenanthe deserti (T…  1         59.82659  23.12375
#> 8  …HR.3211/141648812-U Anser albifrons (Sc…        NA  60.22061  25.02178
#> 9       …JX.1504012#167 Phalaropus fulicari…  1         60.94753  22.88899
#> 10      …JX.1502659#165 Upupa epops Linnaeu…  1         65.776    24.55344
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```
