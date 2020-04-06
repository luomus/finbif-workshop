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
#> Records available: 34617302
#> A data.frame [10 x 10]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Sturnus vulgaris  1         60.7171   27.2106  2020-04-06 12:00:00
#> 2   Tussilago farfara  1         63.74834  27.64843 2020-04-06 12:00:00
#> 3   Nymphalis antiopa  1         61.52834  24.86208 2020-04-05 12:00:00
#> 4  Rabocerus gabrieli  1         63.83328  23.0308  2020-04-05 12:00:00
#> 5       Vulpes vulpes  1         60.11628  23.47399 2020-04-05 12:00:00
#> 6    Hepatica nobilis  3         60.11204  23.5322  2020-04-05 12:00:00
#> 7      Bombus lucorum  1         60.11204  23.5322  2020-04-05 12:00:00
#> 8     Lepus europaeus  1         60.11612  23.46632 2020-04-05 12:00:00
#> 9     Lepus europaeus  1         60.12036  23.51049 2020-04-05 12:00:00
#> 10    Lepus europaeus  3         60.1201   23.49065 2020-04-05 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#>  [1] "scientificName"                "individualCount"              
#>  [3] "decimalLatitude"               "decimalLongitude"             
#>  [5] "eventDateTime"                 "occurrenceID"                 
#>  [7] "hasIssues"                     "occurrenceReliable"           
#>  [9] "identificationQualifier"       "coordinateUncertaintyInMeters"
```

## Choosing taxa
You can limit the records to certain taxa by specifying them as an argument.

```r
finbif_occurrence("Cygnus cygnus")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56796
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus  107       61.86859  22.96684 2020-04-05 12:00:00
#> 2    Cygnus cygnus  1         62.32176  25.98074 2020-04-05 12:00:00
#> 3    Cygnus cygnus  2         61.32291  28.56818 2020-04-04 11:15:00
#> 4    Cygnus cygnus  5         62.61591  29.66465 2020-04-03 12:00:00
#> 5    Cygnus cygnus  1         62.99784  27.83489 2020-04-02 12:00:00
#> 6    Cygnus cygnus  1         61.2824   28.97462 2020-03-31 12:00:00
#> 7    Cygnus cygnus  1         61.41813  23.32198 2020-03-30 12:00:00
#> 8    Cygnus cygnus  2         61.62618  22.86652 2020-03-29 12:00:00
#> 9    Cygnus cygnus  1         61.492    23.742   2020-03-29 12:00:00
#> 10   Cygnus cygnus  1         65.17944  25.36823 2020-03-29 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

Multiple taxa can be requested at once.

```r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 81090
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus  107       61.86859  22.96684 2020-04-05 12:00:00
#> 2    Cygnus cygnus  1         62.32176  25.98074 2020-04-05 12:00:00
#> 3    Cygnus cygnus  2         61.32291  28.56818 2020-04-04 11:15:00
#> 4      Cygnus olor  5         60.42794  22.20052 2020-04-04 12:00:00
#> 5    Cygnus cygnus  5         62.61591  29.66465 2020-04-03 12:00:00
#> 6      Cygnus olor  2         60.42794  22.20052 2020-04-02 12:00:00
#> 7    Cygnus cygnus  1         62.99784  27.83489 2020-04-02 12:00:00
#> 8      Cygnus olor  1         60.17308  25.10529 2020-04-01 12:00:00
#> 9      Cygnus olor  3         60.17308  25.10529 2020-04-01 12:00:00
#> 10   Cygnus cygnus  1         61.2824   28.97462 2020-03-31 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
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
#> [1] 34617302
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
#> Records available: 3319
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time  record_id
#> 1    Vulpes vulpes  1         60.11628  23.47399 2020-04-05 12:00:00   107461#8
#> 2    Vulpes vulpes  1         60.42794  22.20052 2020-03-31 12:00:00  105990#19
#> 3    Vulpes vulpes  1         62.61875  29.66306 2020-03-22 12:00:00   104874#4
#> 4    Vulpes vulpes  1         60.10224  23.5459  2020-03-22 12:00:00  104505#19
#> 5    Vulpes vulpes  1         60.55732  22.25711 2020-03-14 09:00:00   103437#4
#> 6    Vulpes vulpes  1         61.53879  25.16226 2020-03-11 12:00:00 057834#542
#> 7    Vulpes vulpes  2         60.36823  22.00878 2020-03-08 07:00:00 102782#167
#> 8    Vulpes vulpes  1         60.90204  26.16786 2020-03-08 08:35:00 102137#169
#> 9    Vulpes vulpes  1         62.29012  24.70473 2020-03-08 06:45:00   102034#4
#> 10   Vulpes vulpes  1         63.12255  24.32082 2020-03-07 08:00:00  102009#16
#> ...with 0 more records and 4 more variables:
#> any_issues, record_reliable, taxon_reliability, coordinates_uncertainty
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
data for occurrence recording events into a `date_time` variable. This can be
turned off (which can speed up data processing time) by deselecting the
`date_time` variable.

```r
finbif_occurrence(select = "-date_time")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34617519
#> A data.frame [10 x 9]
#>         scientific_name abundance lat_wgs84 lon_wgs84            record_id
#> 1  Mompha sturnipennel…  1         62.23735  27.42594         JX.1107473#4
#> 2                  <NA>  1         60.19302  23.41405         JX.1107471#3
#> 3      Sturnus vulgaris  1         60.7171   27.2106  KE.176/5e8ac1542d0e…
#> 4     Tussilago farfara  1         63.74834  27.64843 KE.176/5e8ab39e2d0e…
#> 5             Aglais io  1         61.50572  23.82138 KE.176/5e8ae6742d0e…
#> 6     Nymphalis antiopa  1         61.52834  24.86208         JX.1107463#4
#> 7    Rabocerus gabrieli  1         63.83328  23.0308          JX.1107462#4
#> 8         Vulpes vulpes  1         60.11628  23.47399         JX.1107461#8
#> 9      Hepatica nobilis  3         60.11204  23.5322         JX.1107461#39
#> 10       Bombus lucorum  1         60.11204  23.5322         JX.1107461#36
#> ...with 0 more records and 4 more variables:
#> any_issues, record_reliable, taxon_reliability, coordinates_uncertainty
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
#> Records available: 34617302
#> A data.frame [10 x 10]
#>       scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Sturnus vulgaris  1         60.7171   27.2106  2020-04-06 09:00:00
#> 2   Tussilago farfara  1         63.74834  27.64843 2020-04-06 09:00:00
#> 3   Nymphalis antiopa  1         61.52834  24.86208 2020-04-05 09:00:00
#> 4  Rabocerus gabrieli  1         63.83328  23.0308  2020-04-05 09:00:00
#> 5       Vulpes vulpes  1         60.11628  23.47399 2020-04-05 09:00:00
#> 6    Hepatica nobilis  3         60.11204  23.5322  2020-04-05 09:00:00
#> 7      Bombus lucorum  1         60.11204  23.5322  2020-04-05 09:00:00
#> 8     Lepus europaeus  1         60.11612  23.46632 2020-04-05 09:00:00
#> 9     Lepus europaeus  1         60.12036  23.51049 2020-04-05 09:00:00
#> 10    Lepus europaeus  3         60.1201   23.49065 2020-04-05 09:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

Or set the global timezone option to set the timezone for the current session.

```r
options(finbif_tz = "Etc/UTC")
```
This may be advisable for reproducibility or when working with multiple systems.
