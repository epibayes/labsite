---
title: "Likelihood and model fit: A visual tour"
authors:
- admin
date: "2021"
# doi: "https://doi.org/10.1186/s12942-020-00256-8"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-03-11T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
# publication_types: ["2"]

# Publication name and optional abbreviated publication name.
# publication: International Journal of Health Geographics
# publication_short: Int J Health Geogr

abstract: "Likelihood is a concept that underlies most statistical modeling that falls under the heading of [generalized linear model](https://en.wikipedia.org/wiki/Generalized_linear_model) or GLMs. 


When we fit any kind of statistical model to a dataset, the goal is to find solutions that either maximize the likelihood of the data, given the model (under a frequentist, maximum likelihood estimation framework), or maximize the likelihood of the data given the data and some prior information on the value of the parameters (under a more Bayesian framework).In this tutorial, we will introduce some key concepts and tools for smoothing and visualizing potentially non-linear data. We will focus on local regression techniques for continuous outcomes, e.g. BMI, blood pressure, etc, in in one dimension, e.g. in response to some exposure, and in two dimensions representing x and y spatial coordinates. In a future tutorial we will look at complementary approaches to spatial density estimation which let us estimate the probability of an event occurring in space that build on the concepts discussed in this tutorial."

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Tutorial
- Likelihood
- Non-linear data

featured: false

links:
- name: Online Tutorial
  url: https://sph-umich.shinyapps.io/modelfit/
# url_pdf: 
# url_code: '#'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: 'zelner_cscs_seminar.pdf'
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# image:
#   caption: ''
#   focal_point: ""
#   preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects: 

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: "content/slides/zelner_2020_cscs_seminar/zelner_cscs_seminar"
---