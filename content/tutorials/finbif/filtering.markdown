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
#> Records available: 32654320
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1             Grus grus         1  60.59627  24.84059 2020-03-05 12:00:00
#> 2         Cygnus cygnus         1  60.90278  22.71329 2020-03-05 12:00:00
#> 3   Acanthis hornemanni        15  61.24887  26.22156 2020-03-05 12:00:00
#> 4  Cladonia ochrochlora         2  60.66508  23.60832 2020-03-04 12:00:00
#> 5  Xanthoparmelia sten…         1  60.66508  23.60832 2020-03-04 12:00:00
#> 6    Parmelia saxatilis        10  60.43472  26.85182 2020-03-04 12:00:00
#> 7             Pica pica        19  65.67320  24.54981 2020-03-04 08:00:00
#> 8       Regulus regulus         3  65.67320  24.54981 2020-03-04 08:00:00
#> 9      Poecile montanus         1  65.67320  24.54981 2020-03-04 08:00:00
#> 10        Cygnus cygnus         5  65.67320  24.54981 2020-03-04 08:00:00
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
#> Records available: 27016956
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1             Grus grus         1  60.59627  24.84059 2020-03-05 12:00:00
#> 2         Cygnus cygnus         1  60.90278  22.71329 2020-03-05 12:00:00
#> 3   Acanthis hornemanni        15  61.24887  26.22156 2020-03-05 12:00:00
#> 4  Cladonia ochrochlora         2  60.66508  23.60832 2020-03-04 12:00:00
#> 5  Xanthoparmelia sten…         1  60.66508  23.60832 2020-03-04 12:00:00
#> 6    Parmelia saxatilis        10  60.43472  26.85182 2020-03-04 12:00:00
#> 7             Pica pica        19  65.67320  24.54981 2020-03-04 08:00:00
#> 8       Regulus regulus         3  65.67320  24.54981 2020-03-04 08:00:00
#> 9      Poecile montanus         1  65.67320  24.54981 2020-03-04 08:00:00
#> 10        Cygnus cygnus         5  65.67320  24.54981 2020-03-04 08:00:00
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
#> Records available: 7994
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 2      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 3  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 5             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 6      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 7   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 8          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 9     Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> 10      Corvus monedula         2  62.21189  21.66492 2019-12-31 09:54:00
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
#> Records available: 344435
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 2      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 3  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 5             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 6      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 7   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 8          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 9     Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> 10      Corvus monedula         2  62.21189  21.66492 2019-12-31 09:54:00
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
#> Records available: 1487158
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Otiorhynchus sulcat…         1  60.82156  21.57260 2020-02-20 12:00:00
#> 2         Cygnus cygnus         1  61.08200  27.78355 2020-02-20 12:00:00
#> 3     Tussilago farfara         1  60.53359  22.25838 2020-02-20 12:00:00
#> 4     Formica (Formica)         1  60.38138  22.41044 2020-02-20 12:00:00
#> 5           Lutra lutra         1  60.80374  25.81131 2020-02-20 12:00:00
#> 6      Acalypta parvula         1  60.28291  22.40971 2020-02-20 12:00:00
#> 7    Dolycoris baccarum         1  60.28291  22.40971 2020-02-20 12:00:00
#> 8    Dolycoris baccarum         4  60.28291  22.40971 2020-02-20 12:00:00
#> 9       Drymus brunneus         3  60.28291  22.40971 2020-02-20 12:00:00
#> 10     Elasmucha grisea         1  60.28291  22.40971 2020-02-20 12:00:00
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
#>     307637   34731956
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
#> [1] 8149367
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
#> Records available: 30489
#> A data.frame [10 x 30]
#>     scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Zootoca vivipara         1  60.60121  21.67021 2020-02-28 12:00:00
#> 2   Anguis fragilis         1  59.96766  24.39325 2020-02-22 12:00:00
#> 3   Anguis fragilis         1  62.25426  25.13755 2020-02-21 12:00:00
#> 4  Zootoca vivipara         1  60.26828  24.89337 2020-02-17 12:00:00
#> 5         Bufo bufo         1  60.23152  24.98346 2020-01-15 18:00:00
#> 6   Anguis fragilis         1  60.23968  25.79487 2020-01-04 18:00:00
#> 7         Bufo bufo         1  61.08603  26.86767 2020-01-03 14:53:00
#> 8        Lacertidae         1  28.14624 -16.43370 2019-12-04 13:00:00
#> 9        Lacertidae         1  28.13532 -16.44389 2019-12-04 13:00:00
#> 10        Bufo bufo         1  60.89002  24.69797 2019-10-18 10:00:00
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
#> Records available: 1648
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Rangifer tarandus f…         5  63.83774  29.16123 2020-02-29 09:18:00
#> 2  Rangifer tarandus f…         4  64.42648  29.11431 2019-10-20 12:00:00
#> 3  Rangifer tarandus f…         1  64.09919  29.40356 2019-09-23 12:00:00
#> 4  Rangifer tarandus f…         1  63.79309  29.51080 2019-09-13 12:00:00
#> 5  Rangifer tarandus f…         1  63.93649  29.59252 2019-07-26 12:00:00
#> 6  Rangifer tarandus f…         2  63.27123  25.35634 2019-06-28 12:00:00
#> 7  Rangifer tarandus f…         1  63.26554  25.36645 2019-06-28 12:00:00
#> 8  Rangifer tarandus f…         4  63.03293  24.32905 2019-06-13 12:00:00
#> 9  Rangifer tarandus f…         1  64.32293  26.69975 2019-05-27 12:00:00
#> 10 Rangifer tarandus f…         1  63.54897  24.54795 2019-05-18 12:00:00
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
#> Records available: 260081
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Galerucella pusilla         1  61.71399  29.39042 2020-03-03 16:12:00
#> 2  Olisthopus rotundat…         1  60.35368  22.36139 2020-02-24 12:00:00
#> 3  Dromius quadrimacul…         1  60.29779  22.40343 2020-02-22 12:00:00
#> 4  Otiorhynchus sulcat…         1  60.82156  21.57260 2020-02-20 12:00:00
#> 5  Dromius quadrimacul…         1  60.29790  22.39917 2020-02-20 12:00:00
#> 6  Dromius quadrimacul…         1  60.29713  22.39969 2020-02-20 12:00:00
#> 7    Hylesinus crenatus         1  60.29713  22.39969 2020-02-20 12:00:00
#> 8   Conistra rubiginosa         4  60.45842  22.17823 2020-02-17 12:00:00
#> 9    Oenopia conglobata         1  61.71205  29.39218 2020-02-13 15:36:00
#> 10   Oenopia conglobata         1  61.71378  29.39089 2020-02-12 18:52:00
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
#> Records available: 104609
#> A data.frame [10 x 30]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Larus hyperboreus         1  63.81115  23.03631 2020-03-01 08:45:00
#> 2       Milvus milvus         1  60.78519  26.07963 2020-02-19 07:00:00
#> 3    Larus glaucoides         1  63.82952  23.03191 2020-02-05 12:00:00
#> 4       Gavia adamsii         1  61.14620  26.72432 2020-02-05 12:00:00
#> 5   Larus hyperboreus         1  63.82944  23.03180 2020-02-04 12:00:00
#> 6    Larus glaucoides         1  63.82939  23.02910 2020-02-03 12:00:00
#> 7   Larus hyperboreus         1  65.05931  25.40096 2020-01-06 11:00:00
#> 8       Milvus milvus         1  60.08416  23.40222 2020-01-06 09:15:00
#> 9  Cygnus columbianus         1  60.15734  24.87389 2020-01-05 09:10:00
#> 10      Gavia adamsii         1  61.15926  28.76690 2020-01-01 09:50:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
