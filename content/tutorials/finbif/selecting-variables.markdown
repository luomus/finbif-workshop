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
#> Records available: 280289
#> A data.frame [10 x 3]
#>      scientific_name life_stage  sex
#> 1  Falco tinnunculus       <NA> <NA>
#> 2  Falco tinnunculus       <NA> <NA>
#> 3  Falco tinnunculus       <NA> <NA>
#> 4  Falco columbarius       <NA> MALE
#> 5  Falco tinnunculus       <NA> <NA>
#> 6  Falco columbarius       <NA> <NA>
#> 7  Falco columbarius       <NA> <NA>
#> 8  Falco tinnunculus       <NA> <NA>
#> 9  Falco columbarius       <NA> <NA>
#> 10 Falco columbarius       <NA> <NA>
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
#> Records available: 56217
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         1  60.41667  16.00000 1997-04-01 01:00:00
#> 2    Cygnus cygnus         1  63.37022  30.37826                <NA>
#> 3    Cygnus cygnus         1  61.08200  27.78355 2017-04-08 00:00:00
#> 4    Cygnus cygnus         1  52.71667   1.55000 1997-01-03 02:00:00
#> 5    Cygnus cygnus         1  61.21489  23.36719 2006-06-12 00:00:00
#> 6    Cygnus cygnus         1  61.80000  22.76667 2000-03-22 00:00:00
#> 7    Cygnus cygnus         1  63.13333  22.43333 2003-06-07 00:00:00
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

### Descending order
You can switch to descending order by prefixing the variable with a dash.

```r
finbif_occurrence("Cygnus cygnus", order_by = "-abundance")
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56217
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus      6000  64.40000 -14.54000 1995-07-05 03:00:00
#> 2    Cygnus cygnus      2010  64.54597  27.88859 2010-01-01 00:00:00
#> 3    Cygnus cygnus      1500        NA        NA 2003-04-18 03:00:00
#> 4    Cygnus cygnus      1200        NA        NA 2003-04-16 03:00:00
#> 5    Cygnus cygnus      1064  62.50172  21.33260 2017-11-04 08:40:00
#> 6    Cygnus cygnus       722  60.97170  26.48918 2012-11-04 09:00:00
#> 7    Cygnus cygnus       673  60.76462  26.09601 2012-11-07 08:00:00
#> 8    Cygnus cygnus       645  64.84588  25.62653 2005-11-05 00:00:00
#> 9    Cygnus cygnus       645  64.84588  25.62653 2005-11-05 09:00:00
#> 10   Cygnus cygnus       641  62.27627  23.59633 2008-11-20 00:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Multiple variables
You can specify multiple variables to order by. Sorting primacy is from left to
right.

```r
finbif_occurrence("Cygnus olor", order_by = c("municipality", "-abundance"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 24208
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Cygnus olor         4  61.13908  23.93331 2007-11-04 09:00:00
#> 2      Cygnus olor         3  61.13908  23.93331 1990-11-04 09:00:00
#> 3      Cygnus olor         3  61.22435  23.73872 1990-11-14 11:00:00
#> 4      Cygnus olor         2  61.16607  23.91207 2013-11-09 08:30:00
#> 5      Cygnus olor         1  61.22435  23.73872 2007-03-01 10:00:00
#> 6      Cygnus olor         4  61.13908  23.93331 2007-11-04 00:00:00
#> 7      Cygnus olor         6  61.22870  23.92458 2002-11-01 00:00:00
#> 8      Cygnus olor         3  61.22870  23.92458 2000-12-22 00:00:00
#> 9      Cygnus olor         1  61.22870  23.92458 2006-03-11 00:00:00
#> 10     Cygnus olor         1  61.22870  23.92458 2010-05-11 00:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Random sample
You can also request a random sample (random order) of occurrence records by
setting the `sample` argument to `TRUE`.

```r
finbif_occurrence(sample = TRUE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34469168
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1  Fringilla montifrin…         1  62.59569  29.78966 1992-05-05 11:00:00
#> 2       Populus tremula         1  64.34498  27.37926 2018-07-04 00:00:00
#> 3     Agriades optilete         8  61.93630  23.47236 2000-01-01 00:00:00
#> 4     Bunias orientalis         1  60.45173  21.99719 1942-07-29 00:00:00
#> 5   Agrimonia eupatoria         1        NA        NA                <NA>
#> 6   Dasiphora fruticosa         1  54.50000 109.83333 1996-08-22 18:00:00
#> 7      Carex pallescens         1  60.75406  26.18074 2011-06-22 00:00:00
#> 8        Motacilla alba         1  62.69862  26.75152 1992-06-11 00:00:00
#> 9           Betula nana         1  68.92768  21.19636 2002-07-19 01:00:00
#> 10          Limnodrilus         1  63.70253  26.71844 2001-10-17 10:01:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
