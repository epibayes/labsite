---
title: Knotes on Knitr
subtitle: originally published online on June 02, 2016 at https://www.jonzelner.net/
summary: About Knitr
authors:
- admin
tags: []
categories: ["post"]
date: "2015-06-02T00:00:00Z"
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

[Knitr](http://yihui.name/knitr/) is a truly indispensible part of any R-based workflow that is designed to place an emphasis on reproducibility. Before I started using Knitr, too much of my time was spent hand-copying results from R into Excel spreadsheets or LaTeX tables. Aside from being an excrutiating waste of time, this is an inherently error-prone undertaking. And it is one of those critical sources of friction that can make it agonizing to contemplate making changes to an analysis.

For the uninitiated, Knitr is an R package that facilitates the embedding of R code into documents, written either in [RMarkdown](http://rmarkdown.rstudio.com/) or LaTeX which can then be processed into many output formats (Markdown, HTML, PDF) either using the `knitr::knit()` function or indirectly by using the amazing [Pandoc](http://pandoc.org/). Knitr holds out the promise of writing documents that are dynamic and can quickly be re-generated when we changes something in the data processing, analysis, plotting, etc.

But my experiences with Knitr have not all been painless. My early use of Knitr served largely to reproduce only the sins of the past: I found myself loading my RMarkdown files with tons of code that made them as slow to run and hard to debug as the monolithic R scripts I had been used to writing.

This is of course not in any way of a criticism of Knitr, but instead a testament to its power and versatility. For short, automatically-generated reports, putting all of your model code into an RMarkdown file and running it through Knitr may be exactly what you want to do. But for more involved analyses, and especially those with computationally intensive or slow-running components (e.g., MCMC, simulation models), an approach in which each component part has its own R script, and the dependencies between these are coordinated using a [makefile](https://www.jonzelner.net/statistics/make/reproducibility/2016/06/01/makefiles/) may be the best bet. In this workflow, Knitr’s considerable powers are used sparingly, specifically to embed parameter estimates and tables in the text, with most or all analysis and plotting confined to external scripts.

To me, this approach also has two key advantages from a day-to-day working perspective. First, it preserves the ability to develop analyses and visualizations interactively by `source`-ing your code into an R session and looking at the results. Second, it doesn’t assume you will be working on the RMarkdown document that will eventually turn into your finished paper from the get-go. Instead, the written output of your analysis can grow organically as you accumulate meaningful results to put into a document. And if you take them out of the document, they don’t just disappear.

## A Worked Example
These ideas may come across a bit more clearly in an example. All of the code for this example is available [on Github](https://github.com/jzelner/blog-examples/tree/master/2016-06-02-knitr), and the raw RMarkdown that this post is written in is available [here](https://raw.githubusercontent.com/jzelner/blog-examples/master/2016-06-02-knitr/2016-06-02-knitr.Rmd). If you want to reproduce the results and have the relevant R packages installed (`ggplot2`, `readr`, `docopt`), you can type `make post` from within the directory and generate the figures and Markdown underlying this post.

Let’s start with simulating from and plotting the Gaussian mixture model that’s at the heart of the toy example from the previous few posts. Using Knitr, we can load the parameters from their source file `data/parameters.csv`, and manipulate them a bit for presentation:

        require(readr)
        require(dplyr)
        d <- read_csv("data/parameters.csv")
        od <- filter(d, parameter != "n")

        ## Extract the number of samples
        nsamples <- filter(d, parameter == "n")$value[1]

        ## Make a table with the input parameters
        pars_table <- kable(od, digits = 10, caption = "Parameter values", format = "markdown")

We can then print the table using a piece of inline R code “r pars_table” in our Rmd file (surrounded by backticks to make it executable):

| parameter | value |
|-----------|-------|
| m1        | 0.5   |
| m2        | 10.0  |
| sd1       | 1.0   |
| sd2       | 3.0   |
| p         | 0.5   |

(A quick guide to reading the table: `m1` and `m2` refer to the means of the two mixture components, and `sd1` and `sd2` refer to their respective standard deviations. The parameter `p` is the mixing parameter, i.e the proportion of samples drawn from the first component.)

We can then simulate 10000 draws from the model using the file `src/sim_data.R` and plot the results with `src/data_plot.R` and look at the results:

{{< figure library="true" src="gaussian_mixture.png" title="Gaussian Mixture" >}}


We can also load the samples themselves into the R session to calculate and present descriptive statistics:

        samples_df <- read_csv("output/samples.csv")

        ## Calculate and format sample mean
        mean <- sprintf("%0.2f", mean(samples_df$x))

        ## Load parameter list
        pars <- readRDS("output/parameters.Rds")

        ## Calculate and format expectation from input parameters
        expected_mean <- sprintf("%0.2f", pars$m1*pars$p + pars$m2*(1.0-pars$p))
        
We can then see that the sample mean, 5.37, is nearly equivalent to the expected value based on the parameters: 5.25.

## Make + Knitr
As I finish up, I just wanted to talk about the way Knitr and Make come together in this example. You can see the Makefile used to generate this post [here](https://github.com/jzelner/blog-examples/blob/master/2016-06-02-knitr/Makefile). But I wanted to direct your attention to the specific part that turns the input into the [Jekyll](https://jekyllrb.com/)-flavored Markdown underlying this post:

        output/2016-06-02-knitr.md : 2016-06-02-knitr.Rmd data/parameters.* output/figures/d_density.png 
          @echo ----Translating RMD to Markdown ----
          @mkdir -p $(@D)
          Rscript \
            -e "require(knitr)" \
                        -e "knitr::render_jekyll()"\
            -e "knitr::knit('$<','$@')"

Rather than writing a whole R script file to tell Knitr to take the RMarkdown input (the `2016-06-02-knitr.Rmd`) file and turn it into Markdown with embedded results (`output/2016-06-02-knitr.md`), this snippet passes the relevant code to R in a single line using the `Rscript` executable you should remember from the earlier discussion of [hashbangs](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/script-is-a-program/). You can see that I’ve also included the parameters in the `output` folder and histogram figure as prerequisites.

What this piece of code does is to load the knitr package (`require(knitr)`), set the output format (`knitr::render_jekyll()`), and then convert from one file to the other, using the automatic variables `$<` and `$@` to automatically insert the filenames of the first prerequsite and target files (`knitr::knit('$<','$@')`).

For an example of how to use this pattern to generate the PDF for the Gaussian mixture toy example, see this [Makefile](https://gitlab.com/jzelner/reproducible-stan/blob/master/Makefile).

## Conclusion
So, those are my thoughts on Knitr. This clearly only scratches the surface, but hopefully gives a good sense of how Knitr can fit into a productive, reproducible workflow.