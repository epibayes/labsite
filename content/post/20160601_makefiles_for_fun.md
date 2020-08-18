---
title: Makefiles for fun and profit
subtitle: originally published online on June 01, 2016 at https://www.jonzelner.net/
summary: All about Makefiles
authors:
- admin
tags: []
categories: []
date: "2016-06-01T00:00:00Z"
lastMod: "2020-08-18T00:00:00Z"
featured: true
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
**Note: This post is part of a series on reproducibility. With any luck, it will make sense on its own. But it may be helpful to start from [the beginning](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/reproducibility-pt-1/).**

For me, much of the fun and challenge of research and programming lies in the artful management of complexity. A well-executed analysis is usually one with a number of moving parts. There’s the usual data cleaning/transformation/analysis/figures pipeline, of course. But within that, there may be additional complications: sub-analyses, complex figures (e.g., maps!), and computationally intensive posterior simulations.

Without tools to manage these moving parts and their interactions, the process of adding new and interesting components to a project can be onerous. And we may feel tempted to step away from our larger ambitions, particularly when confronted with the high likelihood of having to change and re-run everything in response to feedback, either from colleagues and peers or through the review process.

One way to handle this complexity is by using Makefiles, which allow us to document the dependencies between different steps of an analysis, and then update everything using the `make` command at the Mac or Linux/Unix command line.

You can find the Makefile for the reproducible Stan example [here](https://gitlab.com/jzelner/reproducible-stan/blob/master/Makefile). In this quick tutorial, we’ll go through it step-by-step.

Much has been said about Makefiles, both for research using R and otherwise. In particular, Christopher Gandrud’s *[Reproducible Research with R and Rstudio*](https://www.amazon.com/Reproducible-Research-Studio-Second-Chapman/dp/1498715370/ref=sr_1_1?ie=UTF8&qid=1464791322&sr=8-1&keywords=reproducible+research+with+R)* provided much of the motivation to me to adopt Make in my own R workflow. So I’m going to stick to a few key things that I learned along the way that make the ideas from this book and other sources on Make just a bit easier.

## A Make Primer
With that said, here’s the idea behind `make`. Each Makefile is composed of a series of recipes of the following form:

(Please forgive the red blocks in the Makefile code snippets; working on clearing up the syntax-highlighting bug!)

        bar.csv : foo.R
          ./foo.R

To the left of the colon is the *target* of the recipe and to the right is a list of one or more *prerequsites*. What this particular recipe says is “when foo.R changes, re-run foo.R to produce bar.csv”. To do this, Make looks at the timestamps on the files and sees when they were last changed. So if we make some change to `foo.R` and save it, its timestamp will be later than the one on `bar.csv`, and Make will re-run this recipe to generate a new `bar.csv` that reflects these new changes.

The power of Make comes into play when we have something else that depends on `bar.csv`:

        bar.pdf : bar_chart.R bar.csv
          ./bar_chart.R -d bar.csv

What this recipe says is that when `bar.csv` changes, we should re-generate the figure `bar.pdf` using the R script `bar_chart.R`. You can see that we now have two prerequisites: `bar_chart.R` and `bar_chart.R`. This tells Make to re-generate `bar.pdf` if either of these changes. Now, if we make a small change to `foo.R` or `bar_chart.R` and type Make, our figure will be re-generated automatically.

## Make in the real world
You can probably see why this would be useful in the context of re-generating results for a paper. In our [toy example](https://gitlab.com/jzelner/reproducible-stan) of simulating from a Gaussian mixture model and fitting an MCMC model to the simulation output, there are a number of steps to manage:

1. Convert input parameters CSV file to an R list
2. Simulate Gaussian mixture model data
3. Generate histogram of simulated data
4. Fit Stan model to simulated data
5. Generate figures comparing posterior distributions of fitted parameters to input parameters
6. Generate a PDF that presents results in figures and tables

That’s not a lot of steps for a real-world project, but it’s enough to be really tedious when you’re actively developing a project. And that’s why I think of Make not just as a tool for reproducibility, but as something that greases the wheels in my everyday work.

One non-Make solution to this is just to keep everything within R and to `source` all of your files into one master R script that runs everything. This is all well and good for small projects, but what you lose is Make’s ability to track what has changed and to only update those things that depend on the changed files. When we start working with MCMC models that may take more than a second to run, this becomes really tedious, particularly if all you’re trying to do is to update a figure that relies on some piece of model output. Using a makefile, you can tweak your plotting code (like `bar_chart.R`, above) and just re-run that without running `foo.R`, which may be computationally intensive, again.

The other advantage of Make (in combination with [executable R scripts and command-line parameters](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/script-is-a-program/))is that they push you away from writing monolithic R scripts that do everything all in one place. This makes it easier to make small tweaks and to test individual chunks of an analysis independently, rather than consigning yourself to the horrifying spaghetti code such monoliths are destined to be.

## Keeping things organized
Getting the most out of Make requires a bit of forethought about how our data and source files will be organized. I always assume that all code will be run from the root of the project directory, so pathnames are relative to this root. So if my directory is called `proj_dir`, and I’m within this directory at the Mac/*nix command line, the path to my data will be something like `data/input_data.csv`, which is the path I’ll provide to whatever script uses this data.

I’ve also adapted Christopher Gandrud’s directory structure, keeping my data files in a `data` subdirectory within my project directory and code files within a `src` subdirectory. One thing I’m careful to do is to keep everything generated by my R code in an `output` directory that may have subdirectories within it (`transformed_data`, `figures`, `manuscript`, etc). This way, I can delete everything in the output directory (by typing `make clean`) and re-generate.

I can’t stress this enough: **you should never write output into your `data` and `src` directories!** This totally undermines the goal of reproducibility, because it makes it very difficult to share your code with someone else and have them re-run it. Maintaining a clear [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) will pay large dividends long-term. You should also `make clean` and re-generate early and often to make sure that things are still working. This is a critical aspect of coding for reproducibility: don’t assume it will work, or avoid checking it out in fear that it won’t! Of course, you’ll want to back up your working version first (using Git or whatever approach works best for you).

## Getting more out of Make
The basic `foo : bar` recipe template will take you pretty far. But Make has a wide array of features that can also be helpful. What I’d like to do now is to highlight the ones that are useful specifically for working with command-line arguments in a way that follows the don’t-repeat-yourself ([DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)) maxim.

For example, here’s the step in the Makefile for the Gaussian mixture example where we sample from the mixture distribution using the parameters in the R object file `parameters.Rds`:

        output/samples.csv : src/simdata.R output/parameters.Rds
          @echo --- Simulating data ---
          @mkdir -p $(@D)
          ./$< -o $@ -p $(word 2, $^)

In this snippet `$(@D)`, `$<`, `$@`, and `$^` are what Make refers to as *[automatic variables](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html)*:

- `$(@D)`: Is the directory part of the filename of the target, in this case just output. The command `@mkdir -p $(@D)` expands in this instance to `mkdir -p output`, which makes the directory the target is supposed to go to in case it doesn’t exist yet (The `-p` flag just says to create parent directories as well, e.g. if the output directory was `foo/bar/output`, `foo` and `foo/bar` would be created before `output`).

- `$<` is the first prerequsite, typically the executable file we want to run, in this case `src/simdata.R`.

- `$^` refers to all of the prerequsites, returned as a string. The command `$(word 2, $^)` extracts the second prerequisite, in this case `output/parameters.Rds`, which is the path to the input parameter file for the simulation.

Also, placing `@` before a line just ensures that the command itself is not echoed in the terminal. For example, since the command `echo` is used to print text to the terminal, it’s not necessary to print the command itself when running the Makefile.

This really is only the tip of the iceberg as far as Make goes, and there are examples of some slightly more involved techniques, like wildcards, in the project Makefile. But what we’ve talked about here is more than enough to get going with!