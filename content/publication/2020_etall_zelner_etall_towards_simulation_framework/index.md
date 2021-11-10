---
title: "Towards a simulation framework for optimizing infectious disease surveillance: An information theoretic approach for surveillance system design"
authors:
- "Qu Cheng" 
- "Philip A Collender" 
- "Alexandra K Heaney" 
- "Xintong Li" 
- "Rohini Dasan" 
- "Charles Li" 
- "Joseph Lewnard" 
- admin
- "Song Liang" 
- "Howard H Chang" 
- "Lance A Waller" 
- "Benjamin A Lopman" 
- "Changhong Yang" 
- "Justin V Remais"


date: "2020-01-01T00:00:00Z"
doi: "https://doi.org/10.1101/2020.04.06.20048231"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-09-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: MedRxiv
publication_short: medRxiv

abstract: "Infectious disease surveillance systems provide vital data for guiding disease prevention and control policies, yet the formalization of methods to optimize surveillance networks has largely been overlooked. Decisions surrounding surveillance design parameters—such as the number and placement of surveillance sites, target populations, and case definitions—are often determined by expert opinion or deference to operational considerations, without formal analysis of the influence of design parameters on surveillance objectives. Here we propose a simulation framework to guide evidence-based surveillance network design to better achieve specific surveillance goals with limited resources. We define evidence-based surveillance design as a constrained, multi-dimensional, multi-objective, dynamic optimization problem, acknowledging the many operational constraints under which surveillance systems operate, the many dimensions of surveillance system design, the multiple and competing goals of surveillance, and the complex and dynamic nature of disease systems. We describe an analytical framework for the identification of optimal designs through mathematical representations of disease and surveillance processes, definition of objective functions, and the approach to numerical optimization. We then apply the framework to the problem of selecting candidate sites to expand an existing surveillance network under alternative objectives of: (1) improving spatial prediction of disease prevalence at unmonitored sites; or (2) estimating the observed effect of a risk factor on disease. Results of this demonstration illustrate how optimal designs are sensitive to both surveillance goals and the underlying spatial pattern of the target disease. The findings affirm the value of designing surveillance systems through quantitative and adaptive analysis of network characteristics and performance. The framework can be applied to the design of surveillance systems tailored to setting-specific disease transmission dynamics and surveillance needs, and can yield improved understanding of tradeoffs between network architectures."

# Summary. An optional shortened abstract.
summary: Disease surveillance systems are essential for understanding the epidemiology of infectious diseases and improving population health. A well-designed surveillance system can achieve a high level of fidelity in estimates of interest (e.g., disease trends, risk factors) within its operational constraints. Currently, design parameters that define surveillance systems (e.g., number and placement of the surveillance sites, target populations, case definitions) are selected largely by expert opinion and practical considerations. Such an informal approach is less tenable when multiple aspects of surveillance design—or multiple surveillance objectives— need to be considered simultaneously, and are subject to resource or logistical constraints. Here we propose a framework to optimize surveillance system design given a set of defined surveillance objectives and a dynamical model of the disease system under study. The framework provides a platform to conduct in silico surveillance system design, and allows the formulation of surveillance guidelines based on quantitative evidence, tailored to local realities and priorities. The approach facilitates greater collaboration between health planners and computational and data scientists to advance surveillance science and strengthen the architecture of surveillance networks.

tags:
- Infectious Disease
- Disease Surveillance
- Simulation

featured: false

links:
- name: Online Access
  url: https://www.medrxiv.org/content/10.1101/2020.04.06.20048231v1
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