---
title: 'Update: add USA map to Covid-19 app'
author: Mitsuo Shiota
date: '2021-03-03'
slug: update-add-usa-map-to-covid-19-app
categories:
  - economics
tags:
  - R
  - Shiny
---

I have added "in the United States (map)" panel to [Covid-19 app](https://mitsuoxv.shinyapps.io/covid/). Click the arrow, located in the right below the slider bar, you can see how novel corona virus has spread in the United States in animation. Note the color denotes relative, not absolute, hotness, as the legend changes over time.

In January 2020, it landed from China in the West Coast, but failed to spread. However, in spring, it landed again, this time from Europe in the East Coast, especially New York, and spread to the Mid West, and then to the South and the West, such as Arizona. It turned to north, and arrived at North Dakota. And it spread again to the South and the West. Now, as of the end of February 2021, New York is again one of the hot states. I guess new variants have arrived from Europe, South Africa and Brazil, and native new variants have appeared. I hope vaccines will be effective enough to contain new variants.

I was watching the United States situation in ["USA, Covid-19 situation by state"](https://github.com/mitsuoxv/covid/blob/master/USA.md) using static maps, and wished to make animated maps. I happened to read some parts of ["Mastering Shiny" by Hadley Wickham](https://mastering-shiny.org/), and found it is fairly easy to add animate functionality to Shiny app. It is just to set `animate = TRUE` in `sliderInput` function. I first added animate functionality to my other Shiny app, ["City competition to consume"](https://mitsuoxv.shinyapps.io/jp-household/).

Today, I turned to Covid-19 app. At first, it worked fine locally, but failed in shinyapps.io. I struggled a while. Finally I added `library(mapproj)` to app.R, and somehow it worked. I guess `library(maps)` automatically loads `mapproj` in the local RStudio IDE, but it doesn't in shinyapps.io.
