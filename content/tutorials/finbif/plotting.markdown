---
title: Plotting
draft: no
toc: yes
type: docs
weight: 10
menu:
  finbif:
    name: 9. Plotting
    weight: 10
---



## Points

```r
recent_obs <- finbif_occurrence(filter = c(country = "Finland"), n = 1000)
plot(recent_obs)
```

<img src="/tutorials/finbif/plotting_files/figure-html/plot-points-1.png" width="672" />

## Density
### Data

```r
jays <- finbif_occurrence(
  "Eurasian Jay",
  filter = c(coordinates_uncertainty_max = 100, country = "Finland"),
  select = c("lon_wgs84", "lat_wgs84"),
  n = 2e4
)
```

### Bounding box

```r
finland_map$bbox
```

```{.language-r}
#> [1] 19 59 32 71
```

### Breakpoints

```r
(breaks <- breaks_xy(finland_map$bbox, .25))
```

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

### 2d histogram

```r
jay_density <- hist_xy(jays, breaks)
```

### Image

```r
image(
  jay_density,
  asp    = 2.4,
  breaks = 2^seq(0, 12),
  col    = hcl.colors(12, rev = TRUE),
  xlab   = "Longitude",
  ylab   = "Latitude",
  panel.first = grid(),
  las = 1
)
```

### Legend

```r
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

### Border

```r
polygon(finland_map$vertices, lwd = .2)
```

<img src="/tutorials/finbif/plotting_files/figure-html/plot-finland-1.png" width="672" />
