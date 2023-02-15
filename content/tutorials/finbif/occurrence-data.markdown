---
linktitle: 5. Occurrence Data
title: Occurrence Data
draft: no
toc: yes
type: book
weight: 6
---


The core purpose of `{finbif}` is accessing occurrence data stored in the
FinBIF database. Occurrence data can be retrieved from FinBIF with the function
`finbif_occurrence`. Without any arguments specified `finbif_occurrence` will
retrieve the latest 10 occurrence records from FinBIF.

```r
finbif_occurrence()
```

```
#> Records downloaded: 10
#> Records available: 45893791
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 2  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 3         …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> 4  …HR.3211/148812589-U Fomitopsis pinicola…        NA  60.43726  22.37422
#> 5  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 6         …JX.1529815#3 Pteromys volans (Li…        NA  62.46923  25.94574
#> 7         …JX.1529813#6 Carduelis chloris (…  1         60.17831  24.65979
#> 8         …JX.1529813#9 Carduelis chloris (…        NA  60.17857  24.6614 
#> 9        …JX.1529813#12 Carduelis spinus (L…  1         60.1796   24.66341
#> 10        …JX.1529813#3 Passer montanus (Li…  3         60.17811  24.65902
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#>  [1] "occurrenceID"                  "scientificName"               
#>  [3] "individualCount"               "decimalLatitude"              
#>  [5] "decimalLongitude"              "eventDateTime"                
#>  [7] "coordinateUncertaintyInMeters" "hasIssues"                    
#>  [9] "requiresVerification"          "requiresIdentification"       
#> [11] "occurrenceReliability"         "occurrenceQuality"
```

## Choosing taxa
You can limit the records to certain taxa by specifying them as an argument.

```r
finbif_occurrence("Cygnus cygnus")
```

```
#> Records downloaded: 10
#> Records available: 87008
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1529724#3 Cygnus cygnus (Linn…  6         61.23665  21.603  
#> 2         …JX.1529605#3 Cygnus cygnus (Linn…  2         60.17308  25.10504
#> 3        …JX.1528427#12 Cygnus cygnus (Linn…  7         62.67004  26.83646
#> 4        …JX.1528427#21 Cygnus cygnus (Linn…  1         62.71214  26.88074
#> 5  …HR.4412/63df09c19f… Cygnus cygnus (Linn…        NA  64.22258  27.71767
#> 6        …JX.1525388#13 Cygnus cygnus (Linn…  6         61.23082  21.59979
#> 7         …JX.1524017#6 Cygnus cygnus (Linn…  1         62.71322  26.87991
#> 8  …HR.3211/147025285-U Cygnus cygnus (Linn…        NA  60.4534   22.40308
#> 9        …JX.1518416#24 Cygnus cygnus (Linn…  1         62.21534  24.41688
#> 10        …JX.1518050#3 Cygnus cygnus (Linn…        NA  60.45842  22.17798
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

Multiple taxa can be requested at once.

```r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

```
#> Records downloaded: 10
#> Records available: 128631
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1529724#3 Cygnus cygnus (Linn…  6         61.23665  21.603  
#> 2         …JX.1529605#3 Cygnus cygnus (Linn…  2         60.17308  25.10504
#> 3  …HR.3211/148449187-U Cygnus olor (J.F. G…        NA  60.17314  24.96962
#> 4  …HR.4412/63e6f54184… Cygnus olor (J.F. G…        NA  60.17038  24.925  
#> 5  …HR.4412/63e5a1fc8c… Cygnus olor (J.F. G…        NA  60.17038  24.925  
#> 6         …JX.1528551#5 Cygnus olor (J.F. G…  3         60.17975  24.93798
#> 7         …JX.1529628#8 Cygnus olor (J.F. G…  12        60.17989  24.93988
#> 8        …JX.1528427#12 Cygnus cygnus (Linn…  7         62.67004  26.83646
#> 9        …JX.1528427#21 Cygnus cygnus (Linn…  1         62.71214  26.88074
#> 10 …HR.3211/148044622-U Cygnus olor (J.F. G…        NA  60.17996  24.94015
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also chose higher taxonomic groups and use common names (in English,
Finnish and Swedish).

```r
birds  <- finbif_occurrence("Birds")
linnut <- finbif_occurrence("Linnut")
faglar <- finbif_occurrence("Fåglar")

sapply(list(birds, linnut, faglar), nrow)
```

```
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

{{% figure library="true" src="/img/data-viewer.png" lightbox="true" %}}

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

```
#> [1] 43808551
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
#> Warning: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
```

```
#> Records downloaded: 10
#> Records available: 4856
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1529698#3 Vulpes vulpes (Linn…  1         61.52397  24.43148
#> 2  …HR.3211/148618452-U Vulpes vulpes (Linn…        NA  60.5      21.9    
#> 3  …KE.176/63e927b8d5d… Vulpes vulpes (Linn…  1         61.52345  24.43397
#> 4  …KE.176/63e88da6d5d… Vulpes vulpes (Linn…  1         64.95278  25.53677
#> 5  …HR.3211/148628701-U Vulpes vulpes (Linn…        NA  61.51742  24.28717
#> 6         …JX.1529398#3 Vulpes vulpes (Linn…  1         60.31397  25.27919
#> 7         …JX.1529165#3 Vulpes vulpes (Linn…  1         60.42797  22.20048
#> 8  …HR.3211/148184681-U Vulpes vulpes (Linn…        NA  64.82136  25.31144
#> 9  …HR.3211/148170078-U Vulpes vulpes (Linn…        NA  60.25293  22.42181
#> 10        …JX.1526017#3 Vulpes vulpes (Linn…  1         64.93555  25.62159
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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
#> Error: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
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

```
#> Records downloaded: 10
#> Records available: 45893791
#> A data.frame [10 x 11]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 2  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 3         …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> 4  …HR.3211/148812589-U Fomitopsis pinicola…        NA  60.43726  22.37422
#> 5  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 6         …JX.1529815#3 Pteromys volans (Li…        NA  62.46923  25.94574
#> 7         …JX.1529813#6 Carduelis chloris (…  1         60.17831  24.65979
#> 8         …JX.1529813#9 Carduelis chloris (…        NA  60.17857  24.6614 
#> 9        …JX.1529813#12 Carduelis spinus (L…  1         60.1796   24.66341
#> 10        …JX.1529813#3 Passer montanus (Li…  3         60.17811  24.65902
#> ...with 0 more record and 6 more variables:
#> coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 45893791
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 2  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 3         …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> 4  …HR.3211/148812589-U Fomitopsis pinicola…        NA  60.43726  22.37422
#> 5  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 6         …JX.1529815#3 Pteromys volans (Li…        NA  62.46923  25.94574
#> 7         …JX.1529813#6 Carduelis chloris (…  1         60.17831  24.65979
#> 8         …JX.1529813#9 Carduelis chloris (…        NA  60.17857  24.6614 
#> 9        …JX.1529813#12 Carduelis spinus (L…  1         60.1796   24.66341
#> 10        …JX.1529813#3 Passer montanus (Li…  3         60.17811  24.65902
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

Or set the global timezone option to set the timezone for the current session.

```r
options(finbif_tz = "Etc/UTC")
```
This may be advisable for reproducibility or when working with multiple systems.
