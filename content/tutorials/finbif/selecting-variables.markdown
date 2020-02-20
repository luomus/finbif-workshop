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
#> Records available: 34452585
#> A data.frame [10 x 31]
#>        scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1    Galanthus elwesii        20  60.44745  22.27223 2020-02-19 22:00:00
#> 2          Strobilurus         1  61.57393  23.17713 2020-02-19 22:00:00
#> 3   Phigalia pilosaria         1  60.38352  23.16606 2020-02-18 22:00:00
#> 4          Strix aluco         1  60.97880  26.09086 2020-02-18 22:00:00
#> 5        Milvus milvus         1  60.78519  26.07963 2020-02-19 05:00:00
#> 6          Strix aluco         1  60.98431  26.04420 2020-02-18 22:00:00
#> 7        Schizophyllum        10  60.18082  25.01560 2020-02-18 22:00:00
#> 8  Exidia cartilaginea        10  60.37493  25.73387 2020-02-18 22:00:00
#> 9      Graphis scripta      1000  60.37480  25.73329 2020-02-18 22:00:00
#> 10   Formica (Formica)         1  59.89200  22.51700 2020-02-18 22:00:00
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
#> Records available: 56162
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
#> Records available: 56162
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
#> Records available: 24183
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
#> Records available: 34452585
#> A data.frame [10 x 30]
#>         scientific_name abundance lat_wgs84 lon_wgs84           date_time
#> 1       Chloris chloris         1  60.13523  23.84799 2014-08-02 21:00:00
#> 2      Acanthis flammea         1  60.82859  24.25148 1999-12-31 22:00:00
#> 3   Fumaria officinalis         1  60.88608  25.05381 2010-09-09 21:00:00
#> 4     Aricia artaxerxes         4  62.91749  27.67557 1997-07-16 21:00:00
#> 5     Gonepteryx rhamni         5  62.20992  30.36092 2002-12-31 21:00:00
#> 6       Pheosia tremula         1  60.85337  27.92973 2006-12-31 22:00:00
#> 7  Ranunculus auricomu…         1  60.05014  21.95920 1932-06-22 22:00:00
#> 8        Sterna hirundo         1  61.31667  24.16667 1996-06-30 21:00:00
#> 9    Anas platyrhynchos         1  61.08727  28.27855 2007-05-20 21:00:00
#> 10        Spinus spinus         1  61.38042  22.36823 2015-05-23 11:00:00
#> ...with 0 more records and 25 more variables:
#> taxon_rank, country, province, municipality, date_start, date_end,
#> hour_start, hour_end, minute_start, minute_end, record_id,
#> individual_id, event_id, collection_id, any_issues, record_issue,
#> record_reliable, taxon_reliability, document_issue,
#> collection_reliability, coordinates_uncertainty, event_issue,
#> location_issue, time_issue, duration
```
