---
linktitle: 1. Build an SDM
title: Building an SDM using MaxEnt
draft: no
toc: yes
type: book
weight: 2
menu:
  modelling:
    weight: 2
---



This tutorial is a quick demonstration of how to build a species distribution
model (SDM) for Eurasian Red Squirrel (_Sciurus vulgaris_) using Maximum Entropy
(MaxEnt). MaxEnt is a popular method for constructing SDMs for presence-only 
data. The following should not be taken as a "best practice" example, as it only
aims to outline some of the key steps in the modelling process without applying
any of the rigour required to build a fit for purpose model.

## Software setup
To fit distribution models to FinBIF occurrence records will require the
installation of some additional software.

The `{raster}` package is needed for working with gridded data.

```.language-r
if (!require("raster")) install.packages("raster")
library(raster)
```

The `{maxnet}` package is an implementation of the popular presence-only
modelling software, MaxEnt, using the elastic-net regularised generalised linear
models (glmnet).

```.language-r
if (!require("maxnet")) install.packages("maxnet")
library(maxnet)
```

To obtain the occurrence records to model the Eurasian Red Squirrel distribution
will require the `{finbif}` package

```.language-r
library(finbif)
```

For the sake of reproducibility it is a good idea to set an explicit path to
hold cached data.

```.language-r
cache_path <- "cache"
dir.create(cache_path)
options(finbif_cache_path = cache_path)
```

## Occurrence & background
Fitting a presence-only SDM requires two inputs: occurrence records and
background data points to compare with the occurrence records. Both occurrence
and background points can be downloaded directly from FinBIF.

In practice careful thought should go into the selection of both data types.
Here the details of selecting both are glossed over for the sake of brevity and
demonstration.

### Filtering
A common set of filters can be used for both occurrence records and background
data. This filter limits records to those within a bounding box encompassing
(approximately) Finland, and restricts the data to those with a maximum
coordinate uncertainty of 100m.

```.language-r
coordinates_filter <- list(
  coordinates = list(lat = c(60, 70), lon = c(20, 30), system = "wgs84"),
  coordinates_uncertainty_max = 100
)
```

### Occurrence records
Using the predetermined filter the coordinates of the most recent (up to) 5000
occurrences of Eurasian Red Squirrel can be downloaded from FinBIF.

```.language-r
red_squirrel_points <- finbif_occurrence(
  species = "Sciurus vulgaris",
  filter  = coordinates_filter,
  select  = c("lon_wgs84", "lat_wgs84"),
  n       = 5e3
)
```

### Background points
Using the same filter we can obtain background points by selecting a random
sample (10,000) of mammal occurrences. Using the records of a higher taxonomic
group rather than selecting points completely at random helps to mitigate
sampling bias in the occurrence data on the assumption that bias will be similar
in the Squirrel occurrences to the bias in the background points chosen in this
way. In reality this is only one source of bias and more careful thought is
needed to minimise the effect of bias in the model data.

```.language-r
background_points <- finbif_occurrence(
  class  = "Mammals",
  filter = coordinates_filter,
  select = c("lon_wgs84", "lat_wgs84"),
  n      = 1e4,
  sample = TRUE
)
```

### Plotting occurrences
It is useful to compare the Squirrel occurrences to the background points
graphically.

First plot the background data, selecting a semi-transparent colour to convey
the density of points.



```.language-r
plot(
  x   = background_points,
  col = rgb(0, 0, 0, .1)
)
```

Now overlay the Eurasian Red Squirrel occurrence points in a different shade.

```.language-r
points(
  x   = red_squirrel_points,
  col = rgb(1, 0, 0, .1),
  pch = 19,
  cex = .2
)
```

Finally add the Finnish border to the figure.

```.language-r
polygon(finland_map$vertices, lwd = .2)
```

<img src="/tutorials/modelling/simple-sdm_files/figure-html/plot-poly-1.png" width="672" />

## Climate data 
You can obtain climate layers directly from [WorldClim](http://worldclim.org)
with the `{raster}` package function `getData()`. We use these data purely for
convenience, and there is little guarantee that all, or any of them, is related
to a given taxon's distribution. A more robust and rigorous model requires a
deeper understanding of the underlying drivers of the taxon of interest's
distribution to select appropriate response variables.

### Getting climate data
Specify the highest resolution (0.5 arc-minutes) available and the appropriate
latitude and longitude to retrieve the tiles that cover the majority of Finland.
There are 19 bioclimatic variables available, the following retrieves them all
and stores them in the same cache directory as the FinBIF data.

```.language-r
climate_high_res <- getData(
  name = "worldclim",
  var  = "bio",
  res  = .5,
  lat  = 65,
  lon  = 25,
  path = cache_path
)
```

```
#> Warning in getData(name = "worldclim", var = "bio", res = 0.5, lat = 65, : getData will be removed in a future version of raster
#> . You can use access these data, and more, with functions from the geodata package instead
```

### Extracting climate data
You can extract the climate data for all 19 variables at each of the Squirrel
occurrence locations using the `{raster}` function `extract()`.

```.language-r
climate_red_squirrel <- extract(
  x = climate_high_res,
  y = as.data.frame(red_squirrel_points)
)
```

Do the same for the background data points.

```.language-r
climate_background <- extract(
  x = climate_high_res,
  y = as.data.frame(background_points)
)
```

## Formatting input data
Now combine the two datasets into a single object with an indicator variable `p`
that is `1` for presence (occurrence records) and `0` for background points.

```.language-r
input_data <- rbind(
  cbind(p = 1, climate_red_squirrel),
  cbind(p = 0, climate_background)
)
```

To fit a model the input data must be in the form of a `data.frame` and cannot
contain any `NA` data.

```.language-r
input_data <- na.omit(data.frame(input_data))
```

## Fitting MaxEnt model
To fit the SDM use the `{maxnet}` function `maxnet()`. Here the default settings
are used. In general this is inadvisable and care should be taken to find the
appropriate model form and settings for the purpose of the model.

```.language-r
red_squirrel_model <- maxnet(p = input_data[, 1], data = input_data[, -1])
```

## Projection
Using the fitted model we can project the predicted distribution to the broader
region. A caveat is that projections are not reliable if they are being made to
novel parts of the climatic space.

### Climate data
In this case, it will be unnecessary to project to the high resolution climate
data. For the purpose of visualization the 2.5 arc-minutes is fine-grained
enough. 

```.language-r
climate_low_res <- getData(
  name = "worldclim",
  var  = "bio",
  res  = 2.5, 
  path = cache_path
)
```

However, this lower resolution data is untiled so needs to be cropped; in this
case, to the bounding box of the `{finbif}` package's internal map of Finland.

```.language-r
climate_low_res <- crop(
  x = climate_low_res,
  y = extent(sort(finland_map$bbox))
)
```

To make projections to these climate layers with the model requires the data as
a `data.frame`.

```.language-r
climate_low_res_df <- as.data.frame(climate_low_res)
```

And also requires that the names of the bioclimatic layers are the same as the
the lower resolution version

```.language-r
colnames(climate_low_res_df) <- paste0(names(climate_low_res), "_06")
```
(the `"_06"` suffix indicates the sixth Worldclim tile that covers Finland).

### Projecting model
Projecting to the new climate data can be done with `{maxnet}` package's
`predict` method and selecting the "cloglog" (complementary log-log) output
type.

```.language-r
predicted_dist <- predict(
  object   = red_squirrel_model,
  newdata  = climate_low_res_df,
  type     = "cloglog"
)
```

An empty gridded data layer can be created using the low-res climate layers as
a template.

```.language-r
predicted_dist_raster <- raster(climate_low_res)
```

And the projected Squirrel distribution can be added by using non-NA data cells
from the climate layers as an index.

```.language-r
predicted_dist_raster[!is.na(climate_low_res_df[, 1])] <- predicted_dist
```

### Plotting projection
A plot of the Eurasian Red Squirrel's modelled distribution can be made using
the `plot` method from the `{raster}` package,

```.language-r
plot(
  x   = predicted_dist_raster,
  col = hcl.colors(12),
  las = 1,
  asp = 2.4
)
```

adding the border of Finland

```.language-r
polygon(finland_map$vertices, lwd = .5)
```

and finally the original Squirrel occurrence data.

```.language-r
points(
  x   = as.data.frame(red_squirrel_points),
  cex = .05,
  col = rgb(1, 0, 0, .05),
  pch = 19
)
```

<img src="/tutorials/modelling/simple-sdm_files/figure-html/points-1.png" width="672" />
