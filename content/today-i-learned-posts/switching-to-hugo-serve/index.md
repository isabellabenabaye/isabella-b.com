---
title: Switching to `hugo serve` instead of `blogdown::serve_site()`
author: ''
date: '2020-06-07'
categories: [100DaysOfCode, hugo, blogdown]
tags: [100DaysOfCode, hugo, blogdown]
summary: 'Should have done it sooner, it’s so much faster.'
reading_time: yes
image:
  caption: ''
  focal_point: ''
  preview_only: no
type: today-i-learned
---

Today I came across [Dr. Mowinckel](https://twitter.com/DrMowinckels)'s blog post about [changing her `blogdown` workflow](https://drmowinckels.io/blog/changing-you-blogdown-workflow/) and decided to change mine as well. I already used page bundles for this site, but always made them manually instead of using `blogdown`-- before reading her post I hadn't known it was possible to confidure `blogdown` to do so. 

The process also required that instead of using `blogdown::serve_site()`, you had to run `hugo serve` in the terminal, which you can do from RStudio. I haven't tried the forced knitting to `.md` yet, but since she mentioned that she liked `hugo serve` better than the `serve_site()`, I wanted to try it out immediately. 

In my case, `serve_site()` has always been slow, and I didn't like that it wouldn't render if I made changes to `.scss` files. That was no longer the case with `hugo serve`! It's much more convenient for me now that it renders automatically, and the rendering time is ***much* faster**. If you're a `blogdown` user, I recommend you try it!