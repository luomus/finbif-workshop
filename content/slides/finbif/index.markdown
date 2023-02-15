---
title: Using the FinBIF R package
slides:
  theme: black
  highlight_style: github-dark
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
if (!require(remotes)) install.packages("remotes")
remotes::install_github("luomus/finbif@dev")
```

</div>

---

### Previous versions

<div class = 'fragment'>

```r
remotes::install_version("finbif", "0.6.0")
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

```
#> [Ursus arctos] ID: MX.47348
#> [Moomin] Not found
```

</div>

<div class = 'fragment'>

```r
taxa[[1]]
```

</div>
<div class = 'fragment output'> 

```
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

```
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

```
#> [species: Ursus arctos] ID: MX.47348
#> [species: Ursus  ] Not found
#> [genus:   Ursus  ] ID: MX.51311
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

```
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
#>   .. ..$ fi: chr "metsäkauris"
#>   .. ..$ en: chr "Roe Deer"
#>   .. ..$ sv: chr "rådjur"
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

```
#>  [1] "Odocoileus virginianus"     "Capreolus capreolus"       
#>  [3] "Dama dama"                  "Cervus elaphus"            
#>  [5] "Rangifer tarandus"          "Hippuriphila modeeri"      
#>  [7] "Pseudombrophila merdaria"   "Rangifer tarandus fennicus"
#>  [9] "Rangifer tarandus tarandus" "Odocoileus"
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

</div>

---

### Darwin Core Variables

<div class = 'fragment'>

```r
colnames(finbif_occurrence(dwc = TRUE))
```

</div>
<div class = 'fragment output'> 

```
#>  [1] "occurrenceID"                  "scientificName"               
#>  [3] "individualCount"               "decimalLatitude"              
#>  [5] "decimalLongitude"              "eventDateTime"                
#>  [7] "coordinateUncertaintyInMeters" "hasIssues"                    
#>  [9] "requiresVerification"          "requiresIdentification"       
#> [11] "occurrenceReliability"         "occurrenceQuality"
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

</div>

---

### Choosing taxa

<div class = 'fragment'>

```r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

</div>
<div class = 'fragment output'> 

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

```
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

{{% figure library="true" src="/img/data-viewer.png" lightbox="true" class="fragment" %}}

---

{{% figure library="true" src="/img/viewer-occurrence.png" %}}

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

```
#> [1] 43808551
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

```
#> Warning: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
```

</div>
<div class = 'fragment output'> 

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

```
#> Error: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
```

</div>

---

## Time & duration

---

### Compute date & time

<div class = 'fragment'>

```r
finbif_occurrence(select = "-date_time")
```

</div>
<div class = 'fragment output'> 

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
  select = c("scientific_name", "life_stage", "sex"),
  exclude_na = TRUE
)
```

</div>
<div class = 'fragment output'> 

```
#> Records downloaded: 5
#> Records available: 5
#> A data.frame [5 x 3]
#>        scientific_name life_stage    sex
#> 1 Falco subbuteo Linn…   juvenile   male
#> 2 Falco columbarius L…   juvenile   male
#> 3 Falco columbarius L…   juvenile female
#> 4 Falco rusticolus Li…   juvenile female
#> 5 Falco rusticolus Li…      adult   male
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

```
#> Records downloaded: 10
#> Records available: 87008
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1   …KE.67/9403350#Unit Cygnus cygnus (Linn…  1         60.41667  16      
#> 2  …HR.3691/OBS8108939… Cygnus cygnus (Linn…        NA  61.56563  29.56771
#> 3  …A.DE56E1DC-0195-4A… Cygnus cygnus (Linn…        NA  62.64774  26.00681
#> 4  …A.1093E86E-6A8D-42… Cygnus cygnus (Linn…        NA  60.82859  24.22585
#> 5  …HR.4412/6285786fa7… Cygnus cygnus (Linn…        NA  61.66266  23.31439
#> 6   …KE.67/9069501#Unit Cygnus cygnus (Linn…  1         52.71667  1.55    
#> 7         …JX.1386098#6 Cygnus cygnus (Linn…        NA  63.08324  21.52499
#> 8   …KE.67/9465507#Unit Cygnus cygnus (Linn…  1         61.8      22.76667
#> 9   …KE.67/9607357#Unit Cygnus cygnus (Linn…  1         63.13333  22.43333
#> 10 …HR.3691/OBS8865900… Cygnus cygnus (Linn…        NA  61.27566  22.557  
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 87008
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1          …MHU.2981587 Cygnus cygnus (Linn…  6000      64.4     -14.54   
#> 2  …HR.3691/OBS1101526… Cygnus cygnus (Linn…  1760      62.16389  21.45786
#> 3  …HR.3691/OBS6046423… Cygnus cygnus (Linn…  1753      64.50736  24.27894
#> 4  …HR.3691/OBS6635688… Cygnus cygnus (Linn…  1600      65.98787  24.06341
#> 5         …MHU.28815250 Cygnus cygnus (Linn…  1500            NA        NA
#> 6  …HR.3691/OBS6713538… Cygnus cygnus (Linn…  1361      64.71656  24.53188
#> 7         …JX.1357345#5 Cygnus cygnus (Linn…  1300      64.8465   25.2883 
#> 8         …JX.1398409#3 Cygnus cygnus (Linn…  1280      64.8448   25.2816 
#> 9         …MHU.28815110 Cygnus cygnus (Linn…  1200            NA        NA
#> 10 …HR.3691/OBS1119137… Cygnus cygnus (Linn…  1163      64.71656  24.53188
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Multiple variables

<div class = 'fragment'>

```r
finbif_occurrence(
  "Cygnus cygnus", order_by = c("-abundance", "lat_wgs84")
)
```

</div>
<div class = 'fragment output'> 

```
#> Records downloaded: 10
#> Records available: 87008
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1          …MHU.2981587 Cygnus cygnus (Linn…  6000      64.4     -14.54   
#> 2  …HR.3691/OBS1101526… Cygnus cygnus (Linn…  1760      62.16389  21.45786
#> 3  …HR.3691/OBS6046423… Cygnus cygnus (Linn…  1753      64.50736  24.27894
#> 4  …HR.3691/OBS6635688… Cygnus cygnus (Linn…  1600      65.98787  24.06341
#> 5         …MHU.28815250 Cygnus cygnus (Linn…  1500            NA        NA
#> 6  …HR.3691/OBS6713538… Cygnus cygnus (Linn…  1361      64.71656  24.53188
#> 7         …JX.1357345#5 Cygnus cygnus (Linn…  1300      64.8465   25.2883 
#> 8         …JX.1398409#3 Cygnus cygnus (Linn…  1280      64.8448   25.2816 
#> 9         …MHU.28815110 Cygnus cygnus (Linn…  1200            NA        NA
#> 10 …HR.3691/OBS1119137… Cygnus cygnus (Linn…  1163      64.71656  24.53188
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 45893880
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1            …MY.856424 Planorbarius corneu…  3         61.2      31      
#> 2         …MKC.24761835 Erodium cicutarium …        NA  64.71507  28.45421
#> 3          …MHU.2783077 Acrocephalus schoen…        NA  63.79946  22.63115
#> 4  …HR.4511/34709/4474… Perizoma albulata (…  3         62.98123  29.75411
#> 5   …KE.67/4717586#Unit Parus major Linnaeu…  1         62.61667  23.76667
#> 6          …JX.152313#2 Hypochalcia ahenell…  1         60.54412  27.63478
#> 7          …MKC.3406250 Cerastium fontanum …        NA  59.85868  23.22139
#> 8          …MKC.7631936     Quercus robur L.        NA  60.39284  23.05062
#> 9          …MKC.2060299   Humulus lupulus L.        NA  61.66759  29.6385 
#> 10  …KE.67/4603085#Unit Cyanistes caeruleus…  1         60.3      23.65   
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#>    metadata_name            
#> 1  regulatory_status        
#> 2  red_list                 
#> 3  country                  
#> 4  region                   
#> 5  bio_province             
#> 6  municipality             
#> 7  bird_assoc_area          
#> 8  finnish_occurrence_status
#> 9  habitat_type             
#> 10 habitat_qualifier        
#> 11 life_stage               
#> 12 record_basis             
#> 13 restriction_level        
#> 14 restriction_reason       
#> 15 sex_category             
#> 16 source                   
#> 17 taxon_rank
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

```
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

```
#> Algae                                                         
#>  ¦--Macro algae                                               
#>      ¦--Brown algae and yellow green algae                    
#>      ¦--Green algae                                           
#>      ¦--Red algae                                             
#>      ¦--Stoneworts                                            
#> ...142 more groups
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

```
#> Crustaceans                                                   
#>  ¦--Macrocrustaceans                                          
#>  ¦   ¦--Amphipods, isopods, opossum shrimps                   
#>  ¦   ¦--Crabs, shrimps and crayfishes                         
#>  ¦   ¦--Other macrocrustaceans                                
#>  ¦   ¦--Woodlice                                              
#>  ¦--Microcrustaceans                                          
#>      ¦--Branchiopoda                                          
#>      ¦--Copepods                                              
#>      ¦--Seed shrimps
```

</div>

---

### Collections

<div class = 'fragment'>

```r
finbif_collections(
  filter = taxonomic_coverage == "fungi",
  select = c(
    "collection_name", "geographic_coverage", "count"
  )
)
```

</div>
<div class = 'fragment output'> 

```
#> [1] collection_name     geographic_coverage count              
#> <0 rows> (or 0-length row.names)
```

</div>

---

### Collections

<div class = 'fragment'>

```r
collections <- finbif_collections(
  supercollections = TRUE, nmin = 10000
)

View(collections)
```

</div>

<div class = 'fragment'>

```r
collections <- finbif_collections(
  supercollections = TRUE
)

collections["HR.128", "collection_name"]
```

</div>
<div class = 'fragment output'> 

```
#> [1] "Collections of the Finnish Museum of Natural History Luomus"
```

</div>

---

### Collections

<div class = 'fragment'>

```r
finbif_collections(
  is_part_of == "HR.128", "collection_name",
  supercollections = TRUE
)
```

</div>
<div class = 'fragment output'> 

```
#>         collection_name                          
#> HR.129  Collections of the Botanical Museum      
#> HR.160  Zoological collections                   
#> HR.173  Zoological monitoring schemes            
#> HR.1849 Genomic resources collection samples     
#> HR.203  Löydös Open Finnish Observation Database 
#> HR.435  Löydös Open Invasive Species Observations
#> HR.447  Hatikka.fi observations                  
#> HR.48   Ringing and recovery database of birds
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

```
#> Records downloaded: 10
#> Records available: 43524543
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.3211/148814912-U            Betula L.        NA  66.5783   26.01684
#> 2  …HR.3211/148812535-U                 <NA>        NA  60.17128  24.9309 
#> 3  …HR.3211/148815015-U Carduelis spinus (L…        NA  61.21254  21.74742
#> 4  …HR.3211/148814252-U Parus major Linnaeu…        NA  60.17131  24.93085
#> 5  …HR.3211/148814253-U Passer domesticus (…        NA  60.17131  24.93085
#> 6  …HR.3211/148812940-U Sphagnum capillifol…        NA  60.43821  22.37334
#> 7  …HR.3211/148813130-U Trichaptum abietinu…        NA  60.43727  22.37443
#> 8  …KE.176/63ec916fd5d… Carduelis spinus (L…  10        62.31748  21.73122
#> 9  …KE.176/63ec90e7d5d… Carduelis chloris (…  10        62.31748  21.73122
#> 10        …JX.1529821#3 Larus marinus Linna…  4         60.18657  24.98811
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 20092
#> A data.frame [10 x 12]
#>         record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44286930_Unit Cyanistes caeruleus…  6         60.25655  21.38695
#> 2  …44309720_Unit Corvus monedula Lin…        NA  61.25934  22.36198
#> 3  …54618625_Unit Turdus merula Linna…  12        60.27545  24.83069
#> 4  …44368562_Unit Buteo buteo (Linnae…  1         60.39103  23.57326
#> 5  …45418881_Unit Pica pica (Linnaeus…  1         60.2301   24.01585
#> 6  …54624981_Unit Turdus merula Linna…  2         60.26978  24.86533
#> 7  …44304786_Unit Bucephala clangula …  1         61.58844  21.46563
#> 8  …44304775_Unit Larus marinus Linna…  3         61.58844  21.46563
#> 9  …44317298_Unit Larus canus Linnaeu…  1         64.69889  24.46876
#> 10 …44319650_Unit Cyanistes caeruleus…  1         61.25854  22.34658
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 853743
#> A data.frame [10 x 12]
#>         record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44286930_Unit Cyanistes caeruleus…  6         60.25655  21.38695
#> 2  …44309720_Unit Corvus monedula Lin…        NA  61.25934  22.36198
#> 3  …54618625_Unit Turdus merula Linna…  12        60.27545  24.83069
#> 4  …44368562_Unit Buteo buteo (Linnae…  1         60.39103  23.57326
#> 5  …45418881_Unit Pica pica (Linnaeus…  1         60.2301   24.01585
#> 6  …54624981_Unit Turdus merula Linna…  2         60.26978  24.86533
#> 7  …44304786_Unit Bucephala clangula …  1         61.58844  21.46563
#> 8  …44304775_Unit Larus marinus Linna…  3         61.58844  21.46563
#> 9  …44317298_Unit Larus canus Linnaeu…  1         64.69889  24.46876
#> 10 …44319650_Unit Cyanistes caeruleus…  1         61.25854  22.34658
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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
strict <- list(
  collection_quality = "professional",
  coordinates_uncertainty_max = 1,
  record_quality = "expert_verified"
)
```

</div>

<div class = 'fragment'>

```r
permissive <- list(
  quality_issues = "both",
  record_reliability = c(
    "reliable", "unassessed", "unreliable"
  ),
  record_quality = c(
    "expert_verified", "community_verified",
    "unassessed", "uncertain", "erroneous"
  )
)
```

</div>

---

### Data quality

<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(strict, permissive), count_only = TRUE
)
```

</div>
<div class = 'fragment output'> 

```
#> [[1]]
#> [1] 121
#> 
#> [[2]]
#> [1] 46086500
```

</div>

---

### Collections

<div class = 'fragment'>

```r
finbif_occurrence(
  filter = c(collection = "iNaturalist Suomi Finland"),
  count_only = TRUE
)
```

</div>
<div class = 'fragment output'> 

```
#> [1] 504372
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

```
#> [1] 45893880
```

</div>

---

### Informal groups

<div class = 'fragment'>

```r
finbif_occurrence(
  filter = list(informal_groups = "Reptiles and amphibians")
)
```

</div>
<div class = 'fragment output'> 

```
#> Records downloaded: 10
#> Records available: 46918
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …HR.3211/146607558-U Bufo bufo (Linnaeus…        NA  60.29014  24.60482
#> 2  …HR.3211/146520576-U Bufo bufo (Linnaeus…        NA  60.61056  25.22402
#> 3  …HR.3211/141883071-U Lissotriton vulgari…        NA  60.39002  23.11718
#> 4  …HR.3211/141783787-U Bufo bufo (Linnaeus…        NA  61.05236  25.04516
#> 5  …HR.3211/141784215-U Rana temporaria Lin…        NA  61.05141  25.04307
#> 6  …KE.176/63714108d5d… Anguis colchica (No…  1         61.3986   21.99607
#> 7  …KE.176/636e7ca7d5d… Anguis colchica (No…  1         61.29448  27.58093
#> 8  …HR.3211/141648529-U Rana temporaria Lin…        NA  60.22848  24.91664
#> 9  …HR.3211/141598361-U Anguis colchica (No…        NA  60.64372  24.88825
#> 10 …HR.3211/142675274-U Lissotriton vulgari…        NA  63.6829   22.78389
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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
  filter = list(regulatory_status = "EU_INVSV")
)
```

</div>
<div class = 'fragment output'> 

```
#> Records downloaded: 10
#> Records available: 469
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62b1ad90d5d… Oxyura jamaicensis …  7         61.66207  23.57706
#> 2        …JX.1045316#34 Alopochen aegyptiac…  3         52.16081  4.485534
#> 3        …JX.138840#123 Alopochen aegyptiac…  4         53.36759  6.191796
#> 4        …JX.139978#214 Alopochen aegyptiac…  6         53.37574  6.207861
#> 5         …JX.139710#17 Alopochen aegyptiac…  30        52.3399   5.069133
#> 6         …JX.139645#57 Alopochen aegyptiac…  36        51.74641  4.535283
#> 7         …JX.139645#10 Alopochen aegyptiac…  3         51.74641  4.535283
#> 8         …JX.139442#16 Alopochen aegyptiac…  2         51.90871  4.53258 
#> 9      …KE.8_1208123#15 Alopochen aegyptiac…  2         53.19242  5.437417
#> 10     …KE.8_1208068#89 Alopochen aegyptiac…  5         53.32081  6.192341
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 42448
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1        …JX.1515508#39 Rangifer tarandus f…        NA  64.22363  28.96249
#> 2  …HR.3211/145844443-U Rangifer tarandus f…        NA  64.1      28.5    
#> 3        …JX.1509526#13 Rangifer tarandus f…  9         64.28961  29.15437
#> 4        …JX.1509526#16 Rangifer tarandus f…  17        64.18418  29.21215
#> 5         …JX.1509182#3 Rangifer tarandus f…  4         64.13615  26.24839
#> 6  …HR.3211/142946329-U Rangifer tarandus f…        NA  63.5      23.9    
#> 7       …JX.1503045#165 Rangifer tarandus f…  5         62.13633  22.14217
#> 8         …JX.1505392#3 Rangifer tarandus f…  4         63.40215  24.27285
#> 9  …HR.3211/140674988-U Pusa hispida botnic…        NA  60.03843  24.68483
#> 10        …JX.1501060#3 Rangifer tarandus f…  3         64.09919  29.40356
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> Records downloaded: 10
#> Records available: 381879
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1529644#5 Acrocercops brongni…  1         60.44273  22.19863
#> 2         …JX.1529635#7 Conistra rubiginosa…  14        60.45842  22.17798
#> 3  …HR.3211/148388028-U Hypena rostralis (L…        NA  63.02717  27.25028
#> 4         …JX.1528876#3 Conistra rubiginosa…  2         60.45842  22.17798
#> 5         …JX.1525457#3 Agonopterix hyperic…  1         61.87891  28.85772
#> 6  …HR.3211/147770103-U Acrocercops brongni…        NA  60.45174  22.26663
#> 7  …KE.176/63d84820d5d… Semanotus undatus (…  1         60.47044  22.17258
#> 8         …JX.1521830#3 Conistra rubiginosa…  3         60.45842  22.17798
#> 9  …KE.176/63c6f5e2d5d… Anthrenus scrophula…  2         61.1886   28.76845
#> 10 …KE.176/63c6f5ded5d… Anthrenus scrophula…  2         61.1818   28.84525
#> ...with 0 more record and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
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

```
#> [1] 19 59 32 71
```

</div>

<div class = 'fragment'>

```r
(breaks <- breaks_xy(finland_map$bbox, size = .25))
```

</div>
<div class = 'fragment output'> 

```
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

---

## Reproducibility & Caching

---

### Reproducibility

<div class = 'fragment'>

```r
remotes::install_version("finbif", "0.7.2")
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
