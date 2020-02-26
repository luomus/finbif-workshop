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
### Places

```r
finbif_occurrence(filter = c(country = "Finland"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 32630398
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Exaeretia ciniflone…         1  61.51447  24.02330 2020-02-26 00:00:00
#> 2             Pica pica        10  60.45041  25.20184 2020-02-26 07:30:00
#> 3           Picus canus         2  60.45041  25.20184 2020-02-26 07:30:00
#> 4       Regulus regulus         3  60.45041  25.20184 2020-02-26 07:30:00
#> 5          Corvus corax         2  60.45041  25.20184 2020-02-26 07:30:00
#> 6        Periparus ater         2  60.45041  25.20184 2020-02-26 07:30:00
#> 7                 Loxia        22  60.45041  25.20184 2020-02-26 07:30:00
#> 8     Dendrocopos major         8  60.45041  25.20184 2020-02-26 07:30:00
#> 9         Turdus merula         4  60.45041  25.20184 2020-02-26 07:30:00
#> 10      Corvus monedula        16  60.45041  25.20184 2020-02-26 07:30:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Coordinates

```r
finbif_occurrence(
  filter = list(
    coordinates = list(lat = c(60, 68), lon = c(20, 30), system = "wgs84")
  )
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 26997644
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Exaeretia ciniflone…         1  61.51447  24.02330 2020-02-26 00:00:00
#> 2             Pica pica        10  60.45041  25.20184 2020-02-26 07:30:00
#> 3           Picus canus         2  60.45041  25.20184 2020-02-26 07:30:00
#> 4       Regulus regulus         3  60.45041  25.20184 2020-02-26 07:30:00
#> 5          Corvus corax         2  60.45041  25.20184 2020-02-26 07:30:00
#> 6        Periparus ater         2  60.45041  25.20184 2020-02-26 07:30:00
#> 7                 Loxia        22  60.45041  25.20184 2020-02-26 07:30:00
#> 8     Dendrocopos major         8  60.45041  25.20184 2020-02-26 07:30:00
#> 9         Turdus merula         4  60.45041  25.20184 2020-02-26 07:30:00
#> 10      Corvus monedula        16  60.45041  25.20184 2020-02-26 07:30:00
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
#> Records available: 7746
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 2     Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 3  Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 4         Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 5    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> 6      Corvus monedula         2  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Passer montanus        12  62.21189  21.66492 2019-12-31 09:54:00
#> 8    Pyrrhula pyrrhula         1  62.21189  21.66492 2019-12-31 09:54:00
#> 9   Certhia familiaris         2  62.21189  21.66492 2019-12-31 09:54:00
#> 10 Cyanistes caeruleus         6  62.21189  21.66492 2019-12-31 09:54:00
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
#> Records available: 338184
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 2     Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 3  Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 4         Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 5    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> 6      Corvus monedula         2  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Passer montanus        12  62.21189  21.66492 2019-12-31 09:54:00
#> 8    Pyrrhula pyrrhula         1  62.21189  21.66492 2019-12-31 09:54:00
#> 9   Certhia familiaris         2  62.21189  21.66492 2019-12-31 09:54:00
#> 10 Cyanistes caeruleus         6  62.21189  21.66492 2019-12-31 09:54:00
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
#> Records available: 1485628
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84  date_time
#> 1      Acalypta parvula         1  60.28291  22.40971 2020-02-20
#> 2    Dolycoris baccarum         1  60.28291  22.40971 2020-02-20
#> 3    Dolycoris baccarum         4  60.28291  22.40971 2020-02-20
#> 4       Drymus brunneus         3  60.28291  22.40971 2020-02-20
#> 5      Elasmucha grisea         1  60.28291  22.40971 2020-02-20
#> 6  Ischnocoris angustu…         1  60.28291  22.40971 2020-02-20
#> 7  Macrodema micropter…         1  60.28291  22.40971 2020-02-20
#> 8  Macrodema micropter…         1  60.28291  22.40971 2020-02-20
#> 9           Nabis ferus         1  60.28291  22.40971 2020-02-20
#> 10          Nabis ferus         1  60.28291  22.40971 2020-02-20
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
#>     306824   31337594
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
#> [1] 684723
```


```r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland",
  nmin   = 10000
)

finbif_occurrence(filter = list(collection = collections), count_only = TRUE)
```

```{.language-r}
#> [1] 8144995
```

## Informal groups

```r
finbif_occurrence(filter = list(informal_group = "Reptiles and amphibians"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 30483
#> A data.frame [10 x 30]
#>     scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Anguis fragilis         1  59.96766  24.39325 2020-02-22 00:00:00
#> 2   Anguis fragilis         1  62.25426  25.13755 2020-02-21 00:00:00
#> 3  Zootoca vivipara         1  60.26828  24.89337 2020-02-17 00:00:00
#> 4         Bufo bufo         1  60.23152  24.98346 2020-01-15 18:00:00
#> 5   Anguis fragilis         1  60.23968  25.79487 2020-01-04 18:00:00
#> 6         Bufo bufo         1  61.08603  26.86767 2020-01-03 14:53:00
#> 7        Lacertidae         1  28.14624 -16.43370 2019-12-04 13:00:00
#> 8        Lacertidae         1  28.13532 -16.44389 2019-12-04 13:00:00
#> 9         Bufo bufo         1  60.89002  24.69797 2019-10-18 10:00:00
#> 10        Bufo bufo         1  60.82829  24.58493 2019-10-13 00:00:00
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
  filter = list(informal_group = "Birds", administrative_status = "EU_INVSV")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 437
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Alopochen aegyptiaca         3  52.16081  4.485534 2019-10-23 01:00:00
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


```r
finbif_occurrence(
  filter = list(informal_group = "Mammals", red_list_status = "NT")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 1647
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84  date_time
#> 1  Rangifer tarandus f…         4  64.42648  29.11431 2019-10-20
#> 2  Rangifer tarandus f…         1  64.09919  29.40356 2019-09-23
#> 3  Rangifer tarandus f…         1  63.79309  29.51080 2019-09-13
#> 4  Rangifer tarandus f…         1  63.93649  29.59252 2019-07-26
#> 5  Rangifer tarandus f…         2  63.27123  25.35634 2019-06-28
#> 6  Rangifer tarandus f…         1  63.26554  25.36645 2019-06-28
#> 7  Rangifer tarandus f…         4  63.03293  24.32905 2019-06-13
#> 8  Rangifer tarandus f…         1  64.32293  26.69975 2019-05-27
#> 9  Rangifer tarandus f…         1  63.54897  24.54795 2019-05-18
#> 10 Rangifer tarandus f…         7  64.43140  29.11998 2019-04-28
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
#> Records available: 259711
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Dromius quadrimacul…         1  60.29713  22.39969 2020-02-20 00:00:00
#> 2    Hylesinus crenatus         1  60.29713  22.39969 2020-02-20 00:00:00
#> 3   Conistra rubiginosa         4  60.45842  22.17823 2020-02-17 00:00:00
#> 4    Oenopia conglobata         1  61.71205  29.39218 2020-02-13 15:36:00
#> 5    Oenopia conglobata         1  61.71378  29.39089 2020-02-12 18:52:00
#> 6  Nanomimus circumscr…         1  60.41145  26.60956 2020-02-11 00:00:00
#> 7    Nephus bipunctatus         1  60.41145  26.60956 2020-02-11 00:00:00
#> 8  Calodromius spilotus         2  60.14807  22.29686 2020-02-02 00:00:00
#> 9    Stethorus pusillus         1  60.28865  24.86263 2020-01-30 00:00:00
#> 10 Calodromius spilotus         2  60.11620  24.63514 2020-01-26 00:00:00
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
#> Records available: 104607
#> A data.frame [10 x 30]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Milvus milvus         1  60.78519  26.07963 2020-02-19 07:00:00
#> 2       Gavia adamsii         1  61.14620  26.72432 2020-02-05 00:00:00
#> 3    Larus glaucoides         1  63.82952  23.03191 2020-02-05 00:00:00
#> 4   Larus hyperboreus         1  63.82944  23.03180 2020-02-04 00:00:00
#> 5    Larus glaucoides         1  63.82939  23.02910 2020-02-03 00:00:00
#> 6       Milvus milvus         1  60.08416  23.40222 2020-01-06 09:15:00
#> 7  Cygnus columbianus         1  60.15734  24.87389 2020-01-05 09:10:00
#> 8       Gavia adamsii         1  61.15926  28.76690 2020-01-01 09:50:00
#> 9   Larus hyperboreus         1  65.07408  25.40821 2019-12-31 10:05:00
#> 10      Bubulcus ibis         1  26.15296 -81.53502 2019-12-27 07:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
