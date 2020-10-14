---
title: 'Update: IMF World Economic Outlook Database, October 2020'
author: Mitsuo Shiota
date: '2020-10-14'
slug: update-imf-world-economic-outlook-database-october-2020
categories:
  - economics
tags:
  - R
  - Shiny
---

I updated [my shiny app](https://mitsuoxv.shinyapps.io/imf-weo/).

Forecast period has extended from 2021 in April version to 2025. And "Concepts" are not limited.

IMF changed the format of the [download page](https://www.imf.org/en/Publications/WEO/weo-database/2020/October). The link to SDMX Data is not .zip file, but .ashx file. As I don't know how to handle .ashx file in R script, I have decided to download files in a browser.

IMF also changed the formats in search pages, like ["By Countries"](https://www.imf.org/en/Publications/WEO/weo-database/2020/October/select-country-group). I prefer the former format, but will try to be accustomed to the new format.
