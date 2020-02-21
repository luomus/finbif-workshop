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




```r
?variables
```

## Selecting variables
### Limiting variables

```r
finbif_occurrence(
  genus = "Falco",
  select = c("scientific_name", "life_stage", "sex")
)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 280284
#> A data.frame [10 x 3]
#>      scientific_name life_stage  sex
#> 1  Falco tinnunculus       <NA> <NA>
#> 2  Falco columbarius       <NA> MALE
#> 3  Falco tinnunculus       <NA> <NA>
#> 4  Falco columbarius       <NA> <NA>
#> 5  Falco columbarius       <NA> <NA>
#> 6  Falco columbarius       <NA> <NA>
#> 7  Falco columbarius       <NA> <NA>
#> 8  Falco tinnunculus       <NA> <NA>
#> 9  Falco tinnunculus       <NA> MALE
#> 10 Falco columbarius       <NA> <NA>
```

### Extra variables

```r
finbif_occurrence(select = c("default_vars", "life_stage"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34453511
#> A data.frame [10 x 31]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Regulus regulus         1  60.13373  24.93114 2020-02-19 22:00:00
#> 2         Cygnus cygnus         3  60.13373  24.93114 2020-02-19 22:00:00
#> 3     Loxia curvirostra         1  60.13373  24.93114 2020-02-19 22:00:00
#> 4    Attagenus smirnovi         1  60.45229  22.28433 2020-02-19 22:00:00
#> 5            Peniophora         1  65.21097  25.28346 2020-02-19 22:00:00
#> 6      Stereum hirsutum         1  65.21097  25.28346 2020-02-19 22:00:00
#> 7  Basidioradulum radu…         1  65.21097  25.28346 2020-02-19 22:00:00
#> 8        Phellinus alni         1  65.21097  25.28346 2020-02-19 22:00:00
#> 9     Trametes ochracea         1  65.21097  25.28346 2020-02-19 22:00:00
#> 10     Cerrena unicolor         1  65.21097  25.28346 2020-02-19 22:00:00
#> ...with 0 more records and 26 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, life_stage, duration
```

## Ordering
### Ascending order

```r
finbif_occurrence("Cygnus cygnus", order_by = c("abundance"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56164
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus         1  60.41667  16.00000 1997-03-31 22:00:00
#> 2    Cygnus cygnus         1  63.37022  30.37826                <NA>
#> 3    Cygnus cygnus         1  61.08200  27.78355 2017-04-07 21:00:00
#> 4    Cygnus cygnus         1  52.71667   1.55000 1997-01-03 00:00:00
#> 5    Cygnus cygnus         1  61.21489  23.36719 2006-06-11 21:00:00
#> 6    Cygnus cygnus         1  61.80000  22.76667 2000-03-21 22:00:00
#> 7    Cygnus cygnus         1  63.13333  22.43333 2003-06-06 21:00:00
#> 8    Cygnus cygnus         1  61.72481  24.17242                <NA>
#> 9    Cygnus cygnus         1  60.23968  25.79487                <NA>
#> 10   Cygnus cygnus         1  62.27627  23.59633 1994-04-30 16:50:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Descending order

```r
finbif_occurrence("Cygnus cygnus", order_by = c("-abundance"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 56164
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Cygnus cygnus      6000  64.40000 -14.54000 1995-07-05 00:00:00
#> 2    Cygnus cygnus      2010  64.54597  27.88859 2009-12-31 22:00:00
#> 3    Cygnus cygnus      1500        NA        NA 2003-04-18 00:00:00
#> 4    Cygnus cygnus      1200        NA        NA 2003-04-16 00:00:00
#> 5    Cygnus cygnus      1064  62.50172  21.33260 2017-11-04 06:40:00
#> 6    Cygnus cygnus       722  60.97170  26.48918 2012-11-04 07:00:00
#> 7    Cygnus cygnus       673  60.76462  26.09601 2012-11-07 06:00:00
#> 8    Cygnus cygnus       645  64.84588  25.62653 2005-11-04 22:00:00
#> 9    Cygnus cygnus       645  64.84588  25.62653 2005-11-05 07:00:00
#> 10   Cygnus cygnus       641  62.27627  23.59633 2008-11-19 22:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Multiple variables

```r
finbif_occurrence("Cygnus olor", order_by = c("municipality", "-abundance"))
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 24184
#> A data.frame [10 x 30]
#>    scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Cygnus olor         4  61.13908  23.93331 2007-11-04 07:00:00
#> 2      Cygnus olor         3  61.13908  23.93331 1990-11-04 07:00:00
#> 3      Cygnus olor         3  61.22435  23.73872 1990-11-14 09:00:00
#> 4      Cygnus olor         2  61.16607  23.91207 2013-11-09 06:30:00
#> 5      Cygnus olor         1  61.22435  23.73872 2007-03-01 08:00:00
#> 6      Cygnus olor         4  61.13908  23.93331 2007-11-03 22:00:00
#> 7      Cygnus olor         6  61.22870  23.92458 2002-10-31 22:00:00
#> 8      Cygnus olor         3  61.22870  23.92458 2000-12-21 22:00:00
#> 9      Cygnus olor         1  61.22870  23.92458 2006-03-10 22:00:00
#> 10     Cygnus olor         1  61.22870  23.92458 2010-05-10 21:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```

### Random sample

```r
finbif_occurrence(sample = TRUE)
```

```{.language-r}
#> Records downloaded: 10
#> Records available: 34453512
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1      Larus argentatus         1  59.93333  24.40000 1988-06-05 20:00:00
#> 2     Amphipyra perflua         4  60.20207  25.63553 2006-07-17 21:00:00
#> 3      Ipimorpha retusa         1  60.98525  28.56731 1987-12-31 22:00:00
#> 4    Epirrhoe alternata         1  60.45584  26.90618 1993-07-25 21:00:00
#> 5   Armoracia rusticana         1  62.61315  29.79228 2017-06-16 21:00:00
#> 6           Larus canus         1  59.93218  24.32561 1999-12-31 22:00:00
#> 7                 Loxia         1  62.28724  24.34886 2013-06-03 00:30:00
#> 8  Gnorimoschema epith…         1  60.62193  27.06083 2017-06-17 21:00:00
#> 9  Epirranthis diversa…         2  60.16425  24.56528 1987-05-02 21:00:00
#> 10 Xanthorhoe montanata         2  66.60747  25.76980 2014-07-12 21:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
