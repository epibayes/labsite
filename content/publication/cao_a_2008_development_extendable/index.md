---
title: "Development of an extendable arm and software architecture for autonomous and tele-operated control for mobile platforms"
authors:
- Alex-Cao
date: "2008-04-16T00:00:00Z"
doi: "https://doi.org/10.1117/12.778059"

# Schedule page publish date (NOT publication's date).
publishDate: "2020-08-18T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: SPIE
publication_short: SPIE

abstract: "There is a strong demand for efficient explosive detecting devices and deployment methods in the field. In this study we present a prototype mast that uses a telescoping pulley system for optimal performance on top of an unmanned ground vehicle to be able to be controlled wirelessly. The mast and payload reaches up eight feet from the platform with a gripper that can pick up objects. The current mobile platform operators using a remote-control devices to move the arm and the robot itself from a safe distance away. It is equipped with a pulley system that can also be used to extend a camera or explosive detection sensor under a vehicle. The mast is outfitted with sensors. The simple master-slave strategy will not be sufficient as the navigation and sensory inputs will become complex. In this paper we provide a tested software/hardware framework that allows a mobile platform and the expanded arm to offload operator tasks to autonomous behaviors while maintaining tele-operations. This will implement semi-autonomous behaviors. This architecture involves a server which communicates commands and receives sensor inputs via a wireless modem to the mobile platform. This server can take requests from multiple client processes which have prioritized access to on-board sensor readings and can command the steering. The clients would include the tele-operation soldier unit, and any number of other autonomous behaviors linked to particular sensor information or triggered by the operator. For instance, the behavior of certain tasks can be controlled by low-latency clients with sensory information to prevent collisions, place sensor pods precisely, return to preplanned positions, home the units location or even perform image enhancements or object recognition on streamed video."

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Mast
- Teleoperation
- Omnidirectional drive
- Wireless communications
- Mobile robots


featured: false

links:
- name: Online Access
  url: https://www.spiedigitallibrary.org/conference-proceedings-of-spie/6962/69621U/Development-of-an-extendable-arm-and-software-architecture-for-autonomous/10.1117/12.778059.short
# url_pdf: '#'
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