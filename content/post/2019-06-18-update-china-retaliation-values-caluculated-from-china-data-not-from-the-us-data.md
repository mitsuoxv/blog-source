---
title: 'Update: China retaliation values caluculated from China data, not from the
  US data'
author: Mitsuo Shiota
date: '2019-06-18'
slug: update-china-retaliation-values-caluculated-from-china-data-not-from-the-us-data
categories:
  - economics
tags:
  - R
---

I have added [a new page](https://github.com/mitsuoxv/us-tariffs-on-china/blob/master/China-hits-back2.md) to [US tariffs on China](https://github.com/mitsuoxv/us-tariffs-on-china) repo.

When I played with the US customs data, [I guessed that Chinese calculated the retaliation values based on HS 6 digit codes, while they actually impose tariffs based on HS 8 digit codes](https://github.com/mitsuoxv/us-tariffs-on-china/blob/master/China-hits-back.md). Later I have learned that HS codes are not so harmonized, and that HS codes can be different between the US and China. I have felt uneasy about my guess. So I have looked for the China customs data. In [this new page](https://github.com/mitsuoxv/us-tariffs-on-china/blob/master/China-hits-back2.md), I have got the HS 6 digit data reported by China from [UN Comtrade](https://comtrade.un.org/), and found that China data also support my guess.
