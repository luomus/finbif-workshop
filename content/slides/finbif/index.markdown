---
title: FinBIF R Workshop
slides:
  theme: black
  highlight_style: atom-one-dark-reasonable
---



# FinBIF R Workshop

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

## Loading the package
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

## Documentation in R

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

### Documentation online

---

{{< slide background-image="stable-docs.png" >}}

---

{{< slide background-image="dev-docs.png" >}}

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

### Taxa search

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
#>   .. ..$ sv: chr "rådjur"
#>   .. ..$ en: chr "Roe Deer"
#>   .. ..$ fi: chr "metsäkauris"
#>   ..$ informalGroups          :List of 1
#>   .. ..$ :List of 2
#>   .. .. ..$ id  : chr "MVL.2"
#>   .. .. ..$ name:List of 3
#>   .. .. .. ..$ fi: chr "Nisäkkäät"
#>   .. .. .. ..$ en: chr "Mammals"
#>   .. .. .. ..$ sv: chr "Däggdjur"
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
#> Records available: 34492501
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Pica pica        34  62.95217  28.56273 2020-03-04 07:45:00
#> 2     Poecile montanus         2  62.95217  28.56273 2020-03-04 07:45:00
#> 3  Emberiza citrinella        11  62.95217  28.56273 2020-03-04 07:45:00
#> 4         Corvus corax         2  62.95217  28.56273 2020-03-04 07:45:00
#> 5    Dendrocopos major         4  62.95217  28.56273 2020-03-04 07:45:00
#> 6      Corvus monedula        44  62.95217  28.56273 2020-03-04 07:45:00
#> 7      Passer montanus        24  62.95217  28.56273 2020-03-04 07:45:00
#> 8    Pyrrhula pyrrhula         4  62.95217  28.56273 2020-03-04 07:45:00
#> 9  Cyanistes caeruleus        61  62.95217  28.56273 2020-03-04 07:45:00
#> 10         Parus major        64  62.95217  28.56273 2020-03-04 07:45:00
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

## Data viewer
<div class = 'fragment'>

```r
View(occurrences)
```

</div>

{{< figure library="true" src="data-viewer.png" lightbox="true" class="fragment" >}}

---

{{< slide background-image="viewer-occurrence.png" >}}

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
#> [1] 34492501
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
#> Records available: 34492501
#> A data.frame [10 x 28]
#>        scientific_name abundance lat_wgs84 lon_wgs84 taxon_rank
#> 1            Pica pica        34  62.95217  28.56273 MX.species
#> 2     Poecile montanus         2  62.95217  28.56273 MX.species
#> 3  Emberiza citrinella        11  62.95217  28.56273 MX.species
#> 4         Corvus corax         2  62.95217  28.56273 MX.species
#> 5    Dendrocopos major         4  62.95217  28.56273 MX.species
#> 6      Corvus monedula        44  62.95217  28.56273 MX.species
#> 7      Passer montanus        24  62.95217  28.56273 MX.species
#> 8    Pyrrhula pyrrhula         4  62.95217  28.56273 MX.species
#> 9  Cyanistes caeruleus        61  62.95217  28.56273 MX.species
#> 10         Parus major        64  62.95217  28.56273 MX.species
#> ...with 0 more records and 23 more variables:
#> country, province, municipality, date_start, date_end, hour_start,
#> hour_end, minute_start, minute_end, record_id, individual_id,
#> event_id, collection_id, any_issues, record_issue, record_reliable,
#> taxon_reliability, document_issue, collection_reliability,
#> coordinates_uncertainty, event_issue, location_issue, time_issue
```

</div>

---

### Timezone

---

#### Timezone input
<div class = 'fragment'>

```r
finbif_occurrence(date_time_method = "accurate")
```

</div>

---

#### Timezone output

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
#> Records available: 34492501
#> A data.frame [10 x 30]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1            Pica pica        34  62.95217  28.56273 2020-03-04 05:45:00
#> 2     Poecile montanus         2  62.95217  28.56273 2020-03-04 05:45:00
#> 3  Emberiza citrinella        11  62.95217  28.56273 2020-03-04 05:45:00
#> 4         Corvus corax         2  62.95217  28.56273 2020-03-04 05:45:00
#> 5    Dendrocopos major         4  62.95217  28.56273 2020-03-04 05:45:00
#> 6      Corvus monedula        44  62.95217  28.56273 2020-03-04 05:45:00
#> 7      Passer montanus        24  62.95217  28.56273 2020-03-04 05:45:00
#> 8    Pyrrhula pyrrhula         4  62.95217  28.56273 2020-03-04 05:45:00
#> 9  Cyanistes caeruleus        61  62.95217  28.56273 2020-03-04 05:45:00
#> 10         Parus major        64  62.95217  28.56273 2020-03-04 05:45:00
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

#### Set timezone
<div class = 'fragment'>

```r
options(finbif_tz = "Etc/UTC")
```

</div>
