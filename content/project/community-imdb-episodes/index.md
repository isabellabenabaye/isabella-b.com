---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "IMDb ratings of all 110 Community (2009 - 2015) episodes"
summary: ""
authors: []
tags: [web scraping, data visualizations]
categories: [web scraping, data visualizations]
date: "2020-05-09T00:00:00Z"
slug:

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
links:
 - name: code
   url: https://github.com/isabellabenabaye/community-project
   icon_pack: fab
   icon: github
 - name: dataset
   url: https://www.kaggle.com/imbenab/community-episodes-imdb-ratings
   icon_pack: fab
   icon: kaggle
---

First of all, Community is a gem and if you haven't seen it, you should.

On May 9, 2020 I scraped the IMDb ratings of all 110 [Community](https://en.wikipedia.org/wiki/Community_(TV_series)) episodes in honor of their [May 18, 2020 reunion](https://www.cnet.com/news/the-community-reunion-with-donald-glover-is-happening/) to raise money for two coronavirus relief efforts. You can find the dataset on [kaggle](https://www.kaggle.com/imbenab/community-episodes-imdb-ratings). I also made a [tutorial](http://isabella-b.com/blog/scraping-episode-imdb-ratings-tutorial/) describing step-by-step how I scraped the episodes.

After scraping, I wanted to visualize the ratings. In general, the Community episodes were pretty highly rated-- the average rating being 8.3. The lowest and highest ratings were 6.8 and 9.8, respectively. In order to compare them among each other and among the other seasons, I made a heatmap of them with a diverging color palette using Seaborn.

{{< figure src="Community Episodes Ratings - Heatmap.png" title="" lightbox="true" >}}

The red and blue make it easy to see which are the series' worst and best episodes. Clearly, season 4 was the lowest rated of all the seasons. That was also the season that Dan Harmon, the show's creator, was replaced as showrunner of the series and the last season of Chevy Chase, a member of the core cast. It also marked the departure of other producers and writers, including frequent episode directors and executive producers Anthony and Joe Russo. Harmon returned as showrunner for seasons 5 and 6.

We can also see that the series mostly ended each season strong and that the first half of the series was generally higher rated than the second half.

To check out the distributions of each season and visualize them in a different way, I made a beeswarm plot. To make it, I used my visualization tool of choice, R and `ggplot2`. The annotated episodes are the two highest rated, season 1's episode 23 "Modern Warfare" & season 3's episode 4 "Remedial Chaos Theory", both with a rating of 9.8, along with the final episode and the last appearances of two of the core cast members.

{{< figure src="Community Episodes.png" title="" lightbox="true" >}}

