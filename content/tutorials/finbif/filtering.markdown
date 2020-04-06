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
#> Records available: 32770995
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Mompha sturnipennel…  1         62.23735  27.42594 2020-04-06 12:00:00
#> 2                  <NA>  1         60.19302  23.41405 2020-04-06 12:00:00
#> 3      Sturnus vulgaris  1         60.7171   27.2106  2020-04-06 12:00:00
#> 4     Tussilago farfara  1         63.74834  27.64843 2020-04-06 12:00:00
#> 5             Aglais io  1         61.50572  23.82138 2020-04-05 12:00:00
#> 6     Nymphalis antiopa  1         61.52834  24.86208 2020-04-05 12:00:00
#> 7    Rabocerus gabrieli  1         63.83328  23.0308  2020-04-05 12:00:00
#> 8         Vulpes vulpes  1         60.11628  23.47399 2020-04-05 12:00:00
#> 9      Hepatica nobilis  3         60.11204  23.5322  2020-04-05 12:00:00
#> 10       Bombus lucorum  1         60.11204  23.5322  2020-04-05 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> Records available: 27121414
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Mompha sturnipennel…  1         62.23735  27.42594 2020-04-06 12:00:00
#> 2                  <NA>  1         60.19302  23.41405 2020-04-06 12:00:00
#> 3      Sturnus vulgaris  1         60.7171   27.2106  2020-04-06 12:00:00
#> 4     Tussilago farfara  1         63.74834  27.64843 2020-04-06 12:00:00
#> 5             Aglais io  1         61.50572  23.82138 2020-04-05 12:00:00
#> 6     Nymphalis antiopa  1         61.52834  24.86208 2020-04-05 12:00:00
#> 7    Rabocerus gabrieli  1         63.83328  23.0308  2020-04-05 12:00:00
#> 8         Vulpes vulpes  1         60.11628  23.47399 2020-04-05 12:00:00
#> 9      Hepatica nobilis  3         60.11204  23.5322  2020-04-05 12:00:00
#> 10       Bombus lucorum  1         60.11204  23.5322  2020-04-05 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> Records available: 8074
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Flammulina finlandi…  1         60.3753   23.16409 2019-12-31 12:00:00
#> 2     Exidia glandulosa  1         60.37529  23.16411 2019-12-31 12:00:00
#> 3  Hypocreopsis lichen…  10        60.37529  23.16411 2019-12-31 12:00:00
#> 4  Clavulinopsis luteo…  1         60.431    22.281   2019-12-31 12:00:00
#> 5            Flammulina  10        60.39362  25.67044 2019-12-31 12:00:00
#> 6      Panellus ringens  1         63.068    21.6902  2019-12-31 12:00:00
#> 7  Basidioradulum radu…  1         63.068    21.6902  2019-12-31 12:00:00
#> 8    Sarcosoma globosum  1         60.28506  21.98599 2019-12-31 12:00:00
#> 9             Pica pica  3         62.21189  21.66492 2019-12-31 09:54:00
#> 10     Poecile montanus  4         62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> Records available: 379860
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Flammulina finlandi…  1         60.3753   23.16409 2019-12-31 12:00:00
#> 2     Exidia glandulosa  1         60.37529  23.16411 2019-12-31 12:00:00
#> 3  Hypocreopsis lichen…  10        60.37529  23.16411 2019-12-31 12:00:00
#> 4  Clavulinopsis luteo…  1         60.431    22.281   2019-12-31 12:00:00
#> 5            Flammulina  10        60.39362  25.67044 2019-12-31 12:00:00
#> 6      Panellus ringens  1         63.068    21.6902  2019-12-31 12:00:00
#> 7  Basidioradulum radu…  1         63.068    21.6902  2019-12-31 12:00:00
#> 8    Sarcosoma globosum  1         60.28506  21.98599 2019-12-31 12:00:00
#> 9             Pica pica  3         62.21189  21.66492 2019-12-31 09:54:00
#> 10     Poecile montanus  4         62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> Records available: 1488420
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1         Cygnus cygnus  1         61.082    27.78355 2020-02-20 12:00:00
#> 2         Cygnus cygnus  1         61.437    23.031   2020-02-20 12:00:00
#> 3         Cygnus cygnus  1         61.0722   25.70648 2020-02-20 12:00:00
#> 4  Phragmatobia fuligi…  1         64.26197  27.92685 2020-02-20 12:00:00
#> 5  Xeromphalina campan…  1         60.401    22.393   2020-02-20 12:00:00
#> 6     Tussilago farfara  1         61.454    22.116   2020-02-20 12:00:00
#> 7             Pica pica  2         61.43119  24.92867 2020-02-20 07:45:00
#> 8           Picus canus  3         61.43119  24.92867 2020-02-20 07:45:00
#> 9       Regulus regulus  12        61.43119  24.92867 2020-02-20 07:45:00
#> 10     Poecile montanus  18        61.43119  24.92867 2020-02-20 07:45:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#>     311202   34855912
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
#> [1] 8158569
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
#> Records available: 30576
#> A data.frame [10 x 10]
#>     scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Rana temporaria  1         60.2365   24.99785 2020-04-05 12:00:00
#> 2  Zootoca vivipara  1         60.0558   24.24036 2020-04-04 12:00:00
#> 3  Zootoca vivipara  2         61.39162  24.63277 2020-03-31 13:00:00
#> 4  Zootoca vivipara  1         60.393    25.744   2020-03-28 12:00:00
#> 5  Zootoca vivipara  1         60.4338   26.68982 2020-03-28 12:00:00
#> 6  Zootoca vivipara  1         60.4338   26.68982 2020-03-28 12:00:00
#> 7  Zootoca vivipara  1         60.55858  24.22039 2020-03-28 12:00:00
#> 8  Zootoca vivipara  1         60.55858  24.22039 2020-03-28 12:00:00
#> 9  Zootoca vivipara  1         60.15582  24.18372 2020-03-28 12:00:00
#> 10  Rana temporaria  1         60.19852  25.0141  2020-03-28 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Alopochen aegyptiaca  3         52.16081  4.485534 2019-10-23 13:00:00
#> 2  Alopochen aegyptiaca  4         53.36759  6.191796 2018-10-26 11:15:00
#> 3  Alopochen aegyptiaca  6         53.37574  6.207861 2018-10-23 08:30:00
#> 4  Alopochen aegyptiaca  30        52.3399   5.069133 2018-10-22 10:45:00
#> 5  Alopochen aegyptiaca  36        51.74641  4.535283 2018-10-21 13:00:00
#> 6  Alopochen aegyptiaca  3         51.74641  4.535283 2018-10-21 13:00:00
#> 7  Alopochen aegyptiaca  2         51.90871  4.53258  2018-10-20 12:10:00
#> 8  Alopochen aegyptiaca  2         53.19242  5.437417 2017-10-24 11:06:00
#> 9  Alopochen aegyptiaca  20        53.32081  6.192341 2017-10-23 12:15:00
#> 10 Alopochen aegyptiaca  5         53.32081  6.192341 2017-10-23 12:15:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Rangifer tarandus f…  7         63.11867  24.12289 2020-03-28 12:00:00
#> 2  Pusa hispida botnica  1         64.66837  24.40488 2020-03-07 12:00:00
#> 3  Rangifer tarandus f…  5         63.83774  29.16123 2020-02-29 09:18:00
#> 4  Rangifer tarandus f…  4         64.42648  29.11431 2019-10-20 12:00:00
#> 5  Rangifer tarandus f…  1         64.09919  29.40356 2019-09-23 12:00:00
#> 6  Rangifer tarandus f…  1         63.79309  29.5108  2019-09-13 12:00:00
#> 7  Rangifer tarandus f…  1         63.93649  29.59252 2019-07-26 12:00:00
#> 8  Rangifer tarandus f…  2         63.27123  25.35634 2019-06-28 12:00:00
#> 9  Rangifer tarandus f…  1         63.26554  25.36645 2019-06-28 12:00:00
#> 10 Rangifer tarandus f…  4         63.03293  24.32905 2019-06-13 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

### Finnish occurrence
Many taxa in the FinBIF database have been given an "Finnish occurrence status"
and this status can be used to filter records.

```r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 260804
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Uloma rufa  2         61.70041  29.39708 2020-04-05 18:31:00
#> 2  Lithophane ornitopus  1         60.05748  22.49088 2020-04-05 12:00:00
#> 3    Oenopia conglobata  1         61.69288  29.68773 2020-04-03 12:00:00
#> 4      Archiearis notha  3         60.25712  24.73908 2020-03-28 12:00:00
#> 5        Thecla betulae  4         60.33962  25.23897 2020-03-28 12:00:00
#> 6   Agriopis marginaria  20        60.24476  24.74196 2020-03-28 12:00:00
#> 7  Subcoccinella vigin…  1         59.89182  22.5213  2020-03-27 12:00:00
#> 8  Chilocorus bipustul…  1         59.86901  22.46867 2020-03-27 12:00:00
#> 9   Conistra rubiginosa  7         60.12303  20.25994 2020-03-26 12:00:00
#> 10 Eriogaster lanestris  1         60.12303  20.25994 2020-03-26 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> Records available: 104637
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1     Branta ruficollis  1         60.60374  26.49053 2020-04-02 12:00:00
#> 2       Branta bernicla  2         60.83308  26.2358  2020-04-01 12:00:00
#> 3       Anser albifrons  50        60.90404  26.33529 2020-04-01 12:00:00
#> 4       Anser albifrons  1         60.18324  24.66028 2020-03-28 06:30:00
#> 5       Anser albifrons  5         60.14681  24.92787 2020-03-26 07:50:00
#> 6       Anser albifrons  1300      60.85064  26.29335 2020-03-25 12:00:00
#> 7  Anser brachyrhynchus  3         60.84962  26.29034 2020-03-25 12:00:00
#> 8       Anser albifrons  2000      60.7876   26.09082 2020-03-23 12:00:00
#> 9    Cygnus columbianus  4         60.95256  26.02778 2020-03-20 12:00:00
#> 10 Anser brachyrhynchus  1         60.7876   26.09082 2020-03-17 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```
