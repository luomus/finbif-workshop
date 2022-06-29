---
title: Reproducibility and Caching
draft: no
toc: yes
type: book
weight: 11
menu:
  finbif:
    name: 10. Reproducibility
    weight: 11
---



## Reproducibility
In short, [reproducible research
](https://ropensci.github.io/reproducibility-guide/sections/introduction/) is
the practice of documenting and archiving as much of your data collection, data
analysis and data synthesis as is possible to ensure that your work is
verifiable and repeatable.

Some things you might consider doing to ensure your research is reproducible
is to install a specific version of `{finbif}` and set the timezone for
computing event dates and times explicitly.

```r
remotes::install_version("finbif", "0.2.0")
options(finbif_tz = "Europe/Helsinki")
```

## Caching
The most important consideration regarding reproducibility is archiving your
data. Because FinBIF is constantly being updated and amended, you cannot
guarantee that making the same request will return the same data every time.
Therefore, it is a good idea to archive your data in a cache.

### Cache on/off
By default, `{finbif}` caches data in memory so that when you make the same
request to the FinBIF database within a single session you only fetch the data
from the server on the first occasion. This behaviour can be switched off for a
single instance by setting the `cache` parameter to `FALSE`.

```r
finbif_occurrence(cache = FALSE)
```

You can switch it off for the whole session by setting the `finbif_use_cache`
option.

```r
options(finbif_use_cache = FALSE)
```

### Cache on disk
If you are making many large data requests you made need to switch the cache to
write to disk instead of to memory by setting the `finbif_cache_path`.

```r
options(finbif_cache_path = tempdir())
```

You can make your analysis more reproducible by setting the cache path to a
permanent directory in which all your FinBIF data will be archived.

```r
dir.create("cache")
options(finbif_cache_path = "cache")
```

### Clear cache
To clear the cache (in memory or on disk) use the function `finbif_clear_cache`.

```r
finbif_clear_cache()
```
