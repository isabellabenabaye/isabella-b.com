---
title: 'Looking at The Office’s IMDb Ratings and Writers'
author: Isabella Benabaye
date: '2020-03-29'
reading_time: true
slug: tidy-tuesday-the-office
categories: []
tags:
  - Data Visualizations
  - Tidy Tuesday
  - rstats
summary: '[Tidy Tuesday](https://github.com/rfordatascience/tidytuesday)’s Week 12 dataset from the [`schrute` R package](https://bradlindblad.github.io/schrute/index.html) and data.world'
authors: []
external_link: ''
image:
  caption: ''
  focal_point: ''
  preview_only: yes
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''
slides: ''
---

The data this week comes from the [`schrute` R package](https://bradlindblad.github.io/schrute/index.html) for *The Office* transcripts and [data.world](https://data.world/anujjain7/the-office-imdb-ratings-dataset) for IMDb ratings of each episode. The featured article is [The Pudding’s](https://pudding.cool/) [‘The Office’ Dialogue in Five Charts](https://pudding.cool/2017/08/the-office/), which is ‘a breakdown of how every character contributed to the show’.  
<br />

## Ratings

*There are 188 The Office episodes.*

The first visualization I made was of the episode ratings of the entire
series, grouped by season. The width of the violin plot indicates the
density of the episodes with that particular rating.   
{{% staticref "files/tidy-tuesday/The Office IMDb Ratings.png" %}}![Source: data.world. Graph: Isabella
Benabaye.](https://github.com/isabellabenabaye/tidy-tuesday/blob/master/2020/12_theoffice/The%20Office%20IMDb%20Ratings.png?raw=true){{% /staticref %}}
Labeled above are the
highest rated episodes per season, except in the cases of season 1 and
8, which have their lowest rated episodes labeled. Unsurprisingly, those
two seasons were the lowest rated overall of the whole series. “Goodbye,
Michael” and “Finale” are tied with the highest IMDb ratings of 9.7,
with another fan favorite “Stress Relief” coming in second with a rating
of 9.6.  
<br />

## Writers

I also wanted to look into who wrote the episodes and see if there were
any particular writers who did the most episodes.  
{{% staticref "files/tidy-tuesday/The Office Writers.png" %}}![Source: `schrute`. Graph: Isabella
Benabaye.](https://github.com/isabellabenabaye/tidy-tuesday/blob/master/2020/12_theoffice/The%20Office%20Writers.png?raw=true){{% /staticref %}} 
Mindy Kaling wrote 20 episodes
(including “Goodbye, Michael” 💗), while BJ Novak wrote the second
most at 15. Gene Stupnitsky and Lee Eisenberg are next with 14. There
were 10 episodes without writer data.    
<br />

**Other questions I wanted answered but didn’t/couldn’t make
visualizations about:**

  - Highest rated episodes - who wrote them? Who was in them?
      - Mindy Kaling, Greg Daniels, and BJ Novak each wrote three of
        episodes with the highest IMDb ratings (\>= 9). If the episode
        “Niagara” about Pam & Jim’s wedding is to be considered as two
        episodes, Mindy and Greg (who wrote both) would each have
        writted four.
  - What is the average rating of each writer’s episodes?
      - Can be found in the table below:

| writer                | avg\_rating | episode\_count |
| :-------------------- | ----------: | -------------: |
| Mindy Kaling          |    8.405000 |             20 |
| B.J. Novak            |    8.486667 |             15 |
| Gene Stupnitsky       |    8.385714 |             14 |
| Lee Eisenberg         |    8.385714 |             14 |
| Greg Daniels          |    8.575000 |             12 |
| Paul Lieberstein      |    8.250000 |             12 |
| Brent Forrester       |    8.410000 |             10 |
| Justin Spitzer        |    8.360000 |             10 |
| Jennifer Celotta      |    8.388889 |              9 |
| Michael Schur         |    8.488889 |              9 |
| Charlie Grandy        |    8.037500 |              8 |
| Aaron Shure           |    8.033333 |              6 |
| Daniel Chun           |    8.333333 |              6 |
| Halsted Sullivan      |    8.033333 |              6 |
| Warren Lieberstein    |    8.033333 |              6 |
| Carrie Kemper         |    7.675000 |              4 |
| Owen Ellickson        |    7.450000 |              4 |
| Robert Padnick        |    8.125000 |              4 |
| Allison Silverman     |    7.433333 |              3 |
| Steve Hely            |    7.866667 |              3 |
| Amelie Gillette       |    8.500000 |              2 |
| Anthony Q. Farrell    |    8.700000 |              2 |
| Dan Greaney           |    7.800000 |              2 |
| Dan Sterling          |    7.900000 |              2 |
| Graham Wagner         |    8.000000 |              2 |
| Jon Vitti             |    7.850000 |              2 |
| Jonathan Green        |    7.750000 |              2 |
| Lester Lewis          |    8.300000 |              2 |
| Nicki Schwartz-Wright |    8.300000 |              2 |
| Ricky Gervais         |    7.900000 |              2 |
| Ryan Koh              |    8.200000 |              2 |
| Steve Carell          |    9.000000 |              2 |
| Gabe Miller           |    7.750000 |              2 |
| Stephen Merchant      |    7.900000 |              2 |
| Caroline Williams     |    8.800000 |              1 |
| Jason Kessler         |    6.800000 |              1 |
| Jonathan Huges        |    7.800000 |              1 |
| Larry Willmore        |    8.200000 |              1 |
| Peter Ocko            |    7.500000 |              1 |
| Tim McAuliffe         |    8.000000 |              1 |
