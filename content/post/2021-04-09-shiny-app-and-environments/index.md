---
title: Shiny app and environments
author: Mitsuo Shiota
date: '2021-04-09'
slug: shiny-app-and-environments
categories:
  - computer science
tags:
  - R
  - Shiny
---

## Motivation

I transformed my Shiny app, [imfweo](https://mitsuoxv.shinyapps.io/imf-weo/), into a R package. GitHub repo is [here](https://github.com/mitsuoxv/imf-weo). In the process, I fell into trouble, as I didn't understand the namespace issues. So I did some experiments, using [the monthApp example in "Matering Shiny"](https://mastering-shiny.org/scaling-packaging.html#single-file), and reading the [Chapter 7.4.3 Namespaces in "Advanced R"](https://adv-r.hadley.nz/environments.html#namespaces). Both books are written by Hadley Wickham. As always, thank you, Hadley. I write this post which shows my understanding as of today to help future me.

## Namespace issues

"Where does a function find non-argument variables, like a function name and a data name?" I call this namespace issues.

## Experiments using [the monthApp example in "Matering Shiny"](https://mastering-shiny.org/scaling-packaging.html#single-file)

- A single file: Ctl + Shift + Enter, it works fine, and Global Environment is empty.
- A single file: Ctl + Enter, eack line works fine, and Global Environment is filled with function names like `birthstoneServer` and a data name like `stones` 

This experiment suggests that the usual way, Ctl + Shift + Enter in app.R, runs in a function execution environment, not in Global Environment. Let us call this environment monthApp execution environment, even if monthApp is not yet here. I guess the file name `app.R` is so special that it creates a function which encloses all the codes.

- A single file: Change `stones` to `units`, and Ctl + Shift + Enter, it still works.

Don't forget to restart R at each experiment. Note that `units` is a function name in Base Environment. As `birthstoneServer` function is defined in monthApp execution environment, it can find `units` there.

- Module files: Ctl + Shift + Enter, and you will see "Error: object 'stones' not found"
- Module files: Ctl + Enter, `stones <- vroom::` line, and create `stones` in Global Environment. And then, Ctl + Shift + Enter, it works fine.
- Module files: Change `stones` to `units`, Ctl + Shift + Enter, and you will see "Error: object of type 'closure' is not subsettable".
- Module files: Then, create `units` in Global Environment, it works fine.

Let us call the environment in which variables, such as `birthstoneServer` function, are defined, R directory environment: monthApp execution environment is its ephemeral child environment, and Global Environment is its parent environment. Look at the last figure in [Chapter 7.4.3 Namespaces in "Advanced R"](https://adv-r.hadley.nz/environments.html#namespaces), and insert R directory environment left to Global Environment. As there is no namespace: R directory environment, `birthstoneServer` function searches `stones` or `units` only in the lower row of the figure. If `stones` or `units` is in Global Environment, it can find there. If not, it can't find `stones`, or can find `units` as a function in Base Environment.

- Module files: Create a new file `stones.R` and move `stones <- vroom::` line there, and it works fine.
- Module files: Change `stones` to `units`, create a new file `units.R` and move `units <- vroom::` line there, and it works fine.

In this case, `stones` or `units` and `birthstoneServer` exist in the same R directory environment, so `birthstoneServer` can find `stones` or `units` there before searching Base Environment, or even Global Environment.

- A package: Leave `stones <- vroom::` line in monthApp: "Error: object 'stones' not found"
- A package: Leave `stones <- vroom::` line in monthApp: Then create `stones` in Global Environment, and it works fine.
- A package: Leave `stones <- vroom::` line in monthApp: Change `stones` to `units`, and "Error: object of type 'closure' is not subsettable"
- A package: Leave `stones <- vroom::` line in monthApp: Change `stones` to `units`, and create `units` in Global Environment. Still, "Error: object of type 'closure' is not subsettable"

Now it is a package. Let us call it monthApp package. Insert `package: monthApp` right to Global Environment, and `namespace: monthApp` left to `namespace: stats` in the same last figure in [Chapter 7.4.3 Namespaces in "Advanced R"](https://adv-r.hadley.nz/environments.html#namespaces). `birthstoneServer` function searches from the top left. If `stones` is in Global Environment, it finds there, and if not, it can't find. Whether or not `units` is in Global Environment, it finds `units` as a function in `namespace: base` in the top right before searching Global Environment.

- A package: Take optional extra, and create `data/stones.rda`: It works fine.
- A package: Take optional extra, and create `data/units.rda`: "Error: object of type 'closure' is not subsettable"

Taking optional extra to create a package dataset is to make sure `stones` or `units` is in Global Environment. So the results are the same as above in case `stones` or `units` exists in Global Environment.

## For best practices

I don't know what are the best practices at this moment. Joe Cheng recommends to preprocess out of Shiny what all Shiny users do in [this Youtube lecture](https://www.youtube.com/watch?v=Wy3TY0gOmJw). As for `imfweo` package, I followed his recommendation, and created a lot of .rda files in data directory. `units.rda` happened to be there, and I faced "Error: object of type 'closure' is not subsettable". As a solution, I first created a list, like `weo$meta$units`, and hoped `weo` doesn't match any namespace before Global Environment. In the second thought, as I update data every half a year and can compare the current one with the previous one in rolling, I decided to pass every data variable as an argument. As result, I can be sure there will be no accidental match in namespaces, but the codes have become more difficult to read, as there are so many non-reactive arguments.

I am not a developer but a practitioner. Environments are hard to understand. Future me, if you are confused, come back to this post.
