---
title: Using simulation to understand frequentist confidence intervals and Bayesian credible intervals as tools for inference
linktitle: Using simulation to understand frequentist confidence intervals and Bayesian credible intervals as tools for inference
toc: true
type: docs
date: "2020"
draft: false
authors:
- admin
menu:
  example:
    parent: Learning
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
# publication_types: ["2"]

# Publication name and optional abbreviated publication name.
# publication: International Journal of Health Geographics
# publication_short: Int J Health Geogr


# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Tutorial
- Bayesian
- Normal distribution
- Confidence Interval

links:
- name: Online Tutorial
  url: https://jzelner.shinyapps.io/simulation_inference
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
In this example, we’re going to go back to basics, and use both a formula and simulation to calculate confidence intervals for a sample mean. So, first, pick a mean and standard deviation and number of samples to draw from a Normal distribution.