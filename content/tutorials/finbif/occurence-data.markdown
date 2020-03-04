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
#> Records available: 34492000
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Carduelis carduelis         1  60.42794  22.20052 2020-03-04 12:00:00
#> 2      Chloris chloris         4  60.42794  22.20052 2020-03-04 12:00:00
#> 3        Spinus spinus         1  60.42794  22.20052 2020-03-04 12:00:00
#> 4     Nabis ericetorum         1  61.66988  29.45235 2020-03-04 14:16:00
#> 5            Pica pica        29  65.82691  24.61553 2020-03-04 08:20:00
#> 6     Poecile montanus         7  65.82691  24.61553 2020-03-04 08:20:00
#> 7         Corvus corax         4  65.82691  24.61553 2020-03-04 08:20:00
#> 8  Capreolus capreolus         1  65.82691  24.61553 2020-03-04 08:20:00
#> 9     Sciurus vulgaris         1  65.82691  24.61553 2020-03-04 08:20:00
#> 10   Dendrocopos minor         1  65.82691  24.61553 2020-03-04 08:20:00
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
#> Records available: 56318
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus        15  60.84193  26.18736 2020-03-04 12:00:00
#> 2    Cygnus cygnus         2  60.76942  26.11235 2020-03-04 12:00:00
#> 3    Cygnus cygnus         2  60.67690  27.14658 2020-03-03 09:00:00
#> 4    Cygnus cygnus         2  61.10389  21.54485 2020-03-03 14:30:00
#> 5    Cygnus cygnus         1  61.03526  24.52440 2020-03-03 12:00:00
#> 6    Cygnus cygnus         8  60.14002  23.48627 2020-03-03 08:30:00
#> 7    Cygnus cygnus         1  59.86994  23.05875 2020-03-02 08:30:00
#> 8    Cygnus cygnus        33  60.89283  21.58223 2020-03-02 08:30:00
#> 9    Cygnus cygnus         3  60.42794  22.20052 2020-03-02 12:00:00
#> 10   Cygnus cygnus        10  60.45250  22.38029 2020-03-02 12:00:00
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
#> Records available: 80555
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus        15  60.84193  26.18736 2020-03-04 12:00:00
#> 2    Cygnus cygnus         2  60.76942  26.11235 2020-03-04 12:00:00
#> 3      Cygnus olor         4  60.19697  25.10493 2020-03-03 07:45:00
#> 4    Cygnus cygnus         2  60.67690  27.14658 2020-03-03 09:00:00
#> 5    Cygnus cygnus         2  61.10389  21.54485 2020-03-03 14:30:00
#> 6    Cygnus cygnus         1  61.03526  24.52440 2020-03-03 12:00:00
#> 7    Cygnus cygnus         8  60.14002  23.48627 2020-03-03 08:30:00
#> 8      Cygnus olor        73  59.86994  23.05875 2020-03-02 08:30:00
#> 9    Cygnus cygnus         1  59.86994  23.05875 2020-03-02 08:30:00
#> 10   Cygnus cygnus        33  60.89283  21.58223 2020-03-02 08:30:00
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
#> [1] 34492000
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
#> Records available: 3301
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Vulpes vulpes         1  60.82207  21.26828 2020-03-02 20:00:00
#> 2    Vulpes vulpes         2  61.15387  24.67518 2020-03-01 14:30:00
#> 3    Vulpes vulpes         1  60.83577  21.25200 2020-02-29 09:00:00
#> 4    Vulpes vulpes         2  60.72749  26.99773 2020-02-29 08:25:00
#> 5    Vulpes vulpes         1  60.07519  23.39469 2020-02-28 12:00:00
#> 6    Vulpes vulpes         3  62.35611  29.03439 2020-02-28 07:30:00
#> 7    Vulpes vulpes         1  60.41757  22.18200 2020-02-25 07:00:00
#> 8    Vulpes vulpes         1  60.48211  22.38024 2020-02-23 07:45:00
#> 9    Vulpes vulpes         2  61.52358  24.42464 2020-02-22 12:00:00
#> 10   Vulpes vulpes         1  60.83577  21.25200 2020-02-18 20:30:00
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
#> Records available: 34492000
#> A data.frame [10 x 28]
#>        scientific_name abundance lat_wgs84 lon_wgs84 taxon_rank
#> 1  Carduelis carduelis         1  60.42794  22.20052 MX.species
#> 2      Chloris chloris         4  60.42794  22.20052 MX.species
#> 3        Spinus spinus         1  60.42794  22.20052 MX.species
#> 4     Nabis ericetorum         1  61.66988  29.45235 MX.species
#> 5            Pica pica        29  65.82691  24.61553 MX.species
#> 6     Poecile montanus         7  65.82691  24.61553 MX.species
#> 7         Corvus corax         4  65.82691  24.61553 MX.species
#> 8  Capreolus capreolus         1  65.82691  24.61553 MX.species
#> 9     Sciurus vulgaris         1  65.82691  24.61553 MX.species
#> 10   Dendrocopos minor         1  65.82691  24.61553 MX.species
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
#> Records available: 34492000
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Carduelis carduelis         1  60.42794  22.20052 2020-03-04 10:00:00
#> 2      Chloris chloris         4  60.42794  22.20052 2020-03-04 10:00:00
#> 3        Spinus spinus         1  60.42794  22.20052 2020-03-04 10:00:00
#> 4     Nabis ericetorum         1  61.66988  29.45235 2020-03-04 12:16:00
#> 5            Pica pica        29  65.82691  24.61553 2020-03-04 06:20:00
#> 6     Poecile montanus         7  65.82691  24.61553 2020-03-04 06:20:00
#> 7         Corvus corax         4  65.82691  24.61553 2020-03-04 06:20:00
#> 8  Capreolus capreolus         1  65.82691  24.61553 2020-03-04 06:20:00
#> 9     Sciurus vulgaris         1  65.82691  24.61553 2020-03-04 06:20:00
#> 10   Dendrocopos minor         1  65.82691  24.61553 2020-03-04 06:20:00
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
