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




```r
plot(finbif_occurrence(filter = c(country = "Finland"), n = 1000))
```

<img src="/tutorials/finbif/plotting_files/figure-html/plot-points-1.png" width="672" />


```r
jays <- finbif_occurrence(
  "Eurasian Jay",
  filter = c(coordinates_uncertainty_max = 100, country = "Finland"),
  select = c("lon_wgs84", "lat_wgs84"),
  n = 2e4
)
```


```r
jay_density <- hist_xy(jays, breaks_xy(finland_map$bbox, .25))
```


```r
par(mar = c(5, 5, 1, 1))

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

polygon(finland_map$vertices, lwd = .2)
```

<img src="/tutorials/finbif/plotting_files/figure-html/plot-jays-1.png" width="672" />
