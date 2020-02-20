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




```r
finbif_clear_cache()

finbif_occurrence(cache = FALSE)

options(finbif_use_cache = FALSE)
options(finbif_use_cache = TRUE)
options(finbif_cache_path = tempdir())
dir.create("cache")
options(finbif_cache_path = "cache")
```
