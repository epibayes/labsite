---
title: It's not reproducible if it only runs on your laptop.
subtitle: originally published online on June 03, 2016 at https://www.jonzelner.net/
summary: Make sure it runs.
authors:
- admin
tags: []
categories: ["post"]
date: "2016-06-03T00:00:00Z"
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
**Note: This post is part of a series on reproducibility. With any luck, it will make sense on its own. But it may be helpful to start from [the beginning](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/reproducibility-pt-1/).**

So, you’ve made your R scripts [executable](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/script-is-a-program/), created a dynamic document to present your results with [Knitr](https://www.jonzelner.net/knitr/r/reproducibility/2016/06/02/knitr/), converted to PDF with Pandoc and coordinated the whole process of running models, generating figures and producing a final PDF with a [Makefile](https://www.jonzelner.net/statistics/make/reproducibility/2016/06/01/makefiles/).

Now it’s time to clear another hurdle: sharing your code with someone else in a way where they can actually run it and inspect the results. But you may have noticed something about the list above: there are a lot of standalone programs (like Pandoc) and R packages (`knitr`,`rstan`,`ggplot2`, etc), known as *dependencies*, that the next person will have to download and install in order to have a chance of successfully running your code.

There are solutions out to take a snapshot of and share your R environment, like [Packrat](https://rstudio.github.io/packrat/), which is great, particularly for maintaining an isolated and well-documented workspace for individual projects.

But it only solves the problem of sharing the R packages you use locally, and doesn’t serve the goal of total reproducibility, of providing something to an interested colleague/reviewer/adversary that will reproduce every step of your analysis down to the PDF of the completed manuscript by just running a single command.

Finally, taking a Packrat-only approach tethers you to R, when you might decide you want to write some of your data-munging code in Python, use a Perl script to [count the words in your LaTeX document](http://app.uio.no/ifi/texcount/), run an agent-based model written in Java or a numerical simulation in Julia.

## Making a Portable Environment Using Docker
Enter [Docker](https://www.docker.com/). Docker is a relatively new tool for building portable computing environments known as *containers*. Docker containers provide an isolated environment that acts like a separate computer. The contents of a container are specified using a [Dockerfile](https://docs.docker.com/engine/reference/builder/) that contains a list of commands necessary to download and install all of the software necessary to run a given application. This way, we can have R, Pandoc, LaTeX and all of the R packages we need installed in an environment that is designed to be shared.

Thankfully, Dirk Eddelbuettel, Carl Boettiger and others saw the need for this awhile ago, and put together a set of Docker images that include all of these tools under what they call the [rocker](https://github.com/rocker-org/rocker) project. One of their Dockerfiles, for the `hadleyverse` container, contains a whole host of nearly-essential R packages, including the Hadley Wickham classics: `ggplot2`, `dplyr`, `readr`, `purrr`, and more.

One of the great things about Docker is the idea of *layers*, which let us build on top of existing containers. For the [toy example using Stan](https://gitlab.com/jzelner/reproducible-stan), I needed a working Stan install, so I built a new Docker image (borrowing liberally from [this example](https://github.com/jrnold/docker-stan)) on top of the `rocker/hadleyverse` image that has Stan installed as well as some tools that I find useful for grabbing data from other online sources (e.g. [cURL](https://en.wikipedia.org/wiki/CURL)) as well as tools for making slightly prettier LaTeX output (like [XeTeX](https://en.wikipedia.org/wiki/XeTeX) and a bunch of fonts). You can check out the Dockerfile for building a basic working RStan install [here](https://github.com/jzelner/docker-rstan/blob/master/rstan/Dockerfile) and one that includes some additional tools for mapping with R [here](https://github.com/jzelner/docker-rstan/blob/master/rstan-geo/Dockerfile).

## Running the Gaussian mixture example locally with Docker
First, you’re going to need a working Docker install. If you’re on Mac or Windows, I heartily recommend signing up for the [Docker for Mac/Windows beta](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/) which will help you have a seamless Docker experience. If you happen to be working in a Linux environment, just go ahead and do the regular Docker install. The bad news is if you’re on a Mac or Windows and haven’t been accepted into the beta yet, getting going with this may be a bit fiddly. But don’t stop reading here: **this will still be useful in the next installment when we talk about using Docker to run analyses on remote servers for free and with zero configuration!**

Provided you do have a working local Docker install, you can grab the rstan image from [DockerHub](http://hub.docker.com/) just by typing `docker pull jonzelner/rstan` at the command line.

To run the whole analysis and reproduce the [final PDF](https://dl.dropboxusercontent.com/s/e99l7q4c3toderd/mixture_model_output.pdf), you first have to either clone the project git repository by typing: `git clone https://gitlab.com/jzelner/reproducible-stan.git`, or if you don’t have [git](https://en.wikipedia.org/wiki/Git_(software)) installed or just aren’t comfortable with it, you can download the whole project as a [zipfile](https://gitlab.com/jzelner/reproducible-stan/repository/archive.zip?ref=master).

Once you have downloaded the project, enter the directory by typing `cd reproducible-stan`. You can then run the whole thing by executing the shell script `dockerbuild.sh` by typing `./dockerbuild.sh`. (If you don’t have Docker installed, but have all of the relevant dependencies installed locally, you can build everything by typing `make pdf` or `./build.sh` at the command line.)

Let’s take a look inside `dockerbuild.sh` and see what it’s doing:

[#!/usr/bin/env bash]

        #!/usr/bin/env bash

        ## This just makes sure everything is re-run even if parameters file
        ## hasn't been updated
        touch data/parameters.csv

        ## Run in a detached Docker instance
        JOB=$(docker run -v `pwd`:/example -u rstudio -d jonzelner/rstan /bin/bash -c "cd example && make pdf")

        ## Write job ID out to a file in case we want to keep track of a long-running job
        echo $JOB > dockerjob

        ## Follow the logged output from the Docker instance
        docker logs -f $JOB

Pay specific attention to the line starting with `docker run`, because that’s the part that’s doing all the work for us. The command is enclosed in `$()` just to store its output in the variable `JOB` (in this case the ID of the image running the analysis) in case we want to inspect it while it’s running. The `-v` flag tells Docker to mount the current directory (`pwd` is a command that returns the absolute path to the current working directory) to the directory `/example` on the Docker container `jonzelner/rstan`. The flag `-d` says to run it in detached mode, which just means we won’t be interacting directly with the command line on the running container. Finally is the command we run on the Docker container once it starts running `/bin/bash -c "cd example && make pdf"`. This tells the Docker container to start the bash shell when it opens, enter the `example` directory we have mounted into the container, and then run the `make pdf` command just like we would locally.

The `line docker logs -f $JOB` will write all of the output from the running container to the terminal. When it’s finished running, the container will exit and you will be able to find the model output in the `output` directory within the `reproducible-stan` folder.

## Conclusion
This one is admittedly a heavier lift than some of the earlier items, like making reproducible scripts and using command-line arguments. It involves interacting with what can be a fairly intimidating and relatively new technology. But even if this last bit was a bit confusing and overwhelming, do not fret! Making good use of Docker really doesn’t require you to write Dockerfiles and build working environments from scratch if that’s not your thing. That’s what the good [rocker](https://github.com/rocker-org/rocker) folks and others like me are doing so you don’t have to do it.

But understanding what Docker is all about can still pay some serious dividends. First of all, if there’s another Docker image out there that fits the bill for your project (`rocker/hadleyverse` will take you pretty far for most purposes!), you can just modify `dockerbuild.sh` to suit your purposes (i.e. by changing the name of the docker image from `jonzelner/rstan` to something else).

But Docker is also part of a large and growing ecosystem that makes it much easier to run and share your analyses on cloud-based infrastructure. So stay tuned for the next installment, when we’ll talk about how to run and share your models and their results *for free* using Gitlab’s very-excellent [continuous integration](https://about.gitlab.com/gitlab-ci/) tools…