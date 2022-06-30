---
title: Installation
draft: false
toc: true
type: book
weight: 2
menu:
  finbif:
    name: 1. Installation
    weight: 2
---

[CRAN]: https://cran.r-project.org
[GitHub]: https://github.com


The `{finbif}` package can be installed from [CRAN] or [GitHub]. You can choose
either the most recent stable version (recommended), the latest development
version or a previously released version to install.

## Versions
### Stable
To install the current stable version of the package from [CRAN] (currently
0.6.5) use the function
`install.packages`. This is the recommended option and suitable in most cases.

```.language-r
install.packages("finbif")
```

### Development
If you want to try out the newest features, or if there is a bug discovered
in the current stable version and it has yet to be updated, then you can also
install the latest version of the package under development.

```.language-r
install.packages("finbif", repos = "https://luomus.r-universe.dev")
```

### Previous
In some circumstances you may want to install a specific (potentially old)
version of the package. It is often a good idea to install a specific version
if you want to ensure your work is
[reproducible](https://www.practicereproducibleresearch.org/). The
`{remotes}` package can be used in this case.

```.language-r
if (!requireNamespace("remotes", quietly = TRUE)) install.packages("remotes")
remotes::install_version("finbif", "0.6.0")
```

## Loading
Once you have installed the package you can load it into your R session with the
`library` function.

```.language-r
library(finbif)
```
