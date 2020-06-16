---
title: "Improving a bad visualization"
summary: "Recreation of a [visualization](https://wellcome.ac.uk/reports/wellcome-global-monitor/2018#&gid=1&pid=9) originally published by Wellcome Global Monitor in 2018."
authors: []
tags: [data visualizations, visualization makeover, Stat 431]
categories: [data visualizations, visualization makeover, rstats]
date: "2020-04-26T00:00:00Z"

image:
  caption: ""
  focal_point: ""
  preview_only: true

links:
 - name: code
   url: https://github.com/isabellabenabaye/cal-poly-advanced-r/blob/master/week_2/02_Advanced_Data_Visualization.Rmd
   icon_pack: fab
   icon: github
 - name: share my tweet
   url: https://twitter.com/_isabellamb/status/1254322222937735170?s=20
   icon_pack: fab
   icon: twitter
---

Recently, I started following [Dr. Kelly Bodwin](https://twitter.com/KellyBodwin) and [Dr. Hunter Glanz](https://twitter.com/hglanz)'s public-facing version of their Stat 431 course at Cal Poly. Weekly, they update and post the materials on the the course's [website](https://cal-poly-advanced-r.github.io/STAT-431/).

The topic for week two was "Advanced Data Visualization", and the first part of the lab was a task to recreate this plot from Wellcome Global Monitor from 2018:

{{< figure src="infographics-countries_by_continent.png" title="" lightbox="true" >}}

This plot is quite problematic. There is no clear `y` variable-- We don't know on what basis the points rise and there could be information loss because of this or an unclear picture of that the author was trying to convey.

In an attempt to address these issues, I decided to focus on the distribution of the views of each region, rather than specific countries. The ticks on the rug each represent a country, so we can see where they are in the distribution. Like the original, the median percentage of people who think vaccines are safe per region is also shown. Unlike the original, I included the full range of the percentages on the axis to put the values into perspective. 

{{< figure src="featured.png" title="" lightbox="true" >}}

The data could also have been visualized using a beeswarm plot, which would allow for highlighting of specific countries as in the original plot.