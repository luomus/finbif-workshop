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


```r
finbif_occurrence(filter = c(country = "Finland"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 32615090
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Cortinarius dionysae         1  62.14249  23.46889 2020-02-18 22:00:00
#> 2  Clitocybe subsinopi…         1  66.11093  26.76504 2020-02-18 22:00:00
#> 3     Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
#> 4      Larus argentatus         2  60.46486  22.35936 2020-02-18 22:00:00
#> 5     Dendrocopos major         1  60.46486  22.35936 2020-02-18 22:00:00
#> 6         Turdus merula         2  60.46486  22.35936 2020-02-18 22:00:00
#> 7     Dryocopus martius         1  60.46486  22.35936 2020-02-18 22:00:00
#> 8         Corvus corone         1  60.46486  22.35936 2020-02-18 22:00:00
#> 9             Pica pica         4  60.42794  22.20052 2020-02-18 22:00:00
#> 10     Larus argentatus        40  60.42794  22.20052 2020-02-18 22:00:00
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
#> Records available: 26985020
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Cortinarius dionysae         1  62.14249  23.46889 2020-02-18 22:00:00
#> 2  Clitocybe subsinopi…         1  66.11093  26.76504 2020-02-18 22:00:00
#> 3      Larus argentatus         2  60.46486  22.35936 2020-02-18 22:00:00
#> 4     Dendrocopos major         1  60.46486  22.35936 2020-02-18 22:00:00
#> 5         Turdus merula         2  60.46486  22.35936 2020-02-18 22:00:00
#> 6     Dryocopus martius         1  60.46486  22.35936 2020-02-18 22:00:00
#> 7         Corvus corone         1  60.46486  22.35936 2020-02-18 22:00:00
#> 8             Pica pica         4  60.42794  22.20052 2020-02-18 22:00:00
#> 9      Larus argentatus        40  60.42794  22.20052 2020-02-18 22:00:00
#> 10          Picus canus         1  60.42794  22.20052 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(filter = list(date_range_ym = c("2019-12")))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 7546
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
#> Records available: 334575
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
#> Records available: 1483015
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Cortinarius dionysae         1  62.14249  23.46889 2020-02-18 22:00:00
#> 2  Clitocybe subsinopi…         1  66.11093  26.76504 2020-02-18 22:00:00
#> 3     Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
#> 4      Larus argentatus         2  60.46486  22.35936 2020-02-18 22:00:00
#> 5     Dendrocopos major         1  60.46486  22.35936 2020-02-18 22:00:00
#> 6         Turdus merula         2  60.46486  22.35936 2020-02-18 22:00:00
#> 7     Dryocopus martius         1  60.46486  22.35936 2020-02-18 22:00:00
#> 8         Corvus corone         1  60.46486  22.35936 2020-02-18 22:00:00
#> 9             Pica pica         4  60.42794  22.20052 2020-02-18 22:00:00
#> 10     Larus argentatus        40  60.42794  22.20052 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


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
#>     302908   31320885
```


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
#> [1] 679749
```


```r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland", nmin = 10000
)

finbif_occurrence(filter = list(collection = collections))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 8142423
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Formica (Formica)         1  59.89200   22.5170 2020-02-18 22:00:00
#> 2            Pica pica         9  62.10863   28.6248 2020-02-18 07:05:00
#> 3      Regulus regulus         5  62.10863   28.6248 2020-02-18 07:05:00
#> 4     Poecile montanus         6  62.10863   28.6248 2020-02-18 07:05:00
#> 5         Corvus corax         7  62.10863   28.6248 2020-02-18 07:05:00
#> 6    Dendrocopos major         5  62.10863   28.6248 2020-02-18 07:05:00
#> 7      Corvus monedula        43  62.10863   28.6248 2020-02-18 07:05:00
#> 8  Garrulus glandarius         3  62.10863   28.6248 2020-02-18 07:05:00
#> 9    Loxia curvirostra         1  62.10863   28.6248 2020-02-18 07:05:00
#> 10     Passer montanus         4  62.10863   28.6248 2020-02-18 07:05:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(filter = list(informal_group = "Reptiles and amphibians"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 30472
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
#> Records available: 259580
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Oenopia conglobata         1  61.71205  29.39218 2020-02-13 13:36:00
#> 2    Oenopia conglobata         1  61.71378  29.39089 2020-02-12 16:52:00
#> 3  Nanomimus circumscr…         1  60.41145  26.60956 2020-02-10 22:00:00
#> 4    Nephus bipunctatus         1  60.41145  26.60956 2020-02-10 22:00:00
#> 5  Calodromius spilotus         2  60.14807  22.29686 2020-02-01 22:00:00
#> 6    Stethorus pusillus         1  60.28865  24.86263 2020-01-29 22:00:00
#> 7  Calodromius spilotus         2  60.11620  24.63514 2020-01-25 22:00:00
#> 8  Dromius quadrimacul…         1  60.11620  24.63514 2020-01-25 22:00:00
#> 9    Scymnus ferrugatus         1  60.50135  25.94171 2020-01-25 22:00:00
#> 10 Subcoccinella vigin…         1  61.05561  26.70590 2020-01-20 22:00:00
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
#> Records available: 104633
#> A data.frame [10 x 30]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Gavia adamsii         1  61.14620  26.72432 2020-02-04 22:00:00
#> 2    Larus glaucoides         1  63.82952  23.03191 2020-02-04 22:00:00
#> 3   Larus hyperboreus         1  63.82944  23.03180 2020-02-03 22:00:00
#> 4    Larus glaucoides         1  63.82939  23.02910 2020-02-02 22:00:00
#> 5       Milvus milvus         1  60.08416  23.40222 2020-01-06 07:15:00
#> 6  Cygnus columbianus         1  60.15734  24.87389 2020-01-05 07:10:00
#> 7       Gavia adamsii         1  61.15926  28.76690 2020-01-01 07:50:00
#> 8   Larus hyperboreus         1  65.07408  25.40821 2019-12-31 08:05:00
#> 9       Bubulcus ibis         1  26.15296 -81.53502 2019-12-27 05:00:00
#> 10      Bubulcus ibis         1  27.56583 -82.51408 2019-12-27 05:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
