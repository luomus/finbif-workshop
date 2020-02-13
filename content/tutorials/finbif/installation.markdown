---
title: Installation
draft: false
toc: true
type: docs
weight: 2

menu:
  finbif:
    name: Installation
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
0.2.0) use the function
`install.packages`. This is the recommended option and suitable in most cases.

```r
install.packages("finbif")
```

### Development
If you want to try out the newest features, or if there is a bug discovered
in the current stable version and it has yet to be updated, then you can also
install the latest version of the package under development. The `{remotes}`
package can be used to install packages directly from [GitHub].

```r
if (require(remotes)) install.packages("remotes")
remotes::install_github("luomus/finbif@dev")
```

### Previous
In some circumstances you may want to install a specific (potentially old)
version of the package. It is often a good idea to install a specific version
if you want to ensure your work is
[reproducible](https://www.practicereproducibleresearch.org/). Again, the
`{remotes}` package can be used in this case.

```r
remotes::install_version("finbif", "0.2.0")
```

## Loading
Once you have installed the package you can load it into your R environment with
the `library` function.

```r
library(finbif)
```
