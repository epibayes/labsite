---
title: Reproducibility starts at home
subtitle: originally published online on May 31, 2016 at https://www.jonzelner.net/
summary: Reproducibility and some examples.
authors:
- admin
tags: []
categories: ["post"]
date: "2016-05-31T00:00:00Z"
lastMod: "2020-08-18T00:00:00Z"
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ""
  focal_point: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
Reproducibility is becoming more and more a part of the conversation when it comes to public health and social science research. A lot has been said about [p-hacking](https://en.wikipedia.org/wiki/Data_dredging), the file drawer effect, and other subtle and unsubtle biases that can make replicating published results difficult with new data. The importance of these issues is now so well-recognized that we commonly talk about a *reproducibility crisis* in public health and the social sciences.

But comparatively little has been said about another dimension of the reproducibility crisis, which is the difficulty of re-generating already-complete analyses using the *exact same input data*. But as far as I can tell, the ability to do this is a necessary precondition to the new-data replication. The code underlying our figures, estimates and conclusions is the most complete description of what we did, and if we can’t share these in a meaningful way, there’s very little hope that others will be able to replicate our results.

But I think the ease with which we can re-generate complete analyses, on our own computers and those of others, plays directly into the bigger questions of openness and integrity that underlie some of the challenges to reproducibility. Many of you will have experienced the shiver of fear that comes from reviewer comments suggesting that a group of cases should or should not have been dropped, or that a variable should have been coded in a different way.

My first reaction in such situations has historically involved a slightly queasy feeling as I imagine laboriously stepping through each of the downstream things that has to happen (re-run models, re-generate figures, re-construct tables!) all as a result of a small modification of the way input data were cleaned or transformed.

The friction involved in making these changes increases the incentive to cut corners and to not take potentially useful feedback seriously. It also makes it difficult to do incorporate new data as it becomes available, perform sensitivity analysis by re-running the analysis on perturbed datasets, etc.

In truth, structuring research in a way that allows us to replicate every step from data cleaning to analysis to the final paper including the results, requires a kind of forethought and planning that many of us - I’ll speak at least for myself - don’t bring to the early stages of most projects. As a result, we end up with finished papers backed by a morass of [spaghetti code](https://en.wikipedia.org/wiki/Spaghetti_code) that we hope to never to have to run again.

## New(ish) Tools for Old Problems
I have been experimenting with ways to turn the ship around and have been encouraged with the results. I’ve found that a few tools - some old ([GNU Make](https://en.wikipedia.org/wiki/Make_(software)), I’m looking at you!), some new ([Docker](http://www.docker.com/), [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration)) - have made my workflow smoother and more transparent.

But most importantly, they have significantly lessened that shiver of fear: finding errors in data cleaning and analysis is no longer quite as terrifying as it used to be, and I find myself more inclined to think of my various projects as being about cultivating a living entity that can grow and change over time, rather than a mad dash to a static endpoint.

So, over the next few posts, I’m hoping to talk about how these pieces have come together for me. I want to state upfront that I am far from the first person to talk about the fruitful application of tools from software engineering to research. In particular, a number of ideas here are taken from [Kieran Healy](https://kieranhealy.org/resources/) and [Mike Bostock](https://bost.ocks.org/mike/make/) and Christopher Gandrud’s [excellent book](http://www.amazon.com/Reproducible-Research-Studio-Second-Chapman/dp/1498715370?ie=UTF8&keywords=reproducible%20research%20with%20R&qid=1464791322&ref_=sr_1_1&sr=8-1) on reproducible research with R.

What I want to really get across here is why thinking like a programmer and using the tools of software development is not only commendable, but necessary, when doing statistical and computationally-intensive research.

## A Worked Example
Talking about reproducibility in the abstract is useful, but it doesn’t do the thing we really need to do, which is to bring the component parts together into a whole that can be run (and re-run!) anywhere. So, all of the elements of reproducibility I will discuss over the next series of posts are collected [here](https://gitlab.com/jzelner/reproducible-stan), which is a git repository demonstrating a toy example of a project using R and [Stan](http://mc-stan.org/) that can be fully replicated.

Specifically, it’s focused on fitting a Gaussian [finite mixture model](https://en.wikipedia.org/wiki/Mixture_model) to simulated data. Here’s what the output should [look like](https://dl.dropboxusercontent.com/s/e99l7q4c3toderd/mixture_model_output.pdf).

I picked R and Stan for this because they are what I live and breathe in my day-to-day research. But I also chose this example because raw MCMC output can be a bit unwieldy to work with and is a good example of the kind of thing that can cause replication/re-generation headaches if not handled properly. But the upside to engaging with the added complexity of Stan and MCMC in general is more than worth the effort, and with the right tools the cost of doing so can be minimal.

Beyond this, the ideas here are relevant to any and all statistical analysis, and particularly to simulation-based analyses like individual-based models that generate lots of output for which cleaning, processing, and presentation can be tedious.

So, without further ado, here’s what I’ve learned about reproducing my own work (so far). (This list will expand as new tutorials are completed and I think of new things to add):

[Part 1: Your R script is a program!](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/script-is-a-program/)

[Part 2: Makefiles for fun and profit](https://www.jonzelner.net/statistics/make/reproducibility/2016/06/01/makefiles/)

[Part 3: Knotes on Knitr](https://www.jonzelner.net/knitr/r/reproducibility/2016/06/02/knitr/)

[Part 4: It’s not reproducible if it only runs on your laptop.](https://www.jonzelner.net/docker/reproducibility/2016/06/03/docker/)

[Part 5: Bringing it all together with Gitlab CI](https://www.jonzelner.net/docker/gitlab/ci/reproducibility/2016/06/06/gitlab-ci/)