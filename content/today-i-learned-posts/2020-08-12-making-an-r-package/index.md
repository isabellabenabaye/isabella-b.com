---
title: How to Make an R Package
author: ''
date: '2020-08-13'
slug: making-an-r-package-resources
categories: [100DaysOfCode, rstats, r package, resources]
tags: [100DaysOfCode, rstats, r package, resources]
summary: 'For future reference: a compilation of the resources I used to create my first R package '
reading_time: yes
image:
  caption: ''
  focal_point: ''
  preview_only: true
type: today-i-learned
draft: true
links:
 - name: "package"
   url: https://github.com/isabellabenabaye/ib
   icon_pack: fab
   icon: github
 - name: ""
   url: https://twitter.com/_isabellamb/status/1273095907584638976?s=20
   icon_pack: fab
   icon: twitter
# - name: ""
#   url: https://dev.to/isabellabenabaye/bar-plots-in-bokeh-how-to-embed-them-58d2
#   icon_pack: fab
#   icon: dev
---

I recently created my first R package, [`{ib}`](https://github.com/isabellabenabaye/ib), currently containing my personal `ggplot2` theme and other functions for `ggplot2` for my personal use. Since it was my first time making a package, there was a bit of a learning curve and I wanted to compile all of the resources I used to create it so that I can reference them the next time I make a package.

**Jumping off point:** [Stat 431's Lab 4: Create a Package](https://cal-poly-advanced-r.github.io/STAT-431/Canvas_Pages/Week_4-Packages/Lab_4-Packages-Instructions-Public.html) to get started quickly   
Covers creating the package, version control, setting up preliminaries, pushing to GitHub. What I did that's not in the tutorial: make an [RStudio project for the package](https://r-pkgs.org/workflows101.html#projects), which created my git repository in the same step.

For everything else, I referenced [Hadley Wickham](http://hadley.nz/) and [Jenny Bryan](https://twitter.com/JennyBryan?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)'s [**R Packages**](https://r-pkgs.org/index.html). Links to chapters I used most:
- [Package metadata](https://r-pkgs.org/description.html): Filling out the `DESCRIPTION`
- [R code](https://r-pkgs.org/r.html): `devtools::load_all()`
- [Object documentation](https://r-pkgs.org/man.html): 
  - [The documentation workflow](https://r-pkgs.org/man.html#man-workflow): 
    1. Add roxygen comments to your `.R` files.
    2. Run `devtools::document()` (or press Ctrl/Cmd + Shift + D in RStudio) to convert roxygen comments to `.Rd` files. (`devtools::document()` calls `roxygen2::roxygenise()` to do the hard work.)
    3. Preview documentation with `?`.
    4. Rinse and repeat until the documentation looks the way you want
  - [Documenting functions](https://r-pkgs.org/man.html#man-functions)
  - [Documenting multiple functions in the same file](https://r-pkgs.org/man.html#multiple-man)
  - [Text formatting reference sheet](https://r-pkgs.org/man.html#text-formatting)