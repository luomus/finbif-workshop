---
title: Selecting and Ordering Variables
draft: no
toc: yes
type: book
weight: 7
menu:
  finbif:
    name: 6. Select & Order
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
  select = c("scientific_name", "life_stage", "sex")
)
```

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
finbif_occurrence("Cygnus cygnus", order_by = "abundance_interpreted")
```

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

### Descending order
You can switch to descending order by prefixing the variable with a dash.

```r
finbif_occurrence("Cygnus cygnus", order_by = "-abundance_interpreted")
```

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

### Multiple variables
You can specify multiple variables to order by. Sorting primacy is from left to
right.

```r
finbif_occurrence("Cygnus olor", order_by = c("municipality_id", "-abundance_interpreted"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 37120
#> A data.frame [10 x 12]
#>    record_id scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  …12015253     Cygnus olor  2500            NA        NA 2008-08-17 12:00:00
#> 2  …13633876     Cygnus olor  1500            NA        NA 2008-10-03 12:00:00
#> 3    …780984     Cygnus olor  1300            NA        NA 2006-02-14 12:00:00
#> 4    …781416     Cygnus olor  1300            NA        NA 2006-02-14 12:00:00
#> 5   …2062563     Cygnus olor  1200            NA        NA 2006-12-19 12:00:00
#> 6  …10352894     Cygnus olor  1100            NA        NA 2008-06-28 12:00:00
#> 7    …927797     Cygnus olor  1050            NA        NA 2006-04-05 12:00:00
#> 8   …3110953     Cygnus olor  960             NA        NA 2007-10-06 12:00:00
#> 9  …26309317     Cygnus olor  900             NA        NA 2009-07-08 12:00:00
#> 10  …1260385     Cygnus olor  800       58.66     23.57    2006-04-26 18:00:00
#> ...with 0 more records and 6 more variables:
#> coordinates_uncertainty, any_issues, requires_verification,
#> requires_identification, record_reliability, record_quality
```

### Random sample
You can also request a random sample (random order) of occurrence records by
setting the `sample` argument to `TRUE`.

```r
finbif_occurrence(sample = TRUE)
```

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
