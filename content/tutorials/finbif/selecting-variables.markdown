---
linktitle: 6. Select & Order
title: Selecting and Ordering Variables
draft: no
toc: yes
type: book
weight: 7
---



When requesting data using `{finbif}` you can select from among (or order by)
many variables (properties of the occurrence records). The default set of
variables returned is a small subset of those available. Note that not all
variables are available for all records. To see the variables available and
their definitions in the R help system,

```r
?variables
```
or visit the `{finbif}` [documentation online
](https://luomus.github.io/finbif/reference/variables.html).

## Selecting variables
### Limiting variables
To retrieve a limited set of variables from FinBIF simply specify the desired
variables in the `select` argument.

```r
finbif_occurrence(
  genus  = "Falco",
  select = c("scientific_name", "life_stage", "sex"),
  exclude_na = TRUE
)
```

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

### Extra variables
To get extra variables as well as the default set, specify the extra variables
in addition to the keyword `"default_vars"`.

```r
finbif_occurrence(select = c("default_vars", "life_stage"))
```

## Ordering
You can change the order of occurrence records before they are fetched from the
server by using the `order_by` argument. The default ordering is `date_start`
descending, then `load_date` descending, then `reported_name`.

### Ascending order
By default occurrence records are ordered by variables in ascending order.

```r
finbif_occurrence(
  "Cygnus cygnus", order_by = "abundance"
)
```

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

### Descending order
You can switch to descending order by prefixing the variable with a dash.

```r
finbif_occurrence(
  "Cygnus cygnus", order_by = "-abundance"
)
```

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

### Multiple variables
You can specify multiple variables to order by. Sorting primacy is from left to
right.

```r
finbif_occurrence(
  "Cygnus cygnus", order_by = c("-abundance", "lat_wgs84")
)
```

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

### Random sample
You can also request a random sample (random order) of occurrence records by
setting the `sample` argument to `TRUE`.

```r
finbif_occurrence(sample = TRUE)
```

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
