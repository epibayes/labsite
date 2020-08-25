---
title: "A robust method for automated background subtraction of tissue fluorescence"
authors:
- Alex-Cao
date: "2007-05-14T00:00:00Z"
doi: "https://doi.org/10.1002/jrs.1753"

# Schedule page publish date (NOT publication's date).
publishDate: "2020-08-18T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: Journal of Raman Spectroscopy
publication_short: J Raman Spectrosc

abstract: "This paper introduces a new robust method for the removal of background tissue fluorescence from Raman spectra. Raman spectra consist of noise, fluorescence and Raman scattering. In order to extract the Raman scattering, both noise and background fluorescence must be removed, ideally without human intervention and preserving the original data. We describe the rationale behind our robust background subtraction method, determine the parameters of the method and validate it using a Raman phantom against other methods currently used. We also statistically compare the methods using the residual mean square (RMS) with a fluorescence-to-signal (F/S) ratio ranging from 0.1 to 1000. The method, ‘adaptive minmax’, chooses the subtraction method based on the F/S ratio. It uses multiple fits of different orders to maximize each polynomial fit. The results show that the adaptive minmax method was significantly better than any single polynomial fit across all F/S ratios. This method can be implemented as part of a modular automated real-time diagnostic in vivo Raman system."

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Raman spectroscopy
- Raman spectra
- Background subtraction
- Fluorescence
- Polynomial fit
- Adaptive
- Minmax

featured: false

links:
- name: Online Access
  url: https://onlinelibrary.wiley.com/doi/abs/10.1002/jrs.1753
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