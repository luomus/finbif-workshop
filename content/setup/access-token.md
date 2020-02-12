---
date: "2020-02-12"
linktitle: Step 4. Access Token
menu:
  setup:
    parent: Setup
    weight: 5
title: Request a FinBIF access token
type: docs
weight: 5
---

To access data from FinBIF via the finbif R package requires a personal access
token. To obtain an access token follow these instructions:

1. Click on the "Console" pane and type `library(finbif)` followed by the return
   key.
2. Still in the "Console" pane, type `finbif_request_token("YOUR_EMAIL")`
   replacing YOUR_EMAIL with your own email address (retaining the quotes).
3. Check your email for an access token sent from __laji.fi__.
