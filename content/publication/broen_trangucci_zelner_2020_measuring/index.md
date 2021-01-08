---
title: "Measuring the impact of spatial perturbations on the relationship between data privacy and validity of descriptive statistics"
authors:
- Kelly-Broen
- Rob-Trangucci
- admin
date: "2021-01-07T00:00:00Z"
doi: "https://doi.org/10.1186/s12942-020-00256-8"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-01-08T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: International Journal of Health Geographics
publication_short: Int J Health Geogr

abstract: "Background



Like many scientific fields, epidemiology is addressing issues of research reproducibility. Spatial epidemiology, which often uses the inherently identifiable variable of participant address, must balance reproducibility with participant privacy. In this study, we assess the impact of several different data perturbation methods on key spatial statistics and patient privacy.





Methods


We analyzed the impact of perturbation on spatial patterns in the full set of address-level mortality data from Lawrence, MA during the period from 1911 to 1913. The original death locations were perturbed using seven different published approaches to stochastic and deterministic spatial data anonymization. Key spatial descriptive statistics were calculated for each perturbation, including changes in spatial pattern center, Global Moran’s I, Local Moran’s I, distance to the k-th nearest neighbors, and the L-function (a normalized form of Ripley’s K). A spatially adapted form of k-anonymity was used to measure the privacy protection conferred by each method, and its compliance with HIPAA and GDPR privacy standards.





Results


Random perturbation at 50 m, donut masking between 5 and 50 m, and Voronoi masking maintain the validity of descriptive spatial statistics better than other perturbations. Grid center masking with both 100 × 100 and 250 × 250 m cells led to large changes in descriptive spatial statistics. None of the perturbation methods adhered to the HIPAA standard that all points have a k-anonymity > 10. All other perturbation methods employed had at least 265 points, or over 6%, not adhering to the HIPAA standard.





Conclusions


Using the set of published perturbation methods applied in this analysis, HIPAA and GDPR compliant de-identification was not compatible with maintaining key spatial patterns as measured by our chosen summary statistics. Further research should investigate alternate methods to balancing tradeoffs between spatial data privacy and preservation of key patterns in public health data that are of scientific and medical importance."

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Geomasking
- Privacy
- Spatial Anonymity
- Reproducibility

featured: true

links:
- name: Online Access
  url: https://link.springer.com/article/10.1186/s12942-020-00256-8
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