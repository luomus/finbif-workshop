---
title: Access Token
draft: no
toc: yes
type: book
weight: 3
menu:
  finbif:
    name: 2. Access Token
    weight: 3
---


To access data from FinBIF via its public [API](https://api.laji.fi) you will
need to obtain a personal access token. You should only need to request a token
once but you will need to either set your token each time you start an R
session, or store the token in an `Renviron` file so that is loaded each time R
starts up.

If you have not already done so, load `{finbif}` into your R session.

```r
library(finbif)
```

## Requesting a token
First you need to request a token from FinBIF. This can be done using the
`{finbif}` function `finbif_request_token`. Simply specify your own email in
place of the address shown below.

```r
finbif_request_token("your@email.com")
```
You should soon receive an email from __laji.fi__ which contains your access
key. The key is a random series of letters and numbers. Save the email or key
somewhere securely where you can easily access it again later.

## Setting the token
To access data from FinBIF using the R package you need to set your access token
for the current R session. You can either do this each time you start a new
session,

```r
Sys.setenv(
  FINBIF_ACCESS_TOKEN = "xtmSOIxjPwq0pOMB1WvcZgFLU9QBklauOlonWl8K5oaLIx8RniJ"
)
# Note: the above is not a real access token. Do not try using it.
```
or, to have the key automatically set every time you start an R session you can
save it in an [`Renviron`](https://rviews.rstudio.com/2017/04/19/r-for-enterprise-understanding-r-s-startup/)
file. To add the key you to your user `Renviron` file run the following:


```r
cat(
  'FINBIF_ACCESS_TOKEN = "xtmSOIxjPwq0pOMB1WvcZgFLU9QBklauOlonWl8K5oaLIx8RniJ"',
  file = "~/.Renviron",
  append = TRUE,
  fill = TRUE
)
```
