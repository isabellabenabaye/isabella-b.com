---
title: '{ib} - My First R Package'
author: Isabella Benabaye
date: '2020-08-12'
slug: ib-r-package
categories:
  - rstats
  - r package
tags:
  - rstats
  - r package
subtitle: 
summary: A personal R package currently containing functions for `ggplot2`.
image:
  caption: ''
  focal_point: ''
  preview_only: yes
links:
 - name: "package"
   url: https://github.com/isabellabenabaye/ib
   icon_pack: fab
   icon: github
# - name: ""
#   url: https://twitter.com/_isabellamb/status/1281368436073836545?s=20
#   icon_pack: fab
#   icon: twitter
---

I've been busy and haven't been able to code in R for around 3 weeks now, and as my first project back, I decided to do something I've been wanting/planning to do for a while now: make a personal R package.

#### Background
Originally, I had intended to create a themes package called `ibthemes` for myself to speed up my plotting process both when doing EDA (viewing plots in the plots pane) and creating visualizations that I'll be saving. While writing the functions I instead decided to rename the package to `ib` and change its purpose from a plotting package to a general package containng functions for my personal use, since I realized I'll probably be creating more non-`ggplot2` functions at some point in time and would want them all in one place.

#### Functions
As of now, it only contains 6 functions, all for use when creating plots with `ggplot2`:

- **`theme_ib`:** A simple `ggplot2` theme in my personal style. By default (`plots_pane = FALSE`), the theme adjusts the text sizes for printing. `plots_pane = TRUE` is meant to be used when viewing plots in the plots pane and text sizes are not adjusted. There is also an option (`md = TRUE`) to use markdown theme elements from `ggtext` instead of `element_text()`.

- **`update_geom_fonts_ib`:** Update font defaults for text geoms to match `theme_ib`

- **`scale_x_c_ib`:** Sets default values for the `expand` argument of `scale_x_continuous` that adds 0.5 units of space on both sides of the plot

- **`scale_x_d_ib`:** Sets default values for the `expand` argument of `scale_x_discrete` that adds 0.5 units of space on both sides of the plot

- **`scale_y_c_ib`:** Sets default values for the `expand` argument of `scale_y_continuous` such that there is no space below the lowest value and the top end of the plot is extended by 5% (eg. for use with bar plots)

- **`scale_y_d_ib`:** Sets default values for the `expand` argument of `scale_y_discrete` such that there is no space below the lowest value and the top end of the plot is extended by 5% (eg. for use with bar plots)