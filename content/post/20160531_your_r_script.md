---
title: Your R script is a program!
subtitle: originally published online on May 31, 2016 at https://www.jonzelner.net/
summary: R scripts are programs!
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
**Note: This post is part of a series on reproducibility. With any luck, it will make sense on its own. But it may be helpful to start from [the beginning](https://www.jonzelner.net/statistics/make/docker/reproducibility/2016/05/31/reproducibility-pt-1/).**

I really can’t stress this point enough: your R script is a program, and you should treat it as such!

Programs for statistical analysis are typically written in an iterative, interactive way, by running code in a REPL like the command-line version of R, Rstudio, Stata, etc. But there’s a tendency to think of this as being some other kind of activity that is not programming. But the last time I checked, this is basically exactly how developers of interpreted languages like Python and Ruby work and is not really all that different from the way programs in compiled languages (like C and C++) are developed. So whether you like it or not, writing R (or Stata, or SAS) code is programming. It’s just a question of how good and careful of a programmer you want to try to be.

So, what I want to talk about in this quick tutorial is how to start treating your R scripts like the real command-line programs they should be. And to do this, we’re going to need to use two simple but powerful tools: hashbangs and command-line arguments.

## Hashbangs
**Quick warning: this section is unabashedly Mac and *Nix-centric. If you are using Windows, the general ideas apply, but the specific steps will not.**

On Unix-like systems, a *hashbang* or *shebang* is a piece of text at the beginning of a script that tells the computer what program to use to run it if it is run as an executable. As the name implies, it’s a hash symbol and exclamation point `#!` followed by the path to the program.

For R, there are a few ways to [skin this particular cat](http://dirk.eddelbuettel.com/code/littler.html), but I’m going to talk about the one I use most and that is availble with a working R install without any additional dependencies.

Consider the following extremely boring R program:

        #!/usr/bin/env Rscript

        x <- rnorm(100)
        df <- data.frame(x = x)
        write.csv(df, "sim_data.csv")

If you `source` this into your R environment, you’ll find that it takes 100 samples from a standard Normal distribution and saves them out to the file `sim_data.csv`. Good stuff. But what if we want to run this piece of code directly from the command line? First, we have to make it executable. If it’s saved in the file `sim_normal.R`, we navigate to the directory the file is stored in and type `chmod +x sim_normal.R`. This tells the system that the file is executable, and if you run `./sim_normal.R`, the shell will read the file, and send its contents to the program specified in the hasbang `#!/usr/bin/env Rscript` above.

## Command-line options
One big problem with `sim_normal.R` is that it contains what one of my grad school mentors referred to as *magic numbers*. Magic numbers are, of course, the root of all evil. There is no reason we will always want to take only 100 samples, and for that matter, we may also want to sample from a distribution with something other than mean zero and standard deviation 1.

This is where we really make the transition to writing an actual program, where instead of having a piece of code that has a single use (simulating 100 samples from a normal distribution with mean zero and SD 1), we can have a wider range of options by providing new options.

To do this, we’ll use the incredibly useful [docopt](http://docopt.org/) which makes it easy to both specify command-line arguments and implement them in the same piece of code. Docopt is a cross-platform approach to specifying command-line arguments that has been merficully [implemented for R](https://github.com/docopt/docopt.R). This makes it much easier to include arguments than the somewhat rudimentary support included in base R. This is particularly true because docopt provides the ability to easily set default values, so that when we’re testing by `source`-ing code into R, we can just use the default values.

So here’s our exciting program, but with command-line arguments:

        #!/usr/bin/env Rscript
        require(docopt)
        'Usage:
          sim_normal.R [-m <mean> -s <sd> -n <nsamples> -o <output>]

        Options:
          -m Mean of distribution to sample from [default: 0]
          -s SD of distribution to sample from [default: 1]
          -n Number of samples [default: 100]
          -o Output file [default: sim_data.csv]

        ]' -> doc

        opts <- docopt(doc)

        x <- rnorm(opts$n, mean = as.numeric(opts$m), sd = as.numeric(opts$s))
        df <- data.frame(x = x)
        write.csv(df, opts$o)

First, we store the command line options in a string represented by the variable `doc` and then let docopt parse them with `docopt(doc)`, which returns a list in which the command line arguments are accessible in the usual way.

Now, we can sample 10000 samples from a distribution with mean 10 and SD 3 and save the results to `sim_lots_of_data.csv` with the following `command ./sim_normal.R -m 10 -s 3 -n 10000 -o sim_lots_of_data.csv`.

This is a kind of simplistic example, but having the ability to execute directly from the command line and pass arguments will become more important in the next step of our quest for reproducibility, when we tackle [Makefiles](https://www.jonzelner.net/statistics/make/reproducibility/2016/06/01/makefiles/)!