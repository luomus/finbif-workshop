---
title: Selecting and Ordering Variables
draft: no
toc: yes
type: docs
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
#> Records available: 280396
#> A data.frame [10 x 3]
#>      scientific_name life_stage    sex
#> 1  Falco tinnunculus         NA   <NA>
#> 2  Falco tinnunculus         NA   <NA>
#> 3  Falco tinnunculus         NA FEMALE
#> 4  Falco tinnunculus         NA   <NA>
#> 5  Falco tinnunculus         NA   <NA>
#> 6  Falco tinnunculus         NA   <NA>
#> 7  Falco tinnunculus         NA   <NA>
#> 8  Falco tinnunculus         NA   <NA>
#> 9  Falco tinnunculus         NA   <NA>
#> 10 Falco tinnunculus         NA   <NA>
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
finbif_occurrence("Cygnus cygnus", order_by = "abundance")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56797
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus  1         60.41667  16       1997-04-01 13:00:00
#> 2    Cygnus cygnus  1         63.37022  30.37826                <NA>
#> 3    Cygnus cygnus  1         61.082    27.78355 2017-04-08 12:00:00
#> 4    Cygnus cygnus  1         52.71667  1.55     1997-01-03 14:00:00
#> 5    Cygnus cygnus  1         61.21489  23.36719 2006-06-12 12:00:00
#> 6    Cygnus cygnus  1         61.8      22.76667 2000-03-22 12:00:00
#> 7    Cygnus cygnus  1         63.13333  22.43333 2003-06-07 12:00:00
#> 8    Cygnus cygnus  1         61.72481  24.17242                <NA>
#> 9    Cygnus cygnus  1         60.23968  25.79487                <NA>
#> 10   Cygnus cygnus  1         62.27627  23.59633 1994-04-30 19:50:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

### Descending order
You can switch to descending order by prefixing the variable with a dash.

```r
finbif_occurrence("Cygnus cygnus", order_by = "-abundance")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56797
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus  6000      64.4     -14.54    1995-07-05 15:00:00
#> 2    Cygnus cygnus  2010      64.54597  27.88859 2010-01-01 12:00:00
#> 3    Cygnus cygnus  1500            NA        NA 2003-04-18 15:00:00
#> 4    Cygnus cygnus  1200            NA        NA 2003-04-16 15:00:00
#> 5    Cygnus cygnus  1064      62.50172  21.3326  2017-11-04 08:40:00
#> 6    Cygnus cygnus  722       60.9717   26.48918 2012-11-04 09:00:00
#> 7    Cygnus cygnus  673       60.76462  26.09601 2012-11-07 08:00:00
#> 8    Cygnus cygnus  645       64.84588  25.62653 2005-11-05 12:00:00
#> 9    Cygnus cygnus  645       64.84588  25.62653 2005-11-05 09:00:00
#> 10   Cygnus cygnus  641       62.27627  23.59633 2008-11-20 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

### Multiple variables
You can specify multiple variables to order by. Sorting primacy is from left to
right.

```r
finbif_occurrence("Cygnus olor", order_by = c("municipality", "-abundance"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 24294
#> A data.frame [10 x 10]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Cygnus olor  4         61.13908  23.93331 2007-11-04 09:00:00
#> 2      Cygnus olor  3         61.13908  23.93331 1990-11-04 09:00:00
#> 3      Cygnus olor  3         61.22435  23.73872 1990-11-14 11:00:00
#> 4      Cygnus olor  2         61.16607  23.91207 2013-11-09 08:30:00
#> 5      Cygnus olor  1         61.22435  23.73872 2007-03-01 10:00:00
#> 6      Cygnus olor  4         61.13908  23.93331 2007-11-04 12:00:00
#> 7      Cygnus olor  6         61.2287   23.92458 2002-11-01 12:00:00
#> 8      Cygnus olor  3         61.2287   23.92458 2000-12-22 12:00:00
#> 9      Cygnus olor  1         61.2287   23.92458 2006-03-11 12:00:00
#> 10     Cygnus olor  1         61.2287   23.92458 2010-05-11 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```

### Random sample
You can also request a random sample (random order) of occurrence records by
setting the `sample` argument to `TRUE`.

```r
finbif_occurrence(sample = TRUE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34617520
#> A data.frame [10 x 10]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Ficedula hypoleuca  1         62.24129  25.00644 2012-06-22 12:00:00
#> 2    Prunella modularis  1         59.83333  21.61667 1985-04-21 06:00:00
#> 3        Periparus ater  1         61.42749  24.48508 1983-06-07 12:00:00
#> 4     Falco tinnunculus  1         62.73928  21.71203 1990-07-06 12:00:00
#> 5      Luscinia svecica  1         66.52182  25.71332 2010-08-24 08:00:00
#> 6     Pyrrhula pyrrhula  1         66.54377  25.7662  2009-01-12 13:00:00
#> 7    Erithacus rubecula  1         62.50608  27.61767 2014-06-10 03:25:00
#> 8  Haplodrassus soeren…  1         65.20637  25.82153 2011-05-19 12:00:00
#> 9       Riparia riparia  1         65.01667  25.5     1987-08-02 12:00:00
#> 10   Erithacus rubecula  1         59.83333  19.93333 1974-04-30 12:00:00
#> ...with 0 more records and 5 more variables:
#> record_id, any_issues, record_reliable, taxon_reliability,
#> coordinates_uncertainty
```
