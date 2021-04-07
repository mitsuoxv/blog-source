---
title: 'Update: IMF World Economic Outlook Database, April 2021'
author: Mitsuo Shiota
date: '2021-04-07'
slug: update-world-economic-outlook-april-2021
categories:
  - economics
tags:
  - R
  - Shiny
---

I have updated [my Shiny app](https://mitsuoxv.shinyapps.io/imf-weo/) every half a year since April 2019. So this is the fifth iteration. And I believe I could make it more usable this time, as I made some improvements so that:

- You can select multiple areas.
- You can see the values by hovering over a chart.
- You can compare the current forecast with the previous one.
- You can download data as a csv file.

Under the hood, I reconstructed the app as a R package. I could do all of these, as I read the book ["Mastering Shiny" by Hadley Wickham](https://mastering-shiny.org/). Thank you, Hadley.
