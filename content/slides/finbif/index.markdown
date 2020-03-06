---
title: Using the FinBIF R package
slides:
  theme: black
  highlight_style: atom-one-dark-reasonable
---



# Using the FinBIF R package

---

## Installation

---

### Stable version
<div class = 'fragment'>

```r
install.packages("finbif")
```

</div>

---

### Development version
<div class = 'fragment'>

```r
if (require(remotes)) install.packages("remotes")
remotes::install_github("luomus/finbif@dev")
```

</div>

---

### Previous versions
<div class = 'fragment'>

```r
remotes::install_version("finbif", "0.2.0")
```

</div>

---

### Loading the package
<div class = 'fragment'>

```r
library(finbif)
```

</div>

---

## Access token

---

### Requesting a token
<div class = 'fragment'>

```r
finbif_request_token("your@email.com")
```

</div>

---

### Setting the token
<div class = 'fragment'>

```r
Sys.setenv(
  FINBIF_ACCESS_TOKEN = "xtmSOIxjPwq0pOMB1WvcZgFLU9QBkl"
)
```

</div>

<div class = 'fragment'>

```r
cat(
  'FINBIF_ACCESS_TOKEN = "xtmSOIxjPwq0pOMB1WvcZgFLU9QBkl"',
  file = "~/.Renviron",
  append = TRUE,
  fill = TRUE
)
```

</div>

---

## Documentation

---

### Documentation in R
<div class = 'fragment'>

```r
?finbif_request_token
```

</div>
<div class = 'fragment'>

```r
help("finbif_request_token")
```

</div>
{{% fragment %}} Some important help files {{% /fragment %}}
<div class = 'fragment'>

```r
?filters
?variables
```

</div>

---

## Documentation online

---

{{< slide background-image="stable-docs.png" >}}

---

{{< slide background-image="dev-docs.png" >}}

---

{{< slide background-image="changelog.png" >}}

---

{{< slide background-image="vignettes.png" >}}

---

## Working with taxa

---

### Taxa checking
<div class = 'fragment'>

```r
(taxa <- finbif_check_taxa(c("Ursus arctos", "Moomin")))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [Ursus arctos] ID: MX.47348
#> [Moomin      ] Not found
```

</div>

<div class = 'fragment'>

```r
taxa[[1]]
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Ursus arctos 
#>   "MX.47348"
```

</div>

<div class = 'fragment'>

```r
taxa[[2]]
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Moomin 
#>     NA
```

</div>

---

### Taxa checking
<div class = 'fragment'>

```r
finbif_check_taxa(
  list(species = c("Ursus arctos", "Ursus"), genus = "Ursus")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [species: Ursus arctos] ID: MX.47348
#> [species: Ursus       ] Not found
#> [genus:   Ursus       ] ID: MX.51311
```

</div>

---

### Taxa checking
<div class = 'fragment'>

```r
taxa_list <- readLines("taxa.csv")
finbif_check_taxa(taxa_list)
```

</div>

---

## Taxa search

---

### Exact matching
<div class = 'fragment'>

```r
finbif_taxa("Capreolus capreolus")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> <FinBIF taxa/search>
#> List of 1
#>  $ :List of 12
#>   ..$ matchingName            : chr "Capreolus capreolus"
#>   ..$ nameType                : chr "MX.scientificName"
#>   ..$ id                      : chr "MX.47507"
#>   ..$ scientificName          : chr "Capreolus capreolus"
#>   ..$ scientificNameAuthorship: chr "(Linnaeus, 1758)"
#>   ..$ taxonRank               : chr "MX.species"
#>   ..$ cursiveName             : logi TRUE
#>   ..$ finnish                 : logi TRUE
#>   ..$ species                 : logi TRUE
#>   ..$ vernacularName          :List of 3
#>   .. ..$ en: chr "Roe Deer"
#>   .. ..$ fi: chr "metsäkauris"
#>   .. ..$ sv: chr "rådjur"
#>   ..$ informalGroups          :List of 1
#>   .. ..$ :List of 2
#>   .. .. ..$ id  : chr "MVL.2"
#>   .. .. ..$ name:List of 3
#>   .. .. .. ..$ sv: chr "Däggdjur"
#>   .. .. .. ..$ fi: chr "Nisäkkäät"
#>   .. .. .. ..$ en: chr "Mammals"
#>   ..$ type                    : chr "exactMatches"
```

</div>

---

### Partial matching
<div class = 'fragment'>

```r
deer <- finbif_taxa("deer", type = "partial", n = 10)
sapply(deer$content, getElement, "scientificName")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>  [1] "Dama dama"                "Capreolus capreolus"     
#>  [3] "Odocoileus virginianus"   "Rangifer tarandus"       
#>  [5] "Hippuriphila modeeri"     "Pseudombrophila merdaria"
#>  [7] "Odocoileus"               "Cervidae"                
#>  [9] "Dama"                     "Capreolus"
```

</div>

---

## Occurrence data

---

### Requesting occurrence records
<div class = 'fragment'>

```r
finbif_occurrence()
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 34498669
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Propolis farinosa         1  60.44131  22.36936 2020-03-06 12:00:00
#> 2    Dendrocopos major         2  60.44080  22.36923 2020-03-06 12:00:00
#> 3  Garrulus glandarius         7  60.44080  22.36923 2020-03-06 12:00:00
#> 4     Columba palumbus         1  60.44080  22.36923 2020-03-06 12:00:00
#> 5          Parus major         4  60.44080  22.36923 2020-03-06 12:00:00
#> 6        Corvus corone        16  60.44098  22.37359 2020-03-06 12:00:00
#> 7            Pica pica        17  60.91134  25.71562 2020-03-06 08:45:00
#> 8          Picus canus         1  60.91134  25.71562 2020-03-06 08:45:00
#> 9      Regulus regulus        11  60.91134  25.71562 2020-03-06 08:45:00
#> 10    Poecile montanus         2  60.91134  25.71562 2020-03-06 08:45:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Darwin Core Variables
<div class = 'fragment'>

```r
colnames(finbif_occurrence(dwc = TRUE))
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Choosing taxa
<div class = 'fragment'>

```r
finbif_occurrence("Cygnus cygnus")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 56334
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         6  60.91134  25.71562 2020-03-06 08:45:00
#> 2    Cygnus cygnus        32  60.47600  22.02122 2020-03-06 07:40:00
#> 3    Cygnus cygnus         1  62.64896  29.67029 2020-03-06 12:00:00
#> 4    Cygnus cygnus         1  62.32117  21.73212 2020-03-06 12:00:00
#> 5    Cygnus cygnus         2  61.20897  24.23909 2020-03-05 08:39:00
#> 6    Cygnus cygnus        15  61.15112  21.71506 2020-03-05 09:00:00
#> 7    Cygnus cygnus        27  61.22514  21.96610 2020-03-05 07:10:00
#> 8    Cygnus cygnus         1  60.15059  24.94896 2020-03-05 12:00:00
#> 9    Cygnus cygnus         1  60.90278  22.71329 2020-03-05 12:00:00
#> 10   Cygnus cygnus         5  65.67320  24.54981 2020-03-04 08:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Choosing taxa
<div class = 'fragment'>

```r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 80575
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         6  60.91134  25.71562 2020-03-06 08:45:00
#> 2      Cygnus olor         4  60.47600  22.02122 2020-03-06 07:40:00
#> 3    Cygnus cygnus        32  60.47600  22.02122 2020-03-06 07:40:00
#> 4    Cygnus cygnus         1  62.64896  29.67029 2020-03-06 12:00:00
#> 5    Cygnus cygnus         1  62.32117  21.73212 2020-03-06 12:00:00
#> 6      Cygnus olor         1  59.83427  23.08354 2020-03-05 12:00:00
#> 7    Cygnus cygnus         2  61.20897  24.23909 2020-03-05 08:39:00
#> 8    Cygnus cygnus        15  61.15112  21.71506 2020-03-05 09:00:00
#> 9    Cygnus cygnus        27  61.22514  21.96610 2020-03-05 07:10:00
#> 10     Cygnus olor        17  60.46486  22.35936 2020-03-05 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Choosing taxa
<div class = 'fragment'>

```r
birds  <- finbif_occurrence("Birds")
linnut <- finbif_occurrence("Linnut")
faglar <- finbif_occurrence("Fåglar")

sapply(list(birds, linnut, faglar), nrow)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 10 10 10
```

</div>

---

### Request size
<div class = 'fragment'>

```r
occurrences <- finbif_occurrence(n = 1001)
```

</div>

---

### Data viewer
<div class = 'fragment'>

```r
View(occurrences)
```

</div>

{{< figure library="true" src="data-viewer.png" lightbox="true" class="fragment" >}}

---

{{< figure library="true" src="viewer-occurrence.png" >}}

---

### Suppress progress bar
<div class = 'fragment'>

```r
finbif_occurrence(n = 1001, quiet = TRUE)
```

</div>

---

### Count records
<div class = 'fragment'>

```r
finbif_occurrence(count_only = TRUE)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 34498669
```

</div>

---

### Checking taxa
<div class = 'fragment'>

```r
finbif_occurrence("Vulpes vulpes", "Moomin")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Warning: Cannot find taxa: Moomin
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Without checking
<div class = 'fragment'>

```r
finbif_occurrence(
  "Vulpes vulpes", "Moomin", check_taxa = FALSE
)
```

</div>

---

### Failing with error
<div class = 'fragment'>

```r
finbif_occurrence(
  "Vulpes vulpes", "Moomin", on_check_fail = "error"
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Error: Cannot find taxa: Moomin
```

</div>

---

## Time & duration

---

### Compute date & time
<div class = 'fragment'>

```r
finbif_occurrence(date_time = FALSE)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 34498669
#> A data.frame [10 x 28]
#>        scientific_name abundance lat_wgs84 lon_wgs84 taxon_rank
#> 1    Propolis farinosa         1  60.44131  22.36936 MX.species
#> 2    Dendrocopos major         2  60.44080  22.36923 MX.species
#> 3  Garrulus glandarius         7  60.44080  22.36923 MX.species
#> 4     Columba palumbus         1  60.44080  22.36923 MX.species
#> 5          Parus major         4  60.44080  22.36923 MX.species
#> 6        Corvus corone        16  60.44098  22.37359 MX.species
#> 7            Pica pica        17  60.91134  25.71562 MX.species
#> 8          Picus canus         1  60.91134  25.71562 MX.species
#> 9      Regulus regulus        11  60.91134  25.71562 MX.species
#> 10    Poecile montanus         2  60.91134  25.71562 MX.species
#> ...with 0 more records and 23 more variables:
#> country, province, municipality, date_start, date_end, hour_start,
#> hour_end, minute_start, minute_end, record_id, individual_id,
#> event_id, collection_id, any_issues, record_issue, record_reliable,
#> taxon_reliability, document_issue, collection_reliability,
#> coordinates_uncertainty, event_issue, location_issue, time_issue
```

</div>

---

## Timezones

---

### Timezone input
<div class = 'fragment'>

```r
finbif_occurrence(date_time_method = "accurate")
```

</div>

---

### Timezone output
<div class = 'fragment'>

```r
Sys.timezone()
```

</div>
<div class = 'fragment'>

```r
finbif_occurrence(tzone = "Etc/UTC")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 34498669
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Propolis farinosa         1  60.44131  22.36936 2020-03-06 10:00:00
#> 2    Dendrocopos major         2  60.44080  22.36923 2020-03-06 10:00:00
#> 3  Garrulus glandarius         7  60.44080  22.36923 2020-03-06 10:00:00
#> 4     Columba palumbus         1  60.44080  22.36923 2020-03-06 10:00:00
#> 5          Parus major         4  60.44080  22.36923 2020-03-06 10:00:00
#> 6        Corvus corone        16  60.44098  22.37359 2020-03-06 10:00:00
#> 7            Pica pica        17  60.91134  25.71562 2020-03-06 06:45:00
#> 8          Picus canus         1  60.91134  25.71562 2020-03-06 06:45:00
#> 9      Regulus regulus        11  60.91134  25.71562 2020-03-06 06:45:00
#> 10    Poecile montanus         2  60.91134  25.71562 2020-03-06 06:45:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Set timezone
<div class = 'fragment'>

```r
options(finbif_tz = "Etc/UTC")
```

</div>

---

## Selecting & ordering variables

---

### Variables help page
<div class = 'fragment'>

```r
?variables
```

</div>

---

{{< slide background-image="variables-help.png" >}}

---

## Selecting variables

---

### Limiting Variables
<div class = 'fragment'>

```r
finbif_occurrence(
  genus  = "Falco",
  select = c("scientific_name", "life_stage", "sex")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 280298
#> A data.frame [10 x 3]
#>      scientific_name life_stage  sex
#> 1  Falco columbarius       <NA> <NA>
#> 2  Falco tinnunculus       <NA> <NA>
#> 3  Falco tinnunculus       <NA> <NA>
#> 4  Falco tinnunculus       <NA> <NA>
#> 5  Falco columbarius       <NA> MALE
#> 6  Falco tinnunculus       <NA> <NA>
#> 7  Falco columbarius       <NA> <NA>
#> 8  Falco columbarius       <NA> <NA>
#> 9  Falco tinnunculus       <NA> <NA>
#> 10 Falco columbarius       <NA> <NA>
```

</div>

---

### Extra variables
<div class = 'fragment'>

```r
finbif_occurrence(select = c("default_vars", "life_stage"))
```

</div>

---

## Ordering

---

### Ascending order
<div class = 'fragment'>

```r
finbif_occurrence("Cygnus cygnus", order_by = "abundance")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 56334
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         1  60.41667  16.00000 1997-04-01 13:00:00
#> 2    Cygnus cygnus         1  63.37022  30.37826                <NA>
#> 3    Cygnus cygnus         1  61.08200  27.78355 2017-04-08 12:00:00
#> 4    Cygnus cygnus         1  52.71667   1.55000 1997-01-03 14:00:00
#> 5    Cygnus cygnus         1  61.21489  23.36719 2006-06-12 12:00:00
#> 6    Cygnus cygnus         1  61.80000  22.76667 2000-03-22 12:00:00
#> 7    Cygnus cygnus         1  63.13333  22.43333 2003-06-07 12:00:00
#> 8    Cygnus cygnus         1  61.72481  24.17242                <NA>
#> 9    Cygnus cygnus         1  60.23968  25.79487                <NA>
#> 10   Cygnus cygnus         1  62.27627  23.59633 1994-04-30 19:50:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Descending order
<div class = 'fragment'>

```r
finbif_occurrence("Cygnus cygnus", order_by = "-abundance")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 56334
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus      6000  64.40000 -14.54000 1995-07-05 15:00:00
#> 2    Cygnus cygnus      2010  64.54597  27.88859 2010-01-01 12:00:00
#> 3    Cygnus cygnus      1500        NA        NA 2003-04-18 15:00:00
#> 4    Cygnus cygnus      1200        NA        NA 2003-04-16 15:00:00
#> 5    Cygnus cygnus      1064  62.50172  21.33260 2017-11-04 08:40:00
#> 6    Cygnus cygnus       722  60.97170  26.48918 2012-11-04 09:00:00
#> 7    Cygnus cygnus       673  60.76462  26.09601 2012-11-07 08:00:00
#> 8    Cygnus cygnus       645  64.84588  25.62653 2005-11-05 12:00:00
#> 9    Cygnus cygnus       645  64.84588  25.62653 2005-11-05 09:00:00
#> 10   Cygnus cygnus       641  62.27627  23.59633 2008-11-20 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Multiple variables
<div class = 'fragment'>

```r
finbif_occurrence(
  "Cygnus olor", order_by = c("municipality", "-abundance")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 24241
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Cygnus olor         4  61.13908  23.93331 2007-11-04 09:00:00
#> 2      Cygnus olor         3  61.13908  23.93331 1990-11-04 09:00:00
#> 3      Cygnus olor         3  61.22435  23.73872 1990-11-14 11:00:00
#> 4      Cygnus olor         2  61.16607  23.91207 2013-11-09 08:30:00
#> 5      Cygnus olor         1  61.22435  23.73872 2007-03-01 10:00:00
#> 6      Cygnus olor         4  61.13908  23.93331 2007-11-04 12:00:00
#> 7      Cygnus olor         6  61.22870  23.92458 2002-11-01 12:00:00
#> 8      Cygnus olor         3  61.22870  23.92458 2000-12-22 12:00:00
#> 9      Cygnus olor         1  61.22870  23.92458 2006-03-11 12:00:00
#> 10     Cygnus olor         1  61.22870  23.92458 2010-05-11 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Random sample
<div class = 'fragment'>

```r
finbif_occurrence(sample = TRUE)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 34498669
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Carex rupestris         1  69.04206  20.86432 1986-07-12 13:00:00
#> 2     Fringilla coelebs         1  60.28486  25.37444 2001-05-29 09:00:00
#> 3     Veronica arvensis         1  62.87703  27.68462 1962-06-11 12:00:00
#> 4   Aegithalos caudatus         1  60.35096  25.35010 2008-05-11 12:00:00
#> 5     Fringilla coelebs         1  63.20933  27.75193 2008-06-12 04:10:00
#> 6       Lanius collurio         9  59.81111  22.89545 1979-07-21 12:00:00
#> 7       Chloris chloris         1  60.40857  22.35546 2006-03-24 09:00:00
#> 8   Lysimachia europaea         1  68.07695  25.91646 1960-01-01 12:00:00
#> 9  Cnephasia stephensi…         1  60.04611  19.97402 2019-07-15 12:00:00
#> 10         Viola canina         1  60.47106  22.54057 1958-12-31 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

## Metadata

---

### General metadata
<div class = 'fragment'>

```r
finbif_metadata()
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>    metadata_name            
#> 1  admin_status             
#> 2  red_list                 
#> 3  countries                
#> 4  provinces                
#> 5  municipalities           
#> 6  bird_assoc_areas         
#> 7  finnish_occurrence_status
#> 8  habitat_types            
#> 9  habitat_qualifiers       
#> 10 life_stages              
#> 11 record_basis             
#> 12 restriction_levels       
#> 13 restriction_reasons      
#> 14 sex_categories           
#> 15 sources                  
#> 16 taxon_ranks
```

</div>

---

### General metadata
<div class = 'fragment'>

```r
finbif_metadata("red_list")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>    status_name           status_code
#> 1  Critically Endangered CR         
#> 2  Data Deficient        DD         
#> 3  Endangered            EN         
#> 4  Extinct               EX         
#> 5  Extinct in the Wild   EW         
#> 6  Least Concern         LC         
#> 7  Near Threatened       NT         
#> 8  Not Applicable        NA         
#> 9  Not Evaluated         NE         
#> 10 Regionally Extinct    RE         
#> 11 Vulnerable            VU
```

</div>

---

## Special metadata

---

### Informal groups
<div class = 'fragment'>

```r
finbif_informal_groups(limit = 6)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Algae                                                         
#>  °--Macro algae                                               
#>      ¦--Brown algae and yellow green algae                    
#>      ¦--Green algae                                           
#>      ¦--Red algae                                             
#>      °--Stoneworts                                            
#> ...111 more groups
```

</div>

---

### Informal groups
<div class = 'fragment'>

```r
finbif_informal_groups("Crustaceans")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Crustaceans                                                   
#>  ¦--Macrocrustaceans                                          
#>  ¦   ¦--Amphipods, isopods, opossum shrimps                   
#>  ¦   ¦--Crabs, shrimps and crayfishes                         
#>  ¦   ¦--Other macrocrustaceans                                
#>  ¦   °--Woodlice                                              
#>  °--Microcrustaceans                                          
#>      ¦--Branchiopoda                                          
#>      ¦--Copepods                                              
#>      °--Seed shrimps
```

</div>

---

### Collections
<div class = 'fragment'>

```r
finbif_collections(
  filter = geographic_coverage == "Finland",
  select = 
    c("collection_name", "taxonomic_coverage", "count")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>         collection_name            taxonomic_coverage         count  
#> HR.1227 Coll Mikko Heikkinen       Biota                           61
#> HR.1349 JYV - Fungal collections   <NA>                         13398
#> HR.1350 JYV - Lichen collections   <NA>                           398
#> HR.1351 JYV - Bryophyte collectio… <NA>                          3227
#> HR.1467 Per-Eric Grankvist´s butt… Lepidoptera                      5
#> HR.1487 JYV - Fish collections     <NA>                          1371
#> HR.1507 Lingonblad Birger och Hjö… Lepidoptera                   2797
#> HR.1592 Herbarium of The Ark Natu… <NA>                          1287
#> HR.1687 Papilionoidea of Coll. La… Papilionoidea                  525
#> HR.1688 Noctuidae I of Coll. Lauro Noctuidae                      614
#> HR.1689 Noctuidae II of Coll. Lau… Noctuidae                      839
#> HR.1690 Noctuidae III, Bombycoide… Noctuidae, Bombycoidea, G…     521
#> HR.1691 Drepanidae & Geometridae … Drepanidae, Geometridae       1408
#> HR.175  National Finnish butterfl… Lepidoptera                 349461
#> HR.200  Finnish Insect Database    Insecta                    3728982
#> HR.2049 Invasive alien species co… Invasive species                93
#> HR.206  The Finnish Nature League… biota                        82268
#> HR.2089 Håkan Lindberg collection  Hymenoptera                   2295
#> HR.209  Atlas of Finnish Macrolep… Macrolepidoptera           1217383
#> HR.2209 KUO Arachnida collection   Arachnida                        3
#> HR.2289 Specimens that lack colle… <NA>                           109
#> HR.2691 Line transect censuses of… Aves                        588124
#> HR.2692 Censuses of breeding bird… Aves                         14963
#> HR.3051 Viekas project invasive s… <NA>                           647
#> HR.3071 Observing species on milk… <NA>                           160
#> HR.3211 iNaturalist                <NA>                         15716
#> HR.39   Winter Bird Census         Aves                       1358747
#> HR.435  Löydös Open Invasive Spec… Biota                        11668
#> HR.60   Monitoring scheme of bird… Aves, Mammalia              769290
#> HR.627  Invasive mammal species o… Mammalia                       228
#> HR.808  E. Sjöholm´s butterfly co… Lepidoptera                   4952
#> HR.847  Atlas of amphibians and r… Amphibia, Reptilia            5106
```

</div>

---

### Collections
<div class = 'fragment'>

```r
collections <- 
  finbif_collections(supercollections = TRUE, nmin = 10000)
View(collections)
```

</div>
<div class = 'fragment'>

```r
finbif_collections(
  supercollections = TRUE
)["HR.128", "collection_name"]
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] "Collections of the Finnish Museum of Natural History Luomus"
```

</div>

---

### Collections
<div class = 'fragment'>

```r
finbif_collections(
  is_part_of == "HR.128", supercollections = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>        collection_name abbreviation description online_url has_children
#> HR.129 Collections of… H            Herbarium … <NA>        TRUE       
#> HR.160 Zoological col… MZH          The collec… http://ww…  TRUE       
#> HR.173 Zoological mon… <NA>         Monitoring… <NA>        TRUE       
#> HR.203 Löydös Open Fi… <NA>         A service … http://ws…  TRUE       
#> HR.447 Hatikka.fi obs… <NA>         Hatikka.fi… http://ha… FALSE       
#> HR.48  Ringing and re… TIPU         Database o… <NA>        TRUE       
#>        is_part_of data_quality methods collection_type taxonomic_coverage
#> HR.129 HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#> HR.160 HR.128     MY.dataQual… NA      MY.collectionT… Animalia          
#> HR.173 HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#> HR.203 HR.128     MY.dataQual… NA      MY.collectionT… biota             
#> HR.447 HR.128     MY.dataQual… NA      MY.collectionT… Biota             
#> HR.48  HR.128     MY.dataQual… NA      MY.collectionT… <NA>              
#>        geographic_coverage temporal_coverage secure_level count   
#> HR.129 <NA>                <NA>              <NA>             1512
#> HR.160 World               1700 to present   MX.secureLe…      957
#> HR.173 Finland             1950-             <NA>          4134497
#> HR.203 world               2013-             <NA>            14383
#> HR.447 World               <NA>              <NA>          2012954
#> HR.48  Ringing data: Finl… 1913-             <NA>         11915364
```

</div>

---

## Filtering Occurrence Data

---

### Filtering help
<div class = 'fragment'>

```r
?filters
```

</div>

---

{{< slide background-image="filtering-help.png" >}}

---

## Location

---

### Places
<div class = 'fragment'>

```r
finbif_occurrence(filter = c(country = "Finland"))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 32657435
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Propolis farinosa         1  60.44131  22.36936 2020-03-06 12:00:00
#> 2    Dendrocopos major         2  60.44080  22.36923 2020-03-06 12:00:00
#> 3  Garrulus glandarius         7  60.44080  22.36923 2020-03-06 12:00:00
#> 4     Columba palumbus         1  60.44080  22.36923 2020-03-06 12:00:00
#> 5          Parus major         4  60.44080  22.36923 2020-03-06 12:00:00
#> 6        Corvus corone        16  60.44098  22.37359 2020-03-06 12:00:00
#> 7            Pica pica        17  60.91134  25.71562 2020-03-06 08:45:00
#> 8          Picus canus         1  60.91134  25.71562 2020-03-06 08:45:00
#> 9      Regulus regulus        11  60.91134  25.71562 2020-03-06 08:45:00
#> 10    Poecile montanus         2  60.91134  25.71562 2020-03-06 08:45:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Coordinates
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(
    coordinates = list(
      lat = c(60, 68), lon = c(20, 30), system = "wgs84"
    )
  )
)
```

</div>

---

### Dates
<div class = 'fragment'>

```r
finbif_occurrence(filter = c(date_range_ymd = "2019-12"))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 7995
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Clavulinopsis luteo…         1  60.43100  22.28100 2019-12-31 12:00:00
#> 2            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 3      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 5    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 6             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 8   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 9          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 10    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Dates
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(
    date_range_ymd = c("2019-06-01", "2019-12-31")
  )
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 344568
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Clavulinopsis luteo…         1  60.43100  22.28100 2019-12-31 12:00:00
#> 2            Flammulina        10  60.39362  25.67044 2019-12-31 12:00:00
#> 3      Panellus ringens         1  63.06800  21.69020 2019-12-31 12:00:00
#> 4  Basidioradulum radu…         1  63.06800  21.69020 2019-12-31 12:00:00
#> 5    Sarcosoma globosum         1  60.28506  21.98599 2019-12-31 12:00:00
#> 6             Pica pica         3  62.21189  21.66492 2019-12-31 09:54:00
#> 7      Poecile montanus         4  62.21189  21.66492 2019-12-31 09:54:00
#> 8   Emberiza citrinella        16  62.21189  21.66492 2019-12-31 09:54:00
#> 9          Corvus corax         1  62.21189  21.66492 2019-12-31 09:54:00
#> 10    Dendrocopos major         5  62.21189  21.66492 2019-12-31 09:54:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Dates
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(
    date_range_md = c(begin = "12-21", end = "12-31"),
    date_range_md = c(begin = "01-01", end = "02-20")
  )
)
```

</div>

---

### Data quality
<div class = 'fragment'>

```r
strict <- c(
  collection_reliability      = 5,
  coordinates_uncertainty_max = 1,
  taxon_reliability           = "reliable"
)
```

</div>
<div class = 'fragment'>

```r
permissive <- c(quality_issues = "both")
```

</div>
<div class = 'fragment'>

```r
c(
  strict = finbif_occurrence(
    filter = strict, count_only = TRUE
  ),
  permissive = finbif_occurrence(
    filter = permissive, count_only = TRUE
  )
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>     strict permissive 
#>     307655   34735148
```

</div>

---

### Collections
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = c(collection = "iNaturalist"),
  count_only = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 15716
```

</div>
<div class = 'fragment'>

```r
collections <- finbif_collections(
  filter = geographic_coverage == "Finland",
  nmin   = 10000
)
finbif_occurrence(
  filter = list(collection = collections),
  count_only = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 8150000
```

</div>

---

### Informal groups
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(informal_group = "Reptiles and amphibians")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 30489
#> A data.frame [10 x 30]
#>     scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Zootoca vivipara         1  60.60121  21.67021 2020-02-28 12:00:00
#> 2   Anguis fragilis         1  59.96766  24.39325 2020-02-22 12:00:00
#> 3   Anguis fragilis         1  62.25426  25.13755 2020-02-21 12:00:00
#> 4  Zootoca vivipara         1  60.26828  24.89337 2020-02-17 12:00:00
#> 5         Bufo bufo         1  60.23152  24.98346 2020-01-15 18:00:00
#> 6   Anguis fragilis         1  60.23968  25.79487 2020-01-04 18:00:00
#> 7         Bufo bufo         1  61.08603  26.86767 2020-01-03 14:53:00
#> 8        Lacertidae         1  28.14624 -16.43370 2019-12-04 13:00:00
#> 9        Lacertidae         1  28.13532 -16.44389 2019-12-04 13:00:00
#> 10        Bufo bufo         1  60.89002  24.69797 2019-10-18 10:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

## Taxon status

---

### Administrative status
<div class = 'fragment'>

```r
finbif_occurrence(
  "birds",
  filter = list(administrative_status = "EU_INVSV")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 437
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Alopochen aegyptiaca         3  52.16081  4.485534 2019-10-23 13:00:00
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

</div>

---

### Red list
<div class = 'fragment'>

```r
finbif_occurrence(
  "mammals", filter = list(red_list_status = "NT")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 1648
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Rangifer tarandus f…         5  63.83774  29.16123 2020-02-29 09:18:00
#> 2  Rangifer tarandus f…         4  64.42648  29.11431 2019-10-20 12:00:00
#> 3  Rangifer tarandus f…         1  64.09919  29.40356 2019-09-23 12:00:00
#> 4  Rangifer tarandus f…         1  63.79309  29.51080 2019-09-13 12:00:00
#> 5  Rangifer tarandus f…         1  63.93649  29.59252 2019-07-26 12:00:00
#> 6  Rangifer tarandus f…         2  63.27123  25.35634 2019-06-28 12:00:00
#> 7  Rangifer tarandus f…         1  63.26554  25.36645 2019-06-28 12:00:00
#> 8  Rangifer tarandus f…         4  63.03293  24.32905 2019-06-13 12:00:00
#> 9  Rangifer tarandus f…         1  64.32293  26.69975 2019-05-27 12:00:00
#> 10 Rangifer tarandus f…         1  63.54897  24.54795 2019-05-18 12:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Finnish occurrence
<div class = 'fragment'>

```r
finbif_occurrence(
  filter = c(finnish_occurrence_status = "rare")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 260151
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1   Galerucella pusilla         1  61.71399  29.39042 2020-03-03 16:12:00
#> 2  Olisthopus rotundat…         1  60.35368  22.36139 2020-02-24 12:00:00
#> 3  Dromius quadrimacul…         1  60.29779  22.40343 2020-02-22 12:00:00
#> 4  Otiorhynchus sulcat…         1  60.82156  21.57260 2020-02-20 12:00:00
#> 5  Dromius quadrimacul…         1  60.29790  22.39917 2020-02-20 12:00:00
#> 6  Dromius quadrimacul…         1  60.29713  22.39969 2020-02-20 12:00:00
#> 7    Hylesinus crenatus         1  60.29713  22.39969 2020-02-20 12:00:00
#> 8   Conistra rubiginosa         4  60.45842  22.17823 2020-02-17 12:00:00
#> 9    Oenopia conglobata         1  61.71205  29.39218 2020-02-13 15:36:00
#> 10   Oenopia conglobata         1  61.71378  29.39089 2020-02-12 18:52:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

</div>

---

### Finnish occurrence (negation)
<div class = 'fragment'>

```r
finbif_occurrence(
  "Birds",
  filter = c(
    finnish_occurrence_status_neg = "stable",
    taxon_rank = "species"
  )
)
```

</div>

---

## Plotting

---

### Occurrence points
<div class = 'fragment'>

```r
recent_obs <- finbif_occurrence(
  filter = c(country = "Finland"), n = 1000
)
```

</div>

---

### Occurrence points
<div class = 'fragment'>

```r
plot(recent_obs)
```

</div>
<div class = 'fragment output'> <img src="/slides/finbif/index_files/figure-html/plot-points-1.png" width="672" /></div>

---

## Occurrence density

---

### Data
<div class = 'fragment'>

```r
jays <- finbif_occurrence(
  "Eurasian Jay",
  filter = c(
    coordinates_uncertainty_max = 100, country = "Finland"
  ),
  select = c("lon_wgs84", "lat_wgs84"),
  n = 2e4
)
```

</div>

---

### Breakpoints
<div class = 'fragment'>

```r
finland_map$bbox
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 19 59 32 71
```

</div>
<div class = 'fragment'>

```r
(breaks <- breaks_xy(finland_map$bbox, size = .25))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> $x
#>  [1] 19.00 19.25 19.50 19.75 20.00 20.25 20.50 20.75 21.00 21.25 21.50 21.75
#> [13] 22.00 22.25 22.50 22.75 23.00 23.25 23.50 23.75 24.00 24.25 24.50 24.75
#> [25] 25.00 25.25 25.50 25.75 26.00 26.25 26.50 26.75 27.00 27.25 27.50 27.75
#> [37] 28.00 28.25 28.50 28.75 29.00 29.25 29.50 29.75 30.00 30.25 30.50 30.75
#> [49] 31.00 31.25 31.50 31.75 32.00
#> 
#> $y
#>  [1] 59.00 59.25 59.50 59.75 60.00 60.25 60.50 60.75 61.00 61.25 61.50 61.75
#> [13] 62.00 62.25 62.50 62.75 63.00 63.25 63.50 63.75 64.00 64.25 64.50 64.75
#> [25] 65.00 65.25 65.50 65.75 66.00 66.25 66.50 66.75 67.00 67.25 67.50 67.75
#> [37] 68.00 68.25 68.50 68.75 69.00 69.25 69.50 69.75 70.00 70.25 70.50 70.75
#> [49] 71.00
```

</div>

---

### 2d histogram
<div class = 'fragment'>

```r
jay_density <- hist_xy(jays, breaks)
```

</div>

---

### Image
<div class = 'fragment'>

```r
image(
  jay_density,
  asp    = 2.4,
  breaks = 2^seq(0, 12),
  col    = hcl.colors(12, rev = TRUE),
  xlab   = "Longitude",
  ylab   = "Latitude",
  las    = 1,
  panel.first = grid()
)
```

</div>

---

### Legend
<div class = 'fragment'>

```r
legend(
  "topright",
  inset  = c(0, .01),
  legend = expression(2^12, "", "", 2^6, "", "", 2^0),
  fill   = hcl.colors(7),
  border = NA,
  bty    = "n",
  adj    = c(0, 0.25),
  x.intersp = .2,
  y.intersp = .5
)
```

</div>

---

### Border
<div class = 'fragment'>

```r
polygon(finland_map$vertices, lwd = .2)
```

</div>
<div class = 'fragment output'> <img src="/slides/finbif/index_files/figure-html/plot-finland-1.png" width="672" /></div>

---

## Reproduciblity & Caching

---

### Reproduciblity
<div class = 'fragment'>

```r
remotes::install_version("finbif", "0.2.0")
options(finbif_tz = "Europe/Helsinki")
```

</div>

---

## Caching

---

### Cache on/off
<div class = 'fragment'>

```r
finbif_occurrence(cache = FALSE)
```

</div>
<div class = 'fragment'>

```r
options(finbif_use_cache = FALSE)
```

</div>

---

### Cache on disk
<div class = 'fragment'>

```r
options(finbif_cache_path = tempdir())
```

</div>
<div class = 'fragment'>

```r
dir.create("cache")
options(finbif_cache_path = "cache")
```

</div>

---

### Clear cache
<div class = 'fragment'>

```r
finbif_clear_cache()
```

</div>

---

# FIN
