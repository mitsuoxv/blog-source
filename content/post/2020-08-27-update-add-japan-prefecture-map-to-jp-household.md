---
title: 'Update: add Japan prefecture map to jp-household'
author: Mitsuo Shiota
date: '2020-08-27'
slug: update-add-japan-prefecture-map-to-jp-household
categories:
  - economics
tags:
  - R
  - Shiny
---

I have added Japan prefecture map to ["jp-household"](https://github.com/mitsuoxv/jp-household) and [my Shiny app "City competition to consume"](https://mitsuoxv.shinyapps.io/jp-household/). To make the capital city represent each prefecture, I drop 5 non-capital cities.

I use shape data from [NipponMap package](https://cran.r-project.org/web/packages/NipponMap/index.html), and refer to ["13.19 Creating a Map from a Shapefile"](https://r-graphics.org/recipe-miscgraph-map-shapefile) in "R Graphics Cookbook, 2nd edition" by Winston Chang.

This kind of visualization helps us understand which region tends to consume more or less of certain items. For example, go to [my Shiny app](https://mitsuoxv.shinyapps.io/jp-household/), select item level 5, and select item 282 納豆　(fermented soybeans). You can see the western region consumes less, and the eastern region consumes more in 2019. Select different year between 2007 and 2019, you will see this pattern is pretty consistent.

I am now wondering if and how I can quantify this consistency by each item.
