---
title: My first package, tqr, is add-on to tsibble
author: Mitsuo Shiota
date: '2019-07-19'
slug: my-first-package-tqr-is-add-on-to-tsibble
categories:
  - economics
tags:
  - R
---

[tqr package](https://github.com/mitsuoxv/tqr) is my first package, and is for my use only for now. This is basically a replacement of [self-made functions I wrote in yellen-dashboard](https://github.com/mitsuoxv/yellen-dashboard/blob/master/Libraries.R). In the package name `tqr`, `tq` comes from `tidyquant package`(https://cran.r-project.org/web/packages/tidyquant/readme/README.html). I added `r` to make it `tqr`.

For my old functions to work, I had to prepare a dataframe of 3 columns named "date", "symbol" and "price". `tqr` package does not require fixed column names, but require a [`tsibble`](https://cran.r-project.org/web/packages/tsibble/index.html) (tbl_ts class) instead. In a `tsibble`, you must specify which columns are `index` (one time pointing column like "date") and `key` (one or more category columns like "symbol"). `tqr` assumes all the other are numeric value columns like "price", otherwise stops in an error. As `tqr` works with more than one numeric value columns (wide format), you don't have to gather to one numeric value column (tidy or long format). Actually, if you need speed, you had better spread to wide format.

A `tsibble` has `interval` attribute, like "1M" for monthly data. (Actual attribute is a list, but is printed like "1M") For a `tsibble` to get the right `interval`, you have to pre-format `index` by functions like `yearmonth` for monthly and `yearquarter` for quarterly data.

Although it takes some steps to convert a `tibble` to a `tsibble`, I think it is worthwhile, as I can check missing rows in a `tsibble`. As missing rows are dangerous to the functions in `tqr` package, I make it require a `tsibble` as an input.

`tq_diff`, `tq_ma`, `tq_gr` and `tq_sa` in the package are, except for requiring a `tsibble`, backward compatible with my old functions. They calculate differences, moving averages, growth rates and seasonally adjusted values respectively.

`tq_diff`, `tq_ma` and `tq_gr` are manufactured by function factory `cal_factory`, and `tq_sa` is manufactured by function factory `cal_factory_ts`. Other function factories are `cal_factory_zoo` and `cal_factory_xts`. When I find myself manufacturing the same function, like maybe `tq_logdiff`, I will add them to the package.
