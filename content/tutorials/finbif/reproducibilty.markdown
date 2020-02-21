---
title: Reproducibility and Caching
draft: no
toc: yes
type: docs
weight: 11
menu:
  finbif:
    name: 10. Reproducibility
    weight: 11
---



## Reproducibility


## Caching
### Clear cache

```r
finbif_clear_cache()
```

### Cache on/off

```r
finbif_occurrence(cache = FALSE)
```


```r
options(finbif_use_cache = FALSE)
```


```r
options(finbif_use_cache = TRUE)
```

### Cache on disk

```r
options(finbif_cache_path = tempdir())
```


```r
dir.create("cache")
```


```r
options(finbif_cache_path = "cache")
```
