---
title: "Likelihood and model fit: A visual tour"
date: "2021"
authors:
  - admin
type: book
weight: 10
highlight: false
tags:
  - Tutorial
  - Likelihood
  - Non-linear data
menu:
  learning:
    parent: Talks and Tutorials
    weight: 3
---
Likelihood is a concept that underlies most statistical modeling that falls under the heading of [generalized linear model](https://en.wikipedia.org/wiki/Generalized_linear_model) or GLMs. 


When we fit any kind of statistical model to a dataset, the goal is to find solutions that either maximize the likelihood of the data, given the model (under a frequentist, maximum likelihood estimation framework), or maximize the likelihood of the data given the data and some prior information on the value of the parameters (under a more Bayesian framework).In this tutorial, we will introduce some key concepts and tools for smoothing and visualizing potentially non-linear data. We will focus on local regression techniques for continuous outcomes, e.g. BMI, blood pressure, etc, in in one dimension, e.g. in response to some exposure, and in two dimensions representing x and y spatial coordinates. In a future tutorial we will look at complementary approaches to spatial density estimation which let us estimate the probability of an event occurring in space that build on the concepts discussed in this tutorial.

[Check out the full tutorial here.](https://sph-umich.shinyapps.io/modelfit/)