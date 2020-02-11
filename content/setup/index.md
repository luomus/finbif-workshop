---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "FinBIF R Workshop Software Setup"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: ""
lastmod: 2020-02-11T13:24:31Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Attendees of the workshop are expected to bring their own computer and be able
access the internet wirelessly at the workshop venue (e.g., using eduroam or the
attendees own mobile internet access).

Before the workshop begins the attendees will need to have the most up to date
versions of the R programming environment, the RStudio development environment
and the FinBIF R package, and have obtained a FinBIF API access token.

Instructions for how to install these software and obtain an access token are
found below.

## Download and install R
Attendees first need a working installation of R. Follow the instructions for
your computer's operating system.

### For Windows
1. Download R from [here](https://cloud.r-project.org/bin/windows/base) by
   clicking the link "Download R _X_ for Windows" and saving the file
   "R-_X_-win.exe" (where _X_ is the current version of R---at the time of
   writing, 3.6.2) to your computer.
2. Run the installer by double clicking on the downloaded file.
3. Install R by accepting the default options in the installer.

### For macOS
1. Download R from [here](https://cloud.r-project.org/bin/macosx) by clicking
   the link "R-_X_.pkg" and saving the file "R-_X_.pkg" (where _X_ is
   the current version of R---at the time of writing, 3.6.2) to your computer.
2. Run the installer by double clicking on the downloaded file.
3. Install R by accepting the default options in the installer.

## Download and install RStudio
Attendees will interact with the R programming language via the RStudio
development environment. The RStudio Desktop application is available
[here](https://rstudio.com/products/rstudio/download/#download).

Follow the instructions for your operating system,

### For Windows
1. Download the file RStudio-_X_.exe (where _X_ is the current version of
   RStudio Desktop---at the time of writing, 1.2.5033).
2. Run the installer by double clicking on the downloaded file.
3. Install RStudio Desktop by accepting the default options in the installer.

### For macOS
1. Download the file "RStudio-_X_.dmg"" (where _X_ is the current version of
   RStudio Desktop---at the time of writing, 1.2.5033).
2. Mount the disk image by double clicking on the downloaded file.
3. Install RStudio Desktop by dragging the RStudio applications icon to the
   "Applications" folder.

## Install the FinBIF R package
The workshop material is focused on the use of the R package finbif which allows
users to access data from FinBIF directly from within R. To install the package
follow these instructions:

1. Open the RStudio Desktop application.
2. Click on "Tools" in the top menu bar.
3. Click on "Install Packages" in the drop-down menu.
4. Type `finbif` into the "Packages" text input box.
5. Click "Install".

## Request a FinBIF access token
To access data from FinBIF via the finbif R package requires a personal access
token. To obtain an access token follow these instructions.
1. Click on the "Console" pane and type `library(finbif)` followed by the return key.
2. Still in the "Console" pane, type `finbif_request_token("YOUR_EMAIL")`
   replacing YOUR_EMAIL with your own email address (retaining the quotes).
3. Check your email for an access token sent from "noreply@laji.fi".
