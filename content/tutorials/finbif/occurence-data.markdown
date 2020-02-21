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



The principle purpose of `{finbif}` is accessing occurrence data stored in the FinBIF
database. Occurrence data can be retrieved from FinBIF with the function
`finbif_occurrence`. Without any arguments specified `finbif_occurrence` will
retrieve the latest 10 occurrence records from FinBIF.

```r
finbif_occurrence()
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34457813
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1         Cygnus cygnus        12  60.84227  28.29145 2020-02-20 21:00:00
#> 2  Nodulosphaeria doli…         1  61.39360  23.79393 2020-02-20 22:00:00
#> 3         Cygnus cygnus         1  60.71733  27.21708 2020-02-20 22:00:00
#> 4             Grus grus         1  60.39137  23.93784 2020-02-20 22:00:00
#> 5  Impatiens glandulif…      1000  60.98270  25.66108 2020-02-20 22:00:00
#> 6             Pica pica         9  60.69584  27.07649 2020-02-21 06:05:00
#> 7           Picus canus         1  60.69584  27.07649 2020-02-21 06:05:00
#> 8      Poecile montanus         2  60.69584  27.07649 2020-02-21 06:05:00
#> 9   Emberiza citrinella       208  60.69584  27.07649 2020-02-21 06:05:00
#> 10         Corvus corax         6  60.69584  27.07649 2020-02-21 06:05:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
The print method for the resulting `finbif_occ` object will display the number
of records downloaded, the total number of records available, a data summary
including up to 10 rows of some core record variables (when available), the
number of remaining records and variables, as well as the names of additional
variables.

## Choosing taxa
You can limit the records to certain taxa by specifying them as an argument.

```r
finbif_occurrence("Cygnus cygnus")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56167
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus        12  60.84227  28.29145 2020-02-20 21:00:00
#> 2    Cygnus cygnus         1  60.71733  27.21708 2020-02-20 22:00:00
#> 3    Cygnus cygnus        38  60.69584  27.07649 2020-02-21 06:05:00
#> 4    Cygnus cygnus         3  60.13373  24.93114 2020-02-19 22:00:00
#> 5    Cygnus cygnus         1  62.26738  27.18153 2020-02-18 22:00:00
#> 6    Cygnus cygnus         1  61.45189  22.85723 2020-02-18 22:00:00
#> 7    Cygnus cygnus         1  61.99939  22.16288 2020-02-17 22:00:00
#> 8    Cygnus cygnus         1  60.60605  24.51953 2020-02-17 22:00:00
#> 9    Cygnus cygnus         1  60.46486  22.35936 2020-02-16 22:00:00
#> 10   Cygnus cygnus         6  60.98625  26.03254 2020-02-14 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

Multiple taxa can be requested at once.

```r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 80351
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus        12  60.84227  28.29145 2020-02-20 21:00:00
#> 2    Cygnus cygnus         1  60.71733  27.21708 2020-02-20 22:00:00
#> 3    Cygnus cygnus        38  60.69584  27.07649 2020-02-21 06:05:00
#> 4    Cygnus cygnus         3  60.13373  24.93114 2020-02-19 22:00:00
#> 5    Cygnus cygnus         1  62.26738  27.18153 2020-02-18 22:00:00
#> 6    Cygnus cygnus         1  61.45189  22.85723 2020-02-18 22:00:00
#> 7      Cygnus olor         1  60.44731  22.39747 2020-02-18 22:00:00
#> 8    Cygnus cygnus         1  61.99939  22.16288 2020-02-17 22:00:00
#> 9      Cygnus olor         2  60.40923  22.20508 2020-02-17 22:00:00
#> 10   Cygnus cygnus         1  60.60605  24.51953 2020-02-17 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

You can also chose higher taxonomic groups and use common names (in English,
Finnish and Swedish)

```r
birds  <- finbif_occurrence("Birds")
linnut <- finbif_occurrence("Linnut")
faglar <- finbif_occurrence("Fåglar")

sapply(list(birds, linnut, faglar), nrow)
```

```{.language-r}
#> [1] 10 10 10
```

## Request size
You can increase the number of records returned by using the `n` argument.

```r
occurrences <- finbif_occurrence(n = 1001)
```

You can invoke a spreadsheet-style data browser with the `View` function

```r
View(occurrences)
```
When using the RStudio IDE you can also invoke the browser by clicking on the
data in the 'Environment' pane.

{{< figure library="true" src="data-viewer.png" lightbox="true" >}}

When there are more than 1000 records to retrieve a progress bar will be
initiated. You can suppress the progress bar with the `quiet` argument.

```r
finbif_occurrence(n = 1001, quiet = TRUE)
```

You can see how many records are available for a given request, without
retrieving any records, by setting `count_only = TRUE`.

```r
finbif_occurrence(count_only = TRUE)
```

```{.language-r}
#> [1] 34457813
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
#> Records available: 3291
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

## Time & duration

```r
finbif_occurrence(date_time = FALSE)
```

### Accuracy

```r
finbif_occurrence(date_time_method = "accurate")
```

### Timezone

```r
finbif_occurrence(tzone = "Etc/UTC")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34457813
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1         Cygnus cygnus        12  60.84227  28.29145 2020-02-20 21:00:00
#> 2  Nodulosphaeria doli…         1  61.39360  23.79393 2020-02-20 22:00:00
#> 3         Cygnus cygnus         1  60.71733  27.21708 2020-02-20 22:00:00
#> 4             Grus grus         1  60.39137  23.93784 2020-02-20 22:00:00
#> 5  Impatiens glandulif…      1000  60.98270  25.66108 2020-02-20 22:00:00
#> 6             Pica pica         9  60.69584  27.07649 2020-02-21 06:05:00
#> 7           Picus canus         1  60.69584  27.07649 2020-02-21 06:05:00
#> 8      Poecile montanus         2  60.69584  27.07649 2020-02-21 06:05:00
#> 9   Emberiza citrinella       208  60.69584  27.07649 2020-02-21 06:05:00
#> 10         Corvus corax         6  60.69584  27.07649 2020-02-21 06:05:00
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
#> Records available: 34457813
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1         Cygnus cygnus        12  60.84227  28.29145 2020-02-20 23:00:00
#> 2  Nodulosphaeria doli…         1  61.39360  23.79393 2020-02-21 00:00:00
#> 3         Cygnus cygnus         1  60.71733  27.21708 2020-02-21 00:00:00
#> 4             Grus grus         1  60.39137  23.93784 2020-02-21 00:00:00
#> 5  Impatiens glandulif…      1000  60.98270  25.66108 2020-02-21 00:00:00
#> 6             Pica pica         9  60.69584  27.07649 2020-02-21 08:05:00
#> 7           Picus canus         1  60.69584  27.07649 2020-02-21 08:05:00
#> 8      Poecile montanus         2  60.69584  27.07649 2020-02-21 08:05:00
#> 9   Emberiza citrinella       208  60.69584  27.07649 2020-02-21 08:05:00
#> 10         Corvus corax         6  60.69584  27.07649 2020-02-21 08:05:00
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

## Darwin Core Variables

```r
finbif_occurrence(dwc = TRUE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34457813
#> A data.frame [10 x 30]
#>          scientificName individualCount decimalLatitude decimalLongitude
#> 1         Cygnus cygnus              12        60.84227         28.29145
#> 2  Nodulosphaeria doli…               1        61.39360         23.79393
#> 3         Cygnus cygnus               1        60.71733         27.21708
#> 4             Grus grus               1        60.39137         23.93784
#> 5  Impatiens glandulif…            1000        60.98270         25.66108
#> 6             Pica pica               9        60.69584         27.07649
#> 7           Picus canus               1        60.69584         27.07649
#> 8      Poecile montanus               2        60.69584         27.07649
#> 9   Emberiza citrinella             208        60.69584         27.07649
#> 10         Corvus corax               6        60.69584         27.07649
#>          eventDateTime
#> 1  2020-02-20 21:00:00
#> 2  2020-02-20 22:00:00
#> 3  2020-02-20 22:00:00
#> 4  2020-02-20 22:00:00
#> 5  2020-02-20 22:00:00
#> 6  2020-02-21 06:05:00
#> 7  2020-02-21 06:05:00
#> 8  2020-02-21 06:05:00
#> 9  2020-02-21 06:05:00
#> 10 2020-02-21 06:05:00
#> ...with 0 more records and 25 more variables:
#> taxonRankID, country, stateProvince, county, eventDateStart,
#> eventDateEnd, hourStart, hourEnd, minuteStart, minuteEnd,
#> occurrenceID, organismID, eventID, collectionID, hasIssues,
#> occurrenceIssue, occurrenceReliable, identificationQualifier,
#> documentIssue, documentReliability, coordinateUncertaintyInMeters,
#> eventIssue, locationIssue, timeIssue, samplingEffort
```
