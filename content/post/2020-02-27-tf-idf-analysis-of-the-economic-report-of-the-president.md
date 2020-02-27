---
title: Tf-idf analysis of the economic report of the president
author: Mitsuo Shiota
date: '2020-02-27'
slug: tf-idf-analysis-of-the-economic-report-of-the-president
categories:
  - economics
tags:
  - R
---

I have found [“Text Mining Fedspeak” by Len Kiefer](http://lenkiefer.com/2018/07/28/text-mining-fedspeak/), which applies tidytext techniques to analyze the annual Federal Reserve Monetary Policy Report, very interesting. Especially the td-idf analysis part is fascinating, as it reveals what the Fed is talking abount most by year. For example, they talked a lot about “iraq”, “war” and “sars” in 2003, and “subprime” in 2007 and 2008. I could feel the history.

I have got an idea that if I apply the same techniques to the Economic Report of the President, I may know what the Presidents and the fellow Coucil of Economic Advisers talk about most every year. So I have downloaded the reports from 1947 to 2020, and made a new study, ["Tf-idf analysis of the economic report of the president"](https://github.com/mitsuoxv/erp/blob/master/README.md). Tf-idf (term frequency–inverse document frequency) analysis scores high the words which appear frequently in this year’s report, but seldom appear in the other years’ reports. And the highest score over all reports goes to “opioids” in 2020.


