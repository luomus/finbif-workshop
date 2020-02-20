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




```r
?filters
```

## Location

```r
finbif_occurrence(filter = c(country = "Finland"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 32618230
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1          Strobilurus         1  61.57393  23.17713 2020-02-19 22:00:00
#> 2   Phigalia pilosaria         1  60.38352  23.16606 2020-02-18 22:00:00
#> 3          Strix aluco         1  60.97880  26.09086 2020-02-18 22:00:00
#> 4        Milvus milvus         1  60.78519  26.07963 2020-02-19 05:00:00
#> 5          Strix aluco         1  60.98431  26.04420 2020-02-18 22:00:00
#> 6        Schizophyllum        10  60.18082  25.01560 2020-02-18 22:00:00
#> 7  Exidia cartilaginea        10  60.37493  25.73387 2020-02-18 22:00:00
#> 8      Graphis scripta      1000  60.37480  25.73329 2020-02-18 22:00:00
#> 9    Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
#> 10           Culicidae         1  59.89200  22.51700 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(
  filter = list(
    coordinates = list(lat = c(60, 68), lon = c(20, 30), system = "wgs84")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 26987004
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1          Strobilurus         1  61.57393  23.17713 2020-02-19 22:00:00
#> 2   Phigalia pilosaria         1  60.38352  23.16606 2020-02-18 22:00:00
#> 3          Strix aluco         1  60.97880  26.09086 2020-02-18 22:00:00
#> 4        Milvus milvus         1  60.78519  26.07963 2020-02-19 05:00:00
#> 5          Strix aluco         1  60.98431  26.04420 2020-02-18 22:00:00
#> 6        Schizophyllum        10  60.18082  25.01560 2020-02-18 22:00:00
#> 7  Exidia cartilaginea        10  60.37493  25.73387 2020-02-18 22:00:00
#> 8      Graphis scripta      1000  60.37480  25.73329 2020-02-18 22:00:00
#> 9       Dicranum majus         1  62.25868  25.71230 2020-02-18 22:00:00
#> 10  Dicranum polysetum         1  62.25868  25.71230 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

## Dates & times

```r
finbif_occurrence(filter = list(date_range_ym = c("2019-12")))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 7550
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1             Pica pica        26  61.59566  23.35462 2019-12-31 08:05:00
#> 2             Pica pica        31  65.72340  24.62299 2019-12-31 08:00:00
#> 3       Regulus regulus        11  62.91571  27.66064 2019-12-31 07:10:00
#> 4      Poecile montanus         1  62.91571  27.66064 2019-12-31 07:10:00
#> 5  Columba livia domes…        32  65.72340  24.62299 2019-12-31 08:00:00
#> 6  Columba livia domes…         2  61.59566  23.35462 2019-12-31 08:05:00
#> 7           Felis catus         1  61.59566  23.35462 2019-12-31 08:05:00
#> 8        Periparus ater         1  62.91571  27.66064 2019-12-31 07:10:00
#> 9                 Loxia         2  61.59566  23.35462 2019-12-31 08:05:00
#> 10    Dendrocopos major         5  62.91571  27.66064 2019-12-31 07:10:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(
  filter = list(date_range_ymd = c("2019-06-01", "2019-12-31"))
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 334922
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1             Pica pica        26  61.59566  23.35462 2019-12-31 08:05:00
#> 2             Pica pica        31  65.72340  24.62299 2019-12-31 08:00:00
#> 3       Regulus regulus        11  62.91571  27.66064 2019-12-31 07:10:00
#> 4      Poecile montanus         1  62.91571  27.66064 2019-12-31 07:10:00
#> 5  Columba livia domes…        32  65.72340  24.62299 2019-12-31 08:00:00
#> 6  Columba livia domes…         2  61.59566  23.35462 2019-12-31 08:05:00
#> 7           Felis catus         1  61.59566  23.35462 2019-12-31 08:05:00
#> 8        Periparus ater         1  62.91571  27.66064 2019-12-31 07:10:00
#> 9                 Loxia         2  61.59566  23.35462 2019-12-31 08:05:00
#> 10    Dendrocopos major         5  62.91571  27.66064 2019-12-31 07:10:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


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
#> Records available: 1483333
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1          Strobilurus         1  61.57393  23.17713 2020-02-19 22:00:00
#> 2   Phigalia pilosaria         1  60.38352  23.16606 2020-02-18 22:00:00
#> 3          Strix aluco         1  60.97880  26.09086 2020-02-18 22:00:00
#> 4        Milvus milvus         1  60.78519  26.07963 2020-02-19 05:00:00
#> 5          Strix aluco         1  60.98431  26.04420 2020-02-18 22:00:00
#> 6        Schizophyllum        10  60.18082  25.01560 2020-02-18 22:00:00
#> 7  Exidia cartilaginea        10  60.37493  25.73387 2020-02-18 22:00:00
#> 8      Graphis scripta      1000  60.37480  25.73329 2020-02-18 22:00:00
#> 9    Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
#> 10           Culicidae         1  59.89200  22.51700 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

## Data quality

```r
strict <- c(
  collection_reliability = 5, coordinates_uncertainty_max = 1,
  taxon_reliability = "reliable"
)
```


```r
permissive <- list(
  collection_reliability = 1:5, coordinates_uncertainty_max = 10000,
  quality_issues = "both"
)
```


```r
c(
  strict     = finbif_occurrence(filter = strict,     count_only = TRUE),
  permissive = finbif_occurrence(filter = permissive, count_only = TRUE)
)
```

```{.language-r}
#>     strict permissive 
#>     303248   31323061
```

## Collections

```r
finbif_occurrence(
  filter = c(collection = "iNaturalist"), count_only = TRUE
)
```

```{.language-r}
#> [1] 15716
```


```r
finbif_occurrence(
  filter = c(collection = "Notebook, general observations"), count_only = TRUE
)
```

```{.language-r}
#> [1] 680642
```


```r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland", nmin = 10000
)

finbif_occurrence(filter = list(collection = collections), count_only = TRUE)
```

```{.language-r}
#> [1] 8142513
```

## Informal groups

```r
finbif_occurrence(filter = list(informal_group = "Reptiles and amphibians"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 30475
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Zootoca vivipara         1  60.26828  24.89337 2020-02-16 22:00:00
#> 2             Bufo bufo         1  60.23152  24.98346 2020-01-15 16:00:00
#> 3       Anguis fragilis         1  60.23968  25.79487 2020-01-04 16:00:00
#> 4             Bufo bufo         1  61.08603  26.86767 2020-01-03 12:53:00
#> 5            Lacertidae         1  28.14624 -16.43370 2019-12-04 11:00:00
#> 6            Lacertidae         1  28.13532 -16.44389 2019-12-04 11:00:00
#> 7             Bufo bufo         1  60.89002  24.69797 2019-10-18 07:00:00
#> 8             Bufo bufo         1  60.82829  24.58493 2019-10-12 21:00:00
#> 9             Bufo bufo         2  60.83577  21.25200 2019-10-12 21:00:00
#> 10 Lissotriton vulgaris         1  60.14040  24.22113 2019-09-29 21:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(
  filter = list(informal_group = "Birds", administrative_status = "EU_INVSV")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 437
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Alopochen aegyptiaca         3  52.16081  4.485534 2019-10-22 22:00:00
#> 2  Alopochen aegyptiaca         4  53.36759  6.191796 2018-10-26 08:15:00
#> 3  Alopochen aegyptiaca         6  53.37574  6.207861 2018-10-23 05:30:00
#> 4  Alopochen aegyptiaca        30  52.33990  5.069133 2018-10-22 07:45:00
#> 5  Alopochen aegyptiaca        36  51.74641  4.535283 2018-10-21 10:00:00
#> 6  Alopochen aegyptiaca         3  51.74641  4.535283 2018-10-21 10:00:00
#> 7  Alopochen aegyptiaca         2  51.90871  4.532580 2018-10-20 09:10:00
#> 8  Alopochen aegyptiaca         2  53.19242  5.437417 2017-10-24 08:06:00
#> 9  Alopochen aegyptiaca        20  53.32081  6.192341 2017-10-23 09:15:00
#> 10 Alopochen aegyptiaca         5  53.32081  6.192341 2017-10-23 09:15:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

## Taxon status

```r
finbif_occurrence(
  filter = list(informal_group = "Mammals", red_list_status = "NT")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1647
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Rangifer tarandus f…         4  64.42648  29.11431 2019-10-19 21:00:00
#> 2  Rangifer tarandus f…         1  64.09919  29.40356 2019-09-22 21:00:00
#> 3  Rangifer tarandus f…         1  63.79309  29.51080 2019-09-12 21:00:00
#> 4  Rangifer tarandus f…         1  63.93649  29.59252 2019-07-25 21:00:00
#> 5  Rangifer tarandus f…         2  63.27123  25.35634 2019-06-27 21:00:00
#> 6  Rangifer tarandus f…         1  63.26554  25.36645 2019-06-27 21:00:00
#> 7  Rangifer tarandus f…         4  63.03293  24.32905 2019-06-12 21:00:00
#> 8  Rangifer tarandus f…         1  64.32293  26.69975 2019-05-26 21:00:00
#> 9  Rangifer tarandus f…         1  63.54897  24.54795 2019-05-17 21:00:00
#> 10 Rangifer tarandus f…         7  64.43140  29.11998 2019-04-27 21:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(filter = c(finnish_occurrence_status = "rare"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 259633
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Conistra rubiginosa         4  60.45842  22.17823 2020-02-16 22:00:00
#> 2    Oenopia conglobata         1  61.71205  29.39218 2020-02-13 13:36:00
#> 3    Oenopia conglobata         1  61.71378  29.39089 2020-02-12 16:52:00
#> 4  Nanomimus circumscr…         1  60.41145  26.60956 2020-02-10 22:00:00
#> 5    Nephus bipunctatus         1  60.41145  26.60956 2020-02-10 22:00:00
#> 6  Calodromius spilotus         2  60.14807  22.29686 2020-02-01 22:00:00
#> 7    Stethorus pusillus         1  60.28865  24.86263 2020-01-29 22:00:00
#> 8  Calodromius spilotus         2  60.11620  24.63514 2020-01-25 22:00:00
#> 9  Dromius quadrimacul…         1  60.11620  24.63514 2020-01-25 22:00:00
#> 10   Scymnus ferrugatus         1  60.50135  25.94171 2020-01-25 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(
  "Birds",
  filter = c(finnish_occurrence_status_neg = "stable", taxon_rank = "species")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 104634
#> A data.frame [10 x 30]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Milvus milvus         1  60.78519  26.07963 2020-02-19 05:00:00
#> 2       Gavia adamsii         1  61.14620  26.72432 2020-02-04 22:00:00
#> 3    Larus glaucoides         1  63.82952  23.03191 2020-02-04 22:00:00
#> 4   Larus hyperboreus         1  63.82944  23.03180 2020-02-03 22:00:00
#> 5    Larus glaucoides         1  63.82939  23.02910 2020-02-02 22:00:00
#> 6       Milvus milvus         1  60.08416  23.40222 2020-01-06 07:15:00
#> 7  Cygnus columbianus         1  60.15734  24.87389 2020-01-05 07:10:00
#> 8       Gavia adamsii         1  61.15926  28.76690 2020-01-01 07:50:00
#> 9   Larus hyperboreus         1  65.07408  25.40821 2019-12-31 08:05:00
#> 10      Bubulcus ibis         1  26.15296 -81.53502 2019-12-27 05:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
