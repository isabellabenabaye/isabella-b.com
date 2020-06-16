---
title: "Who is being killed by local police in Los Angeles County?"
summary: "The [Los Angeles Times](https://www.latimes.com/) recently released their [database](https://github.com/datadesk/los-angeles-police-killings-data) of people who died at the hands of police in L.A. County since 2000. After reading their [article](https://www.latimes.com/projects/los-angeles-police-killings-database/) about it, I wanted to learn a little more about the two communities affected the most, particularly the Black community."
authors: []
tags: [data visualizations, rstats, ggplot2, L.A. police killings]
categories: [data visualizations, rstats, ggplot2]
date: "2020-06-13"

image:
  caption: ""
  focal_point: ""
  preview_only: true

links:
 - name: "code"
   url: https://github.com/isabellabenabaye/los-angeles-police-killings
   icon_pack: fab
   icon: github
 - name: "source"
   url: https://github.com/datadesk/los-angeles-police-killings-data
 - name: ""
   url: https://twitter.com/_isabellamb/status/1272047145554567168?s=20
   icon_pack: fab
   icon: twitter
---

The [Los Angeles Times](https://www.latimes.com) published an [article](https://www.latimes.com/projects/los-angeles-police-killings-database/) on June 9 that went into the details of the killings by local law enforcement in Los Angeles County that were ruled a homicide since 2000. It was striking to me how in the last 20 years and after almost **900 deaths**, only **two officers were charged** as a result of shooting a civilian  while on duty. The Times shows the trend of deaths over time, highlighted how some communities are disproportionately affected by police violence, map the deaths across the county, and honor those who died by listing each and every one of their names. They discuss and visualize more, and I recommend you check it out. [<i class="fas fa-external-link-square-alt"></i>](https://www.latimes.com/projects/los-angeles-police-killings-database/)

At the end of the article they mention their source and announce that The Times has released their database of police killings to the public and direct you to its repository on [github](https://github.com/datadesk/los-angeles-police-killings-data). Struck by information they presented, I wanted to learn more about those who were killed.

<center>
<p class="btn-articles"><a href="/blog/los-angeles-police-killings/#full-graphic" class="btn btn-articles"><i class="far fa-chart-bar"></i> full graphic </a>
</p></i>
</center>
<br>

{{% alert look %}}
**About the data**: 
The data for the plots was extracted on June 13, 2020. At the time there were 885 recorded deaths. Almost all relevant fields were complete except for 3 people missing a recorded race, one without a gender & cause of death, and 7 with some details about where the deaths took place missing.
{{% /alert %}} 

For the following descriptives, I looked at all of the deaths since 2000.     
#### Race
As the L.A. Times mentioned and as you can see in the plot of theirs that I recreated, almost **80%** of the people killed were **Latino or Black**. By comparing the percentages of the populations and deaths we can see how disproportionately they're affected, particularly the Black community. 
{{< figure src="perc_plot.png" title="" lightbox="true" >}}

#### Cause of death 
**870 (98%)** of the 885 deaths were caused by a gunshot.
{{< figure src="cause_all.png" title="" lightbox="true" >}}

#### Where the person died
There was an overwhelming amount of people who were killed in **Long Beach**, with the count being more than double that of Compton, the area with the second most frequent killings.
{{< figure src="top_5_neighborhoods_all.png" title="" lightbox="true" >}}
When we look at the neighborhoods in which Black and Latino people were killed the most, we can see that they both have Long Beach in common. As mentioned by the L.A. Times, these neighborhoods with the most killings are home to many Black and Latino residents.
{{< figure src="neighborhoods.png" title="" lightbox="true" >}}

#### Age at time of death
L.A. Times showed the distribution of the ages of all of those killed by law enforcement, so instead I looked into the ages of those who were Black and Latino. Like the distribution of all people, most of them were in their **20s** and **30s**.
{{< figure src="ages.png" title="" lightbox="true" >}}

In addition, I checked to see if there was a pattern in the frequency of the killings by visualizing how many there were per month. There didn't seem to be one, but I did learn there were only **4 months in those 20 years that no one died at the hands of police**.

#### Full graphic
{{< figure src="featured.png" title="👆 enlarge" lightbox="true" >}}

