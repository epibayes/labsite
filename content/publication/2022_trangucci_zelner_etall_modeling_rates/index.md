---
title: "Modeling rates of disease with missing categorical data"
authors:
- Rob-Trangucci
- "Yang Chen"
- admin
date: "2022-06-16T00:00:00Z"
doi: "https://doi.org/10.1371/journal.pcbi.1009795"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-09-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "arXiv"
publication_short: "arXiv"

abstract: "Covariates like age, sex, and race/ethnicity provide invaluable insight to public health authorities trying to interpret surveillance data collected during a public health emergency such as the COVID-19 pandemic. However, the utility of such data is limited when many cases are missing key covariates. This problem is most concerning when this missingness likely depends on the values of missing covariates, i.e. they are not missing at random (NMAR). We propose a Bayesian parametric model that leverages joint information on spatial variation in the disease and covariate missingness processes and can accommodate both MAR and NMAR missingness. We show that the model is locally identifiable when the spatial distribution of the population covariates is known and observed cases can be associated with a spatial unit of observation. We also use a simulation study to investigate the model's finite-sample performance. We compare our model's performance on NMAR data against complete-case analysis and multiple imputation (MI), both of which are commonly used by public health researchers when confronted with missing categorical covariates. Finally, we model spatial variation in cumulative COVID-19 incidence in Wayne County, Michigan using data from the Michigan Department and Health and Human Services. The analysis suggests that population relative risk estimates by race during the early part of the COVID-19 pandemic in Michigan were understated for non-white residents compared to white residents when cases missing race were dropped or had these values imputed using MI."

# Summary. An optional shortened abstract.
# summary: 

tags:
- Public Health
- Surveillance
- COVID-19
- Bayesian Model
- Spatial Variation
- Multiple Imputation
- Covariates

featured: false

links:
- name: Online Access
  url: "https://doi.org/10.48550/arXiv.2206.08161"
# url_pdf: 
# url_code: '#'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
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
slides: ""
---