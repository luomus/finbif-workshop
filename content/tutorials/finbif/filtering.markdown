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
#> Records available: 32673736
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Regulus regulus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 2   Emberiza citrinella         1  61.10426  21.56173 2020-03-10 07:50:00
#> 3          Corvus corax         1  61.10426  21.56173 2020-03-10 07:50:00
#> 4         Cygnus cygnus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 5         Turdus merula         3  61.10426  21.56173 2020-03-10 07:50:00
#> 6  Plectrophenax nival…         1  61.10426  21.56173 2020-03-10 07:50:00
#> 7   Cyanistes caeruleus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 8           Parus major         3  61.10426  21.56173 2020-03-10 07:50:00
#> 9  Lophophanes cristat…         1  61.10426  21.56173 2020-03-10 07:50:00
#> 10             Acanthis         1  61.10426  21.56173 2020-03-10 07:50:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 27034696
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Regulus regulus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 2   Emberiza citrinella         1  61.10426  21.56173 2020-03-10 07:50:00
#> 3          Corvus corax         1  61.10426  21.56173 2020-03-10 07:50:00
#> 4         Cygnus cygnus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 5         Turdus merula         3  61.10426  21.56173 2020-03-10 07:50:00
#> 6  Plectrophenax nival…         1  61.10426  21.56173 2020-03-10 07:50:00
#> 7   Cyanistes caeruleus         1  61.10426  21.56173 2020-03-10 07:50:00
#> 8           Parus major         3  61.10426  21.56173 2020-03-10 07:50:00
#> 9  Lophophanes cristat…         1  61.10426  21.56173 2020-03-10 07:50:00
#> 10             Acanthis         1  61.10426  21.56173 2020-03-10 07:50:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 8037
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Clavulinopsis luteo…         1  60.43100  22.28100 2019-12-31 12:00:00
#> 2            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 3      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 5    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 6             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 8   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 9          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 10    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 347883
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Clavulinopsis luteo…         1  60.43100  22.28100 2019-12-31 12:00:00
#> 2            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 3      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 5    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 6             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 8   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 9          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 10    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 1487757
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Pica pica         2  61.43119  24.92867 2020-02-20 07:45:00
#> 2          Picus canus         3  61.43119  24.92867 2020-02-20 07:45:00
#> 3      Regulus regulus        12  61.43119  24.92867 2020-02-20 07:45:00
#> 4     Poecile montanus        18  61.43119  24.92867 2020-02-20 07:45:00
#> 5  Emberiza citrinella         1  61.43119  24.92867 2020-02-20 07:45:00
#> 6         Corvus corax         3  61.43119  24.92867 2020-02-20 07:45:00
#> 7      Cinclus cinclus         1  61.43119  24.92867 2020-02-20 07:45:00
#> 8       Periparus ater         3  61.43119  24.92867 2020-02-20 07:45:00
#> 9                Loxia         3  61.43119  24.92867 2020-02-20 07:45:00
#> 10   Dendrocopos major        73  61.43119  24.92867 2020-02-20 07:45:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

## Data quality
Not all data in FinBIF is created equal. Often it will be desirable to use
`{finbif}`'s data quality filters. The package documentation outlines each
quality filter in detail.

To restrict occurrence records to the highest quality level you can use the
following set of filters.

```r
strict <- c(
  collection_reliability = 5, coordinates_uncertainty_max = 1,
  taxon_reliability = "reliable"
)
```
These filters will limit the occurrence records to those belonging to the most
reliable collections, have the least coordinate uncertainty (most precise
location data), and have reliable taxonomic identifications.

At the other end of the spectrum, you can also allow all records regardless of
quality with the following filter.

```r
permissive <- c(quality_issues = "both")
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
#>     307679   34751933
```

## Collections
You can filter by collection using the collection ID, the collection name or
the abbreviated collection name (if available).

```r
finbif_occurrence(filter = c(collection = "iNaturalist"), count_only = TRUE)
```

```{.language-r}
#> [1] 15716
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
#> [1] 8153033
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
#> Records available: 30493
#> A data.frame [10 x 30]
#>     scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Zootoca vivipara         1  60.93303  26.84106 2020-03-08 12:00:00
#> 2  Zootoca vivipara         1  60.60121  21.67021 2020-02-28 12:00:00
#> 3   Anguis fragilis         1  59.96766  24.39325 2020-02-22 12:00:00
#> 4   Anguis fragilis         1  62.25426  25.13755 2020-02-21 12:00:00
#> 5  Zootoca vivipara         1  60.26828  24.89337 2020-02-17 12:00:00
#> 6         Bufo bufo         1  60.23152  24.98346 2020-01-15 18:00:00
#> 7   Anguis fragilis         1  60.23968  25.79487 2020-01-04 18:00:00
#> 8         Bufo bufo         1  61.08603  26.86767 2020-01-03 14:53:00
#> 9        Lacertidae         1  28.14624 -16.43370 2019-12-04 13:00:00
#> 10       Lacertidae         1  28.13532 -16.44389 2019-12-04 13:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 437
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Alopochen aegyptiaca         3  52.16081  4.485534 2019-10-23 13:00:00
#> 2  Alopochen aegyptiaca         4  53.36759  6.191796 2018-10-26 11:15:00
#> 3  Alopochen aegyptiaca         6  53.37574  6.207861 2018-10-23 08:30:00
#> 4  Alopochen aegyptiaca        30  52.33990  5.069133 2018-10-22 10:45:00
#> 5  Alopochen aegyptiaca        36  51.74641  4.535283 2018-10-21 13:00:00
#> 6  Alopochen aegyptiaca         3  51.74641  4.535283 2018-10-21 13:00:00
#> 7  Alopochen aegyptiaca         2  51.90871  4.532580 2018-10-20 12:10:00
#> 8  Alopochen aegyptiaca         2  53.19242  5.437417 2017-10-24 11:06:00
#> 9  Alopochen aegyptiaca        20  53.32081  6.192341 2017-10-23 12:15:00
#> 10 Alopochen aegyptiaca         5  53.32081  6.192341 2017-10-23 12:15:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Red list
Using the `red_list` filter you can search for records of near threatened
mammals.

```r
finbif_occurrence("mammals", filter = list(red_list_status = "NT"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1650
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Pusa hispida botnica         1  64.66837  24.40488 2020-03-07 12:00:00
#> 2  Rangifer tarandus f…         5  63.83774  29.16123 2020-02-29 09:18:00
#> 3  Rangifer tarandus f…         4  64.42648  29.11431 2019-10-20 12:00:00
#> 4  Rangifer tarandus f…         1  64.09919  29.40356 2019-09-23 12:00:00
#> 5  Rangifer tarandus f…         1  63.79309  29.51080 2019-09-13 12:00:00
#> 6  Rangifer tarandus f…         1  63.93649  29.59252 2019-07-26 12:00:00
#> 7  Rangifer tarandus f…         2  63.27123  25.35634 2019-06-28 12:00:00
#> 8  Rangifer tarandus f…         1  63.26554  25.36645 2019-06-28 12:00:00
#> 9  Rangifer tarandus f…         4  63.03293  24.32905 2019-06-13 12:00:00
#> 10 Rangifer tarandus f…         1  64.32293  26.69975 2019-05-27 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Finnish occurrence
Many taxa in the FinBIF database have been given an "Finnish occurrence status"
and this status can be used to filter records.

```r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 260312
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Agriopis marginaria         7  60.24385  24.74891 2020-03-09 12:00:00
#> 2  Coleophora binderel…         1  62.23735  27.42594 2020-03-06 12:00:00
#> 3   Coleophora violacea         1  62.23735  27.42594 2020-03-06 12:00:00
#> 4   Galerucella pusilla         1  61.71399  29.39042 2020-03-03 16:12:00
#> 5      Scymnus limbatus         1  60.83753  26.72020 2020-03-01 12:00:00
#> 6  Olisthopus rotundat…         1  60.35368  22.36139 2020-02-24 12:00:00
#> 7  Dromius quadrimacul…         1  60.29779  22.40343 2020-02-22 12:00:00
#> 8  Otiorhynchus sulcat…         1  60.82156  21.57260 2020-02-20 12:00:00
#> 9  Dromius quadrimacul…         1  60.29790  22.39917 2020-02-20 12:00:00
#> 10 Dromius quadrimacul…         1  60.29713  22.39969 2020-02-20 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
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
#> Records available: 104618
#> A data.frame [10 x 30]
#>      scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Anser albifrons        37  60.44720  24.22434 2020-03-08 06:40:00
#> 2    Anser albifrons         5  60.21013  25.17325 2020-03-07 08:15:00
#> 3    Anser albifrons         4  60.58187  21.83153 2020-03-07 07:10:00
#> 4    Anser albifrons         8  60.20768  23.99499 2020-03-07 07:20:00
#> 5    Anser albifrons         2  60.88855  26.12326 2020-03-07 12:00:00
#> 6    Anser albifrons         2  59.90500  23.11641 2020-03-06 07:02:00
#> 7    Anser albifrons         1  60.41835  22.11738 2020-03-06 08:00:00
#> 8    Anser albifrons         1  60.05221  24.25531 2020-03-06 07:10:00
#> 9    Anser albifrons         7  60.76204  23.23494 2020-03-06 09:20:00
#> 10 Larus hyperboreus         1  63.81115  23.03631 2020-03-01 08:45:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
