---
title: Occurrence Data
draft: no
toc: yes
type: book
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

```.language-r
finbif_occurrence()
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 43808551
#> A data.frame [10 x 12]
#>    record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1      …42#3            Apus apus        NA  60.4911   22.1561 
#> 2      …41#3 Phylloscopus trochi…        NA  60.4911   22.1561 
#> 3      …39#6       Sylvia curruca  1         59.83882  19.92228
#> 4      …39#3      Sylvia communis  1         59.84056  19.91378
#> 5      …35#5      Sylvia communis  1         61.0872   23.65435
#> 6      …35#3     Saxicola rubetra  2         61.0872   23.65435
#> 7     …31#15    Charadrius dubius  4         64.83067  26.10181
#> 8     …31#11       Turdus pilaris  1         64.82108  26.01163
#> 9      …31#3   Anas platyrhynchos  14        64.82164  25.96167
#> 10     …31#7            Apus apus  30        64.80656  25.99359
#> ...with 0 more records and 7 more variables:
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

```.language-r
colnames(finbif_occurrence(dwc = TRUE))
```

```{.language-r}
#>  [1] "occurrenceID"                  "scientificName"               
#>  [3] "individualCount"               "decimalLatitude"              
#>  [5] "decimalLongitude"              "eventDateTime"                
#>  [7] "coordinateUncertaintyInMeters" "hasIssues"                    
#>  [9] "requiresVerification"          "requiresIdentification"       
#> [11] "occurrenceReliability"         "occurrenceQuality"
```

## Choosing taxa
You can limit the records to certain taxa by specifying them as an argument.

```.language-r
finbif_occurrence("Cygnus cygnus")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 80292
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1411611#18   Cygnus cygnus        NA  61.35074  27.83794
#> 2  …HR.4412/62bb91fcbd…   Cygnus cygnus        NA  60.77169  21.02729
#> 3  …HR.4412/62bb91ff5c…   Cygnus cygnus        NA  63.85516  25.26802
#> 4  …HR.4412/62bb920880…   Cygnus cygnus        NA  66.28617  26.43911
#> 5  …HR.4412/62bb921b4f…   Cygnus cygnus        NA  61.15693  24.8605 
#> 6  …HR.4412/62bb920b6a…   Cygnus cygnus        NA  61.69497  24.82332
#> 7  …HR.4412/62bb9209ce…   Cygnus cygnus        NA  60.78464  24.15072
#> 8  …HR.4412/62bb920676…   Cygnus cygnus        NA  66.09645  28.87577
#> 9  …HR.4412/62bb920db6…   Cygnus cygnus        NA  62.04549  21.35311
#> 10 …HR.4412/62bb92172a…   Cygnus cygnus        NA  65.81431  24.2622 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

Multiple taxa can be requested at once.

```.language-r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 117412
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1411611#18   Cygnus cygnus        NA  61.35074  27.83794
#> 2  …HR.4412/62bb91fcbd…   Cygnus cygnus        NA  60.77169  21.02729
#> 3  …HR.4412/62bb91ff5c…   Cygnus cygnus        NA  63.85516  25.26802
#> 4  …HR.4412/62bb920880…   Cygnus cygnus        NA  66.28617  26.43911
#> 5  …HR.4412/62bb921b4f…   Cygnus cygnus        NA  61.15693  24.8605 
#> 6  …HR.4412/62bb920b6a…   Cygnus cygnus        NA  61.69497  24.82332
#> 7  …HR.4412/62bb9209ce…   Cygnus cygnus        NA  60.78464  24.15072
#> 8  …HR.4412/62bb920676…   Cygnus cygnus        NA  66.09645  28.87577
#> 9  …HR.4412/62bb920db6…   Cygnus cygnus        NA  62.04549  21.35311
#> 10 …HR.4412/62bb92172a…   Cygnus cygnus        NA  65.81431  24.2622 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can also chose higher taxonomic groups and use common names (in English,
Finnish and Swedish).

```.language-r
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

```.language-r
occurrences <- finbif_occurrence(n = 1001)
```

You can invoke a spreadsheet-style data browser with the `View` function

```.language-r
View(occurrences)
```
When using the RStudio IDE you can also invoke the browser by clicking on the
data in the 'Environment' pane.

{{% figure library="true" src="/img/data-viewer.png" lightbox="true" %}}

When there are more than 1000 records to retrieve a progress bar will be
initiated. You can suppress the progress bar with the `quiet` argument.

```.language-r
finbif_occurrence(n = 1001, quiet = TRUE)
```

You can see how many records are available for a given request, without
retrieving any records, by setting `count_only = TRUE`.

```.language-r
finbif_occurrence(count_only = TRUE)
```

```{.language-r}
#> [1] 43808551
```

## Checking taxa
When you request occurrence records for specific taxa, by default, the taxon
names are first checked against the FinBIF database. If any of the requested
taxa are not found in the database you will receive a warning but the data will
still be retrieved for the remaining taxa.

```.language-r
finbif_occurrence("Vulpes vulpes", "Moomin")
```

```
#> Warning: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 4600
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1411439#86   Vulpes vulpes  1         67.44423  23.77218
#> 2  …HR.3211/123404764-U   Vulpes vulpes        NA  65.01624  25.60409
#> 3         …JX.1408878#3   Vulpes vulpes  1         62.30458  29.63992
#> 4  …HR.3211/123069087-U   Vulpes vulpes        NA  60.73751  24.76117
#> 5  …KE.176/62b3609cd5d…   Vulpes vulpes  2         60.11016  25.01864
#> 6         …JX.1408390#3   Vulpes vulpes  4         60.82445  21.53643
#> 7         …JX.1407814#7   Vulpes vulpes  1         62.80186  24.42096
#> 8  …HR.3211/122701464-U   Vulpes vulpes        NA  63.83883  23.15996
#> 9  …HR.3211/122682509-U   Vulpes vulpes        NA  59.93074  20.93271
#> 10 …HR.3211/122473532-U   Vulpes vulpes        NA  60.75704  24.77011
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

You can turn off taxon name pre-checking by setting the value of the
`check_taxa` argument to `FALSE`. 

```.language-r
finbif_occurrence("Vulpes vulpes", "Moomin", check_taxa = FALSE)
```

By setting the argument, `on_check_fail` to `"error"` (the default is `"warn"`),
you can elevate the warnings to errors and the request will fail if any of the
taxa are not found in the FinBIF database.

```.language-r
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

```.language-r
finbif_occurrence(select = "-date_time")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 43809442
#> A data.frame [10 x 11]
#>    record_id    scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …925586-U   Abraxas sylvatus        NA  60.21452  25.15645
#> 2  …929172-U   Adscita statices        NA  62.01821  22.96884
#> 3  …896520-U    Archips podanus        NA  60.06069  23.66039
#> 4  …929698-U    Bombus hypnorum        NA  60.91897  25.89668
#> 5  …929447-U         Brachycera        NA  62.01821  22.96884
#> 6  …921913-U          Bryophyta        NA  67.92459  23.8096 
#> 7  …892019-U Caradrina morpheus        NA  60.38722  24.75005
#> 8  …930698-U Chiasmia clathrata        NA  62.12781  27.45273
#> 9  …918736-U       Dactylorhiza        NA  67.92468  23.81718
#> 10 …918504-U Hypomecis atomaria        NA  67.92603  23.82139
#> ...with 0 more records and 6 more variables:
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

```.language-r
finbif_occurrence(date_time_method = "accurate")
```

#### Timezone output
The timezone of the calculated `date_time` variable is determined by the
timezone of your operating system.

```.language-r
Sys.timezone()
```

You can override this by setting the `tzone` argument to a different value.

```.language-r
finbif_occurrence(tzone = "Etc/UTC")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 43808551
#> A data.frame [10 x 12]
#>    record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1      …42#3            Apus apus        NA  60.4911   22.1561 
#> 2      …41#3 Phylloscopus trochi…        NA  60.4911   22.1561 
#> 3      …39#6       Sylvia curruca  1         59.83882  19.92228
#> 4      …39#3      Sylvia communis  1         59.84056  19.91378
#> 5      …35#5      Sylvia communis  1         61.0872   23.65435
#> 6      …35#3     Saxicola rubetra  2         61.0872   23.65435
#> 7     …31#15    Charadrius dubius  4         64.83067  26.10181
#> 8     …31#11       Turdus pilaris  1         64.82108  26.01163
#> 9      …31#3   Anas platyrhynchos  14        64.82164  25.96167
#> 10     …31#7            Apus apus  30        64.80656  25.99359
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

Or set the global timezone option to set the timezone for the current session.

```.language-r
options(finbif_tz = "Etc/UTC")
```
This may be advisable for reproducibility or when working with multiple systems.
