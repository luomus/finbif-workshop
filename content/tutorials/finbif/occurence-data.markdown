---
title: Occurrence Data
draft: no
toc: yes
type: docs
weight: 6
menu:
  finbif:
    name: 5. Occurrence Data
    weight: 6
---




```r
finbif_occurrence()
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34449106
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Sclerencoelia fasci…      1000  60.37497  25.73377 2020-02-18 22:00:00
#> 2     Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
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

## Choosing taxa

```r
finbif_occurrence("Cygnus cygnus")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56160
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         1  61.99939  22.16288 2020-02-17 22:00:00
#> 2    Cygnus cygnus         1  60.60605  24.51953 2020-02-17 22:00:00
#> 3    Cygnus cygnus         1  60.46486  22.35936 2020-02-16 22:00:00
#> 4    Cygnus cygnus         6  60.98625  26.03254 2020-02-14 22:00:00
#> 5    Cygnus cygnus         4  60.82640  26.23698 2020-02-12 22:00:00
#> 6    Cygnus cygnus         1  61.45401  22.11611 2020-02-11 22:00:00
#> 7    Cygnus cygnus         4  60.76301  26.23474 2020-02-11 22:00:00
#> 8    Cygnus cygnus         1  61.11695  21.52778 2020-02-12 08:00:00
#> 9    Cygnus cygnus         5  60.84168  26.18780 2020-02-10 22:00:00
#> 10   Cygnus cygnus         7  60.46486  22.35936 2020-02-10 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence(c("Cygnus cygnus", "Cygnus olor"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 80341
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         1  61.99939  22.16288 2020-02-17 22:00:00
#> 2      Cygnus olor         2  60.40923  22.20508 2020-02-17 22:00:00
#> 3    Cygnus cygnus         1  60.60605  24.51953 2020-02-17 22:00:00
#> 4      Cygnus olor         1  60.46486  22.35936 2020-02-16 22:00:00
#> 5    Cygnus cygnus         1  60.46486  22.35936 2020-02-16 22:00:00
#> 6      Cygnus olor         4  60.18776  24.80067 2020-02-15 06:00:00
#> 7    Cygnus cygnus         6  60.98625  26.03254 2020-02-14 22:00:00
#> 8    Cygnus cygnus         4  60.82640  26.23698 2020-02-12 22:00:00
#> 9    Cygnus cygnus         1  61.45401  22.11611 2020-02-11 22:00:00
#> 10   Cygnus cygnus         4  60.76301  26.23474 2020-02-11 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence("Birds")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 17771800
#> A data.frame [10 x 30]
#>      scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Larus argentatus         2  60.46486  22.35936 2020-02-18 22:00:00
#> 2  Dendrocopos major         1  60.46486  22.35936 2020-02-18 22:00:00
#> 3      Turdus merula         2  60.46486  22.35936 2020-02-18 22:00:00
#> 4  Dryocopus martius         1  60.46486  22.35936 2020-02-18 22:00:00
#> 5      Corvus corone         1  60.46486  22.35936 2020-02-18 22:00:00
#> 6          Pica pica         4  60.42794  22.20052 2020-02-18 22:00:00
#> 7   Larus argentatus        40  60.42794  22.20052 2020-02-18 22:00:00
#> 8        Picus canus         1  60.42794  22.20052 2020-02-18 22:00:00
#> 9    Regulus regulus         1  60.42794  22.20052 2020-02-18 22:00:00
#> 10  Mergus merganser         2  60.42794  22.20052 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

## Request size

```r
occurrences<- finbif_occurrence(n = 1001)
View(occurrences)
```


```r
finbif_occurrence(n = 1001, quiet = TRUE)
```


```r
finbif_occurrence(count_only = TRUE)
```

```{.language-r}
#> [1] 34449106
```

## Checking taxa

```r
finbif_occurrence("Vulpes vulpes", "Moomin")
```

```
#> Warning in select_taxa(..., quiet = quiet, cache = cache, check_taxa =
#> check_taxa, : Cannot find taxa: Moomin
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 3288
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Vulpes vulpes         1  60.83577  21.25200 2020-02-18 18:30:00
#> 2    Vulpes vulpes         1  61.10698  21.54084 2020-02-15 05:10:00
#> 3    Vulpes vulpes         1  61.52412  24.42621 2020-02-13 22:00:00
#> 4    Vulpes vulpes         1  61.53563  24.60958 2020-02-10 22:00:00
#> 5    Vulpes vulpes         1  60.82982  21.26534 2020-02-03 14:30:00
#> 6    Vulpes vulpes         2  60.42676  22.20634 2020-01-28 22:00:00
#> 7    Vulpes vulpes         1  60.41130  22.27454 2020-01-21 22:00:00
#> 8    Vulpes vulpes         1  60.08711  23.51647 2020-01-11 22:00:00
#> 9    Vulpes vulpes         1  61.48478  25.13942 2020-01-06 07:30:00
#> 10   Vulpes vulpes         1  60.42794  22.20052 2020-01-04 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
finbif_occurrence("Vulpes vulpes", "Moomin", check_taxa = FALSE)
```


```r
finbif_occurrence("Vulpes vulpes", "Moomin", on_check_fail = "error")
```

## Time & Duration


```r
finbif_occurrence(date_time_method = "accurate")
```


```r
finbif_occurrence(tzone = "Etc/UTC")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34449106
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Sclerencoelia fasci…      1000  60.37497  25.73377 2020-02-18 22:00:00
#> 2     Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
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
finbif_occurrence(tzone = "Europe/Helsinki")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34449106
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84  date_time
#> 1  Sclerencoelia fasci…      1000  60.37497  25.73377 2020-02-19
#> 2     Formica (Formica)         1  59.89200  22.51700 2020-02-19
#> 3      Larus argentatus         2  60.46486  22.35936 2020-02-19
#> 4     Dendrocopos major         1  60.46486  22.35936 2020-02-19
#> 5         Turdus merula         2  60.46486  22.35936 2020-02-19
#> 6     Dryocopus martius         1  60.46486  22.35936 2020-02-19
#> 7         Corvus corone         1  60.46486  22.35936 2020-02-19
#> 8             Pica pica         4  60.42794  22.20052 2020-02-19
#> 9      Larus argentatus        40  60.42794  22.20052 2020-02-19
#> 10          Picus canus         1  60.42794  22.20052 2020-02-19
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```


```r
Sys.timezone()
```


```r
finbif_occurrence(date_time = FALSE)
```
## Darwin Core Variables

```r
finbif_occurrence(dwc = TRUE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34449106
#> A data.frame [10 x 30]
#>          scientificName individualCount decimalLatitude decimalLongitude
#> 1  Sclerencoelia fasci…            1000        60.37497         25.73377
#> 2     Formica (Formica)               1        59.89200         22.51700
#> 3      Larus argentatus               2        60.46486         22.35936
#> 4     Dendrocopos major               1        60.46486         22.35936
#> 5         Turdus merula               2        60.46486         22.35936
#> 6     Dryocopus martius               1        60.46486         22.35936
#> 7         Corvus corone               1        60.46486         22.35936
#> 8             Pica pica               4        60.42794         22.20052
#> 9      Larus argentatus              40        60.42794         22.20052
#> 10          Picus canus               1        60.42794         22.20052
#>          eventDateTime
#> 1  2020-02-18 22:00:00
#> 2  2020-02-18 22:00:00
#> 3  2020-02-18 22:00:00
#> 4  2020-02-18 22:00:00
#> 5  2020-02-18 22:00:00
#> 6  2020-02-18 22:00:00
#> 7  2020-02-18 22:00:00
#> 8  2020-02-18 22:00:00
#> 9  2020-02-18 22:00:00
#> 10 2020-02-18 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxonRankID, country, stateProvince, county, eventDateStart,
#> eventDateEnd, hourStart, hourEnd, minuteStart, minuteEnd,
#> occurrenceID, organismID, eventID, collectionID, hasIssues,
#> occurrenceIssue, occurrenceReliable, identificationQualifier,
#> documentIssue, documentReliability, coordinateUncertaintyInMeters,
#> eventIssue, locationIssue, timeIssue, samplingEffort
```

