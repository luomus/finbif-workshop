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

```.language-r
install.packages("finbif")
```

</div>

---

### Development version

<div class = 'fragment'>

```.language-r
if (!require(remotes)) install.packages("remotes")
remotes::install_github("luomus/finbif@dev")
```

</div>

---

### Previous versions

<div class = 'fragment'>

```.language-r
remotes::install_version("finbif", "0.6.0")
```

</div>

---

### Loading the package

<div class = 'fragment'>

```.language-r
library(finbif)
```

</div>

---

## Access token

---

### Requesting a token

<div class = 'fragment'>

```.language-r
finbif_request_token("your@email.com")
```

</div>

---

### Setting the token

<div class = 'fragment'>

```.language-r
Sys.setenv(
  FINBIF_ACCESS_TOKEN = "xtmSOIxjPwq0pOMB1WvcZgFLU9QBkl"
)
```

</div>

<div class = 'fragment'>

```.language-r
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

```.language-r
?finbif_request_token
```

</div>

<div class = 'fragment'>

```.language-r
help("finbif_request_token")
```

</div>

{{% fragment %}} Some important help files {{% /fragment %}}

<div class = 'fragment'>

```.language-r
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

```.language-r
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

```.language-r
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

```.language-r
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

```.language-r
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

```.language-r
taxa_list <- readLines("taxa.csv")
finbif_check_taxa(taxa_list)
```

</div>

---

## Taxa search

---

### Exact matching

<div class = 'fragment'>

```.language-r
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

```.language-r
deer <- finbif_taxa("deer", type = "partial", n = 10)
sapply(deer$content, getElement, "scientificName")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
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

```.language-r
finbif_occurrence()
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Darwin Core Variables

<div class = 'fragment'>

```.language-r
colnames(finbif_occurrence(dwc = TRUE))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
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

```.language-r
finbif_occurrence("Cygnus cygnus")
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Choosing taxa

<div class = 'fragment'>

```.language-r
finbif_occurrence("Cygnus cygnus", "Cygnus olor")
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Choosing taxa

<div class = 'fragment'>

```.language-r
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

```.language-r
occurrences <- finbif_occurrence(n = 1001)
```

</div>

---

### Data viewer

<div class = 'fragment'>

```.language-r
View(occurrences)
```

</div>

{{% figure library="true" src="/img/data-viewer.png" lightbox="true" class="fragment" %}}

---

{{% figure library="true" src="/img/viewer-occurrence.png" %}}

---

### Suppress progress bar

<div class = 'fragment'>

```.language-r
finbif_occurrence(n = 1001, quiet = TRUE)
```

</div>

---

### Count records

<div class = 'fragment'>

```.language-r
finbif_occurrence(count_only = TRUE)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 43808551
```

</div>

---

### Checking taxa

<div class = 'fragment'>

```.language-r
finbif_occurrence("Vulpes vulpes", "Moomin")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Warning: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> Moomin
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Without checking

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  "Vulpes vulpes", "Moomin", check_taxa = FALSE
)
```

</div>

---

### Failing with error

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  "Vulpes vulpes", "Moomin", on_check_fail = "error"
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
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

```.language-r
finbif_occurrence(select = "-date_time")
```

</div>
<div class = 'fragment output'> 

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

</div>

---

## Timezones

---

### Timezone input

<div class = 'fragment'>

```.language-r
finbif_occurrence(date_time_method = "accurate")
```

</div>

---

### Timezone output

<div class = 'fragment'>

```.language-r
Sys.timezone()
```

</div>

<div class = 'fragment'>

```.language-r
finbif_occurrence(tzone = "Etc/UTC")
```

</div>
<div class = 'fragment output'> 

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

</div>

---

### Set timezone

<div class = 'fragment'>

```.language-r
options(finbif_tz = "Etc/UTC")
```

</div>

---

## Selecting & ordering variables

---

### Variables help page

<div class = 'fragment'>

```.language-r
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

```.language-r
finbif_occurrence(
  genus  = "Falco",
  select = c("scientific_name", "life_stage", "sex"),
  na_exclude = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Warning: Cannot find the following taxa in the FinBIF taxonomy.
#> Please check you are using accepted names and not synonyms or
#> other names for the taxa you are selecting:
#> 
#> na_exclude - TRUE
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 324767
#> A data.frame [10 x 3]
#>      scientific_name life_stage sex
#> 1  Falco tinnunculus         NA  NA
#> 2     Falco subbuteo         NA  NA
#> 3  Falco tinnunculus         NA  NA
#> 4  Falco tinnunculus         NA  NA
#> 5     Falco subbuteo         NA  NA
#> 6  Falco tinnunculus         NA  NA
#> 7     Falco subbuteo         NA  NA
#> 8  Falco tinnunculus         NA  NA
#> 9  Falco tinnunculus         NA  NA
#> 10 Falco tinnunculus         NA  NA
```

</div>

---

### Extra variables

<div class = 'fragment'>

```.language-r
finbif_occurrence(select = c("default_vars", "life_stage"))
```

</div>

---

## Ordering

---

### Ascending order

<div class = 'fragment'>

```.language-r
finbif_occurrence("Cygnus cygnus", order_by = "abundance")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 80292
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1   …KE.67/9403350#Unit   Cygnus cygnus  1         60.41667  16      
#> 2         …MHU.29327372   Cygnus cygnus        NA  63.37022  30.37826
#> 3  …KE.176/58c7db302d0…   Cygnus cygnus        NA  61.082    27.78355
#> 4          …MHU.2529766   Cygnus cygnus        NA  64.94099  27.52532
#> 5  …HR.4412/6285786fa7…   Cygnus cygnus        NA  61.66266  23.31439
#> 6   …KE.67/9069501#Unit   Cygnus cygnus  1         52.71667  1.55    
#> 7         …MHU.12651157   Cygnus cygnus  1         61.21489  23.36719
#> 8         …MHU.21539922   Cygnus cygnus        NA  60.42008  22.44084
#> 9         …MHU.29669347   Cygnus cygnus        NA  63.57075  29.71466
#> 10  …KE.67/9465507#Unit   Cygnus cygnus  1         61.8      22.76667
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Descending order

<div class = 'fragment'>

```.language-r
finbif_occurrence("Cygnus cygnus", order_by = "-abundance")
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 80292
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1          …MHU.2981587   Cygnus cygnus  6000      64.4     -14.54   
#> 2         …MHU.29480894   Cygnus cygnus  2010      64.54597  27.88859
#> 3  …HR.3691/OBS6046423…   Cygnus cygnus  1753      64.50736  24.27894
#> 4  …HR.3691/OBS6635688…   Cygnus cygnus  1600      65.98787  24.06341
#> 5         …MHU.28815250   Cygnus cygnus  1500            NA        NA
#> 6  …HR.3691/OBS6713538…   Cygnus cygnus  1361      64.71656  24.53188
#> 7         …JX.1357345#5   Cygnus cygnus  1300      64.8465   25.2883 
#> 8         …JX.1398409#3   Cygnus cygnus  1280      64.8448   25.2816 
#> 9         …MHU.28815110   Cygnus cygnus  1200            NA        NA
#> 10        …JX.1402662#3   Cygnus cygnus  1160      64.872    24.8788 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Multiple variables

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  "Cygnus cygnus", order_by = c("-abundance", "lat_wgs84")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 80319
#> A data.frame [10 x 12]
#>               record_id scientific_name abundance lat_wgs84 lon_wgs84
#> 1          …MHU.2981587   Cygnus cygnus  6000      64.4     -14.54   
#> 2         …MHU.29480894   Cygnus cygnus  2010      64.54597  27.88859
#> 3  …HR.3691/OBS6046423…   Cygnus cygnus  1753      64.50736  24.27894
#> 4  …HR.3691/OBS6635688…   Cygnus cygnus  1600      65.98787  24.06341
#> 5         …MHU.28815250   Cygnus cygnus  1500            NA        NA
#> 6  …HR.3691/OBS6713538…   Cygnus cygnus  1361      64.71656  24.53188
#> 7         …JX.1357345#5   Cygnus cygnus  1300      64.8465   25.2883 
#> 8         …JX.1398409#3   Cygnus cygnus  1280      64.8448   25.2816 
#> 9         …MHU.28815110   Cygnus cygnus  1200            NA        NA
#> 10        …JX.1402662#3   Cygnus cygnus  1160      64.872    24.8788 
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Random sample

<div class = 'fragment'>

```.language-r
finbif_occurrence(sample = TRUE)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 43808551
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …tun.fi/JX.1024552#…   Bucephala clangula  1         60.28977  25.86029
#> 2  …tun.fi/MKC.25656454   Salix myrsinifolia        NA  66.47118  29.1717 
#> 3  …tun.fi/KE.67/11535…          Parus major  1         60.77856  22.41808
#> 4  …id.luomus.fi/MY.47…   Astragalus alpinus        NA        NA        NA
#> 5  …tun.fi/A.22B93AD5-… Herminia tarsipenna…  1         59.86133  23.15867
#> 6  …tun.fi/KE.67/44938…   Erithacus rubecula  1         59.83333  19.93333
#> 7   …tun.fi/MKC.1268070 Amaranthus retrofle…        NA  61.69857  27.27081
#> 8  …tun.fi/JX.1177981#…   Erannis defoliaria  215       60.45842  22.17798
#> 9  …tun.fi/KE.941/Samp…   Lepidostoma hirtum        NA  61.63891  21.70778
#> 10 …tun.fi/MKC.32851600 Leucanthemum vulgare        NA  63.06518  28.35152
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

## Metadata

---

### General metadata

<div class = 'fragment'>

```.language-r
finbif_metadata()
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>    metadata_name            
#> 1  admin_status             
#> 2  red_list                 
#> 3  country                  
#> 4  province                 
#> 5  municipality             
#> 6  bird_assoc_area          
#> 7  finnish_occurrence_status
#> 8  habitat_type             
#> 9  habitat_qualifier        
#> 10 life_stage               
#> 11 record_basis             
#> 12 restriction_level        
#> 13 restriction_reason       
#> 14 sex_category             
#> 15 source                   
#> 16 taxon_rank
```

</div>

---

### General metadata

<div class = 'fragment'>

```.language-r
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

```.language-r
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
#> ...142 more groups
```

</div>

---

### Informal groups

<div class = 'fragment'>

```.language-r
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

```.language-r
finbif_collections(
  filter = taxonomic_coverage == "fungi",
  select = c("collection_name", "geographic_coverage", "count")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#>         collection_name geographic_coverage count 
#> HR.2129 Fungal atlas    Finland             102238
```

</div>

---

### Collections

<div class = 'fragment'>

```.language-r
collections <- finbif_collections(
  supercollections = TRUE, nmin = 10000
)

View(collections)
```

</div>

<div class = 'fragment'>

```.language-r
collections <- finbif_collections(
  supercollections = TRUE
)

collections["HR.128", "collection_name"]
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

```.language-r
finbif_collections(
  is_part_of == "HR.128", "collection_name",
  supercollections = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
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

```.language-r
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

```.language-r
finbif_occurrence(filter = c(country = "Finland"))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 41580509
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

</div>

---

### Coordinates

<div class = 'fragment'>

```.language-r
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

```.language-r
finbif_occurrence(filter = c(date_range_ymd = "2019-12"))
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 19883
#> A data.frame [10 x 12]
#>         record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44280127_Unit       Turdus merula  2         60.41401  22.24457
#> 2  …44304840_Unit   Dendrocopos major  1         60.40432  22.18121
#> 3  …44280136_Unit Emberiza citrinella  2         60.41401  22.24457
#> 4  …54619078_Unit       Turdus merula  3         60.27095  24.83408
#> 5  …44317394_Unit    Larus argentatus  1         64.66585  24.40813
#> 6  …54625618_Unit         Parus major  6         60.27448  24.86076
#> 7  …44308453_Unit        Corvus corax  1         61.97913  21.42103
#> 8  …44300432_Unit    Carduelis spinus  2         60.42983  22.21151
#> 9  …44286929_Unit   Fringilla coelebs  2         60.25655  21.38695
#> 10 …44304839_Unit    Carduelis spinus  10        60.40432  22.18121
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Dates

<div class = 'fragment'>

```.language-r
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
#> Records available: 835439
#> A data.frame [10 x 12]
#>         record_id     scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …44280127_Unit       Turdus merula  2         60.41401  22.24457
#> 2  …44304840_Unit   Dendrocopos major  1         60.40432  22.18121
#> 3  …44280136_Unit Emberiza citrinella  2         60.41401  22.24457
#> 4  …54619078_Unit       Turdus merula  3         60.27095  24.83408
#> 5  …44317394_Unit    Larus argentatus  1         64.66585  24.40813
#> 6  …54625618_Unit         Parus major  6         60.27448  24.86076
#> 7  …44308453_Unit        Corvus corax  1         61.97913  21.42103
#> 8  …44300432_Unit    Carduelis spinus  2         60.42983  22.21151
#> 9  …44286929_Unit   Fringilla coelebs  2         60.25655  21.38695
#> 10 …44304839_Unit    Carduelis spinus  10        60.40432  22.18121
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Dates

<div class = 'fragment'>

```.language-r
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

```.language-r
strict <- c(
  collection_quality = "professional",
  coordinates_uncertainty_max = 1,
  record_quality = "expert_verified"
)
```

</div>

<div class = 'fragment'>

```.language-r
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

<div class = 'fragment'>

```.language-r
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
#>         50   44002046
```

</div>

---

### Collections

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  filter = c(collection = "iNaturalist Suomi Finland"),
  count_only = TRUE
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 504372
```

</div>

<div class = 'fragment'>

```.language-r
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
#> [1] 13577108
```

</div>

---

### Informal groups

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  filter = list(informal_group = "Reptiles and amphibians")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 44950
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62bbcbcdd5d…      Anguis fragilis  1         61.10221  22.88537
#> 2  …KE.176/62bbd8e9d5d… Pelophylax esculent…  3         60.61041  21.5252 
#> 3  …KE.176/62bb6a86d5d…      Anguis fragilis  1         59.98272  23.99422
#> 4  …KE.176/62bb617fd5d…      Anguis fragilis  1         60.14724  24.36741
#> 5  …HR.3211/123833894-U     Zootoca vivipara        NA  63.64611  27.17139
#> 6  …HR.3211/123838182-U      Rana temporaria        NA        NA        NA
#> 7  …KE.176/62baf319d5d…      Anguis fragilis  1         61.98459  24.06683
#> 8  …KE.176/62baeaffd5d…      Anguis fragilis  1         60.04463  24.55186
#> 9  …HR.3211/123804109-U     Zootoca vivipara        NA  61.03338  25.88673
#> 10 …KE.176/62baa39cd5d…      Anguis fragilis  1         61.47152  24.43033
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

## Taxon status

---

### Administrative status

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  "birds",
  filter = list(administrative_status = "EU_INVSV")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 469
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62b1ad90d5d…   Oxyura jamaicensis  7         61.66207  23.57706
#> 2        …JX.1045316#34 Alopochen aegyptiaca  3         52.16081  4.485534
#> 3        …JX.138840#123 Alopochen aegyptiaca  4         53.36759  6.191796
#> 4        …JX.139978#214 Alopochen aegyptiaca  6         53.37574  6.207861
#> 5         …JX.139710#17 Alopochen aegyptiaca  30        52.3399   5.069133
#> 6         …JX.139645#57 Alopochen aegyptiaca  36        51.74641  4.535283
#> 7         …JX.139645#10 Alopochen aegyptiaca  3         51.74641  4.535283
#> 8         …JX.139442#16 Alopochen aegyptiaca  2         51.90871  4.53258 
#> 9      …KE.8_1208123#15 Alopochen aegyptiaca  2         53.19242  5.437417
#> 10    …KE.8_1208068#101 Alopochen aegyptiaca  20        53.32081  6.192341
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Red list

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  "mammals", filter = list(red_list_status = "NT")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 2457
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1  …KE.176/62bab390d5d…         Castor fiber  1         62.24068  28.8834 
#> 2         …JX.1408115#3 Rangifer tarandus f…  1         63.21216  24.31222
#> 3        …JX.1397132#39 Rangifer tarandus f…  2         64.13285  26.27761
#> 4       …JX.1396580#493 Rangifer tarandus f…  1         64.32912  28.7958 
#> 5  …HR.3211/121755178-U Rangifer tarandus f…        NA  63.5      24.3    
#> 6  …HR.3211/121759281-U Rangifer tarandus f…        NA  63.5      24.3    
#> 7  …HR.3211/121755627-U Rangifer tarandus f…        NA  63.9      24.7    
#> 8        …JX.1392113#15 Rangifer tarandus f…  1         64.0517   28.32895
#> 9  …KE.176/62a04ad6d5d… Pusa hispida botnica  1         60.21181  25.37497
#> 10       …JX.1390384#11 Rangifer tarandus f…  1         64.33209  25.73386
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Finnish occurrence

<div class = 'fragment'>

```.language-r
finbif_occurrence(
  filter = c(finnish_occurrence_status = "rare")
)
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> Records downloaded: 10
#> Records available: 357479
#> A data.frame [10 x 12]
#>               record_id      scientific_name abundance lat_wgs84 lon_wgs84
#> 1         …JX.1411601#9     Stegania cararia  3         61.48089  29.45853
#> 2         …JX.1411614#3 Habrosyne pyritoides  1         61.71285  29.39905
#> 3        …JX.1411450#36      Ancylis upupana  1         61.51447  24.0233 
#> 4        …JX.1411450#15  Eupithecia selinata  1         61.51447  24.0233 
#> 5        …JX.1411579#17        Pyrgus alveus  2         60.24476  22.30047
#> 6  …HR.3211/123829199-U Korscheltellus lupu…        NA  60.98495  25.54631
#> 7         …JX.1411456#6         Colias tyche  1         69.06191  20.82332
#> 8         …JX.1411456#3     Euphydryas iduna  6         69.06191  20.82332
#> 9  …HR.3211/123811818-U Ypsolopha chazariel…        NA  60.31112  25.03602
#> 10        …JX.1411418#3      Eucosma fulvana  2         61.71372  29.39204
#> ...with 0 more records and 7 more variables:
#> date_time, coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

</div>

---

### Finnish occurrence (negation)

<div class = 'fragment'>

```.language-r
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

```.language-r
recent_obs <- finbif_occurrence(
  filter = c(country = "Finland"), n = 1000
)
```

</div>

---

### Occurrence points

<div class = 'fragment'>

```.language-r
plot(recent_obs)
```

</div>

---

## Occurrence density

---

### Data

<div class = 'fragment'>

```.language-r
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

```.language-r
finland_map$bbox
```

</div>
<div class = 'fragment output'> 

```{.language-r}
#> [1] 19 59 32 71
```

</div>

<div class = 'fragment'>

```.language-r
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

```.language-r
jay_density <- hist_xy(jays, breaks)
```

</div>

---

### Image

<div class = 'fragment'>

```.language-r
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

```.language-r
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

```.language-r
polygon(finland_map$vertices, lwd = .2)
```

</div>

---

## Reproducibility & Caching

---

### Reproducibility

<div class = 'fragment'>

```.language-r
remotes::install_version("finbif", "0.6.5")
options(finbif_tz = "Europe/Helsinki")
```

</div>

---

## Caching

---

### Cache on/off

<div class = 'fragment'>

```.language-r
finbif_occurrence(cache = FALSE)
```

</div>

<div class = 'fragment'>

```.language-r
options(finbif_use_cache = FALSE)
```

</div>

---

### Cache on disk

<div class = 'fragment'>

```.language-r
options(finbif_cache_path = tempdir())
```

</div>

<div class = 'fragment'>

```.language-r
dir.create("cache")
options(finbif_cache_path = "cache")
```

</div>

---

### Clear cache

<div class = 'fragment'>

```.language-r
finbif_clear_cache()
```

</div>

---

# FIN
