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



The core purpose of `{finbif}` is accessing occurrence data stored in the
FinBIF database. Occurrence data can be retrieved from FinBIF with the function
`finbif_occurrence`. Without any arguments specified `finbif_occurrence` will
retrieve the latest 10 occurrence records from FinBIF.

```r
finbif_occurrence()
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34469168
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
The print method for the resulting `finbif_occ` object will display the number
of records downloaded, the total number of records available, a data summary
including up to 10 rows of some core record variables (when available), the
number of remaining records and variables, as well as the names of additional
variables.

## Darwin Core Variables
You can switch from the default variable names to [Darwin Core
](http://rs.tdwg.org/dwc/) style names by setting `dwc = TRUE`.

```r
colnames(finbif_occurrence(dwc = TRUE))
```

```{.language-r}
#>  [1] "scientificName"                "taxonRankID"                  
#>  [3] "individualCount"               "country"                      
#>  [5] "stateProvince"                 "county"                       
#>  [7] "decimalLatitude"               "decimalLongitude"             
#>  [9] "eventDateStart"                "eventDateEnd"                 
#> [11] "hourStart"                     "hourEnd"                      
#> [13] "minuteStart"                   "minuteEnd"                    
#> [15] "occurrenceID"                  "organismID"                   
#> [17] "eventID"                       "collectionID"                 
#> [19] "hasIssues"                     "occurrenceIssue"              
#> [21] "occurrenceReliable"            "identificationQualifier"      
#> [23] "documentIssue"                 "documentReliability"          
#> [25] "coordinateUncertaintyInMeters" "eventIssue"                   
#> [27] "locationIssue"                 "timeIssue"                    
#> [29] "eventDateTime"                 "samplingEffort"
```

## Choosing taxa
You can limit the records to certain taxa by specifying them as an argument.

```r
finbif_occurrence("Cygnus cygnus")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56217
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         2  60.84191  26.18741 2020-02-26 00:00:00
#> 2    Cygnus cygnus         1  63.02968  27.56801 2020-02-26 00:00:00
#> 3    Cygnus cygnus         1  60.27739  25.12584 2020-02-25 07:45:00
#> 4    Cygnus cygnus         6  60.83173  26.23621 2020-02-25 00:00:00
#> 5    Cygnus cygnus         2  61.15504  24.03195 2020-02-25 08:32:00
#> 6    Cygnus cygnus         2  60.41757  22.18200 2020-02-25 07:00:00
#> 7    Cygnus cygnus        17  60.76462  26.09601 2020-02-25 07:30:00
#> 8    Cygnus cygnus         4  61.12274  21.52946 2020-02-25 09:15:00
#> 9    Cygnus cygnus        74  60.76204  23.23494 2020-02-25 09:20:00
#> 10   Cygnus cygnus         6  60.07656  23.48915 2020-02-25 08:30:00
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
#> Records available: 80425
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         2  60.84191  26.18741 2020-02-26 00:00:00
#> 2    Cygnus cygnus         1  63.02968  27.56801 2020-02-26 00:00:00
#> 3    Cygnus cygnus         1  60.27739  25.12584 2020-02-25 07:45:00
#> 4      Cygnus olor         2  60.96802  25.94211 2020-02-25 00:00:00
#> 5    Cygnus cygnus         6  60.83173  26.23621 2020-02-25 00:00:00
#> 6    Cygnus cygnus         2  61.15504  24.03195 2020-02-25 08:32:00
#> 7      Cygnus olor        12  60.41757  22.18200 2020-02-25 07:00:00
#> 8    Cygnus cygnus         2  60.41757  22.18200 2020-02-25 07:00:00
#> 9    Cygnus cygnus        17  60.76462  26.09601 2020-02-25 07:30:00
#> 10   Cygnus cygnus         4  61.12274  21.52946 2020-02-25 09:15:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

You can also chose higher taxonomic groups and use common names (in English,
Finnish and Swedish).

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
#> [1] 34469168
```

## Checking taxa
When you request occurrence records for specific taxa, by default, the taxon
names are first checked against the FinBIF database. If any of the requested
taxa are not found in the database you will receive a warning but the data will
still be retrieved for the remaining taxa.

```r
finbif_occurrence("Vulpes vulpes", "Moomin")
```

```
#> Warning: Cannot find taxa: Moomin
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 3293
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Vulpes vulpes         1  60.41757  22.18200 2020-02-25 07:00:00
#> 2    Vulpes vulpes         2  61.52358  24.42464 2020-02-22 00:00:00
#> 3    Vulpes vulpes         1  60.83577  21.25200 2020-02-18 20:30:00
#> 4    Vulpes vulpes         1  61.10698  21.54084 2020-02-15 07:10:00
#> 5    Vulpes vulpes         1  61.52412  24.42621 2020-02-14 00:00:00
#> 6    Vulpes vulpes         1  61.53563  24.60958 2020-02-11 00:00:00
#> 7    Vulpes vulpes         1  60.82982  21.26534 2020-02-03 16:30:00
#> 8    Vulpes vulpes         2  60.42676  22.20634 2020-01-29 00:00:00
#> 9    Vulpes vulpes         1  60.41130  22.27454 2020-01-22 00:00:00
#> 10   Vulpes vulpes         1  60.08711  23.51647 2020-01-12 00:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

You can turn off taxon name pre-checking by setting the value of the
`check_taxa` argument to `FALSE`. 

```r
finbif_occurrence("Vulpes vulpes", "Moomin", check_taxa = FALSE)
```

By setting the argument, `on_check_fail` to `"error"` (the default is `"warn"`),
you can elevate the warnings to errors and the request will fail if any of the
taxa are not found in the FinBIF database.

```r
finbif_occurrence("Vulpes vulpes", "Moomin", on_check_fail = "error")
```

```
#> Error: Cannot find taxa: Moomin
```
This can be a useful strategy if you are using `{finbif}` non-interactively
(in a script), and you do not want to proceed if any of your taxon names are
wrong or misspelled.

## Time & duration
The default behaviour of `finbif_occurrence` is to consolidate date and time
data for occurrence recording events into `date_time` and `duration` variables.
This can be turned off (which can speed up data processing time) by setting
`date_time` to `"FALSE"`.

```r
finbif_occurrence(date_time = FALSE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34469168
#> A data.frame [10 x 28]
#>         scientific_name abundance lat_wgs84 lon_wgs84 taxon_rank
#> 1  Exaeretia ciniflone…         1  61.51447  24.02330 MX.species
#> 2             Pica pica        10  60.45041  25.20184 MX.species
#> 3           Picus canus         2  60.45041  25.20184 MX.species
#> 4       Regulus regulus         3  60.45041  25.20184 MX.species
#> 5          Corvus corax         2  60.45041  25.20184 MX.species
#> 6        Periparus ater         2  60.45041  25.20184 MX.species
#> 7                 Loxia        22  60.45041  25.20184   MX.genus
#> 8     Dendrocopos major         8  60.45041  25.20184 MX.species
#> 9         Turdus merula         4  60.45041  25.20184 MX.species
#> 10      Corvus monedula        16  60.45041  25.20184 MX.species
#> ...with 0 more records and 23 more variables:
#> country, province, municipality, date_start, date_end, hour_start,
#> hour_end, minute_start, minute_end, record_id, individual_id,
#> event_id, collection_id, any_issues, record_issue, record_reliable,
#> taxon_reliability, document_issue, collection_reliability,
#> coordinates_uncertainty, event_issue, location_issue, time_issue
```

### Timezone
#### Timezone input
The FinBIF database doesn't currently store timezone information, so `{finbif}`
makes assumptions about the appropriate timezone based on the time and location
of the occurrence recording events to calculate `date_time` and `duration`. By
default, a fast heuristic is used to determine the timezones. If you require
greater accuracy (e.g., you are using data on the Finnish/Swedish border and
daytime/nighttime hours are important), you can switch to more accurate, though
slower, timezone calculation method.

```r
finbif_occurrence(date_time_method = "accurate")
```

#### Timezone output
The timezone of the calculated `date_time` variable is determined by the
timezone of your operating system.

```r
Sys.timezone()
```

You can override this by setting the `tzone` argument to a different value.

```r
finbif_occurrence(tzone = "Etc/UTC")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34469168
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Exaeretia ciniflone…         1  61.51447  24.02330 2020-02-25 22:00:00
#> 2             Pica pica        10  60.45041  25.20184 2020-02-26 05:30:00
#> 3           Picus canus         2  60.45041  25.20184 2020-02-26 05:30:00
#> 4       Regulus regulus         3  60.45041  25.20184 2020-02-26 05:30:00
#> 5          Corvus corax         2  60.45041  25.20184 2020-02-26 05:30:00
#> 6        Periparus ater         2  60.45041  25.20184 2020-02-26 05:30:00
#> 7                 Loxia        22  60.45041  25.20184 2020-02-26 05:30:00
#> 8     Dendrocopos major         8  60.45041  25.20184 2020-02-26 05:30:00
#> 9         Turdus merula         4  60.45041  25.20184 2020-02-26 05:30:00
#> 10      Corvus monedula        16  60.45041  25.20184 2020-02-26 05:30:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

Or set the global timezone option to set the timezone for the current session.

```r
options(finbif_tz = "Etc/UTC")
```
This may be advisable for reproducibility or when working with multiple systems.
