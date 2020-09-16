---
title: "The Backstory: Rising Cases of Measles Despite High Vaccination Coverage"
subtitle: originally published online on September 16, 2020 at https://knowyourvax.com/
summary: 
authors:
- Nina-Masters
tags: [coronavirus, measles, vaccination, herd immunity, measles-containing-vaccine]
categories: ["post"]
date: "2020-09-16T00:00:00Z"
lastMod: "2020-09-16T00:00:00Z"
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: "A spliced-together image of the measles virus and coronavirus. Images from the CDC Image Library"
  focal_point: "center"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
Even though US measles **vaccination rates** were on average **higher than 95%**, which is the WHO vaccination coverage target and threshold for **maintaining herd immunity** for measles, there were 1,282 cases of measles in 31 states in 2019.

High coverage with **measles-containing-vaccine (MCV)** is necessary because of how contagious measles is – it has a basic reproduction number (R<sub>0</sub>) of 12-18: among the highest known values for any infectious disease.  Because of how infectious measles is, the proportion of the population that needs to be vaccinated or have natural immunity from prior disease to prevent outbreaks, known as the c**ritical vaccination fraction (V<sub>c</sub>)**, is around **94-95%**.

The Vc can be expressed in terms of the Ro and vaccine efficacy (V<sub>E</sub>):
$$V_c=\frac{(1-1/R_0 )/V_E}$$ 

This formula makes a key assumption: that the population is evenly mixed - all individuals contact each other with equal likelihood. However, when non-vaccinated individuals are geographically clustered, the formula **can underestimate the V<sub>c</sub>, meaning that outbreaks remain possible despite vaccination coverage targets being met or exceeded**, as we saw in 2019.  

## Research Goals
1. Present a proof of concept using a simple, easy-to-visualize model that showcases what happens as non-vaccinators become more clustered even with high levels of vaccination coverage that would typically be considered enough to maintain herd immunity. 
2. Illustrate the consequences of aggregating data from small to large spatial scales and show how such aggregation may miss important fine-scale clustering, leading to errors in predicted outbreak size.

Answering these research questions will help to successfully implement control strategies for *both* emergent measles outbreaks and ongoing COVID-19 infections. 

## What did we do?
We created a simplified grid with 256 cells of 1,000 people each. Our model had 4 nested levels which matched what we see in real vaccination data: blocks of 1,000 people (individual cells), tracts of 4,000 people (4 cells), neighborhoods of 16,000 people (16 cells), and quadrants of 64,000 people (64 cells). Here, quadrants could represent a small city or township. We used a spatial model where each block of people can transmit only within their cell and their neighboring cells. 

## Clustering Motifs
Within this environment, we created schematic clustering motifs to represent different types of clustered environments: environments that are clustered at a high level, fine-scale patterning, and a mix of both. We generated these motifs using stratified random sampling at the spatial scales described above. See the supplement/GitHub repository for more details on how these clustering conditions were created. 

We kept the overall number of non-vaccinators in the environment as a fixed value and only toggled the degree of clustering to see how that impacts outbreak probability and size. We measured how clustered these ‘motifs’ were using two metrics commonly used in the literature (**Moran’s I** and the **Isolation Index**). We also aggregated these motifs, averaging out the non-vaccinators at each of the spatial levels to assess the effects of aggregated vaccination surveillance data.

## The Model
We modeled a **Susceptible-Infected-Recovered** compartmental transmission measles model on this grid. This is a common strategy for modeling infectious diseases like measles, where individuals can pass through three states: susceptible (i.e. not yet infected), infectious, and recovered (or vaccinated, in this case). Read more here.

## What did we find?

### <u>The Isolation Index is a better metric than Moran’s I</u> for measuring how clustering of non-vaccinated individuals poses a risk to outbreaks. 

The two indices of clustering we used to measure how ‘clustered’ the initial conditions were had very different abilities to predict outbreak size. Moran’s I was unable to predict outbreak size, but the isolation index showed a strong association with final outbreak size. <u>This suggests that isolation index is better at capturing how clustering affects disease transmission.</u> 

### <u>More clustering</u> of unvaccinated individuals leads to <u>higher outbreak probability and larger outbreak size.</u>

We found that although *without clustering*, overall vaccination coverage of 94% and higher *upholds herd immunity* (i.e. there were no outbreaks), once we introduced our clustering motifs, all vaccination levels tested (up to 99% overall vaccination) allowed breakthrough outbreaks to occur. <u>As clustering increased (measured by the isolation index), outbreaks occurred with both higher outbreak probability and higher overall outbreak size.</u> 

### If we <u>aggregate</u> the fine-scale clustering motifs to larger units (analogous to using county, state, or national-level vaccination coverage), this severely <i><u>underestimates</u></i> the expected outbreak probability and size. 

At 95% overall vaccination, the expected outbreak size was predicted to be 3,886 cases using unaggregated data, 2,122 cases using tract-level aggregation (a 45.4% reduction), 911 cases using neighborhood-level aggregation (a 76.5% reduction), and **0 secondary cases** when aggregated to the quadrant level (a 99.9% reduction). 

The following diagram shows how this aggregation process obscures fine-scale spatial heterogeneity for 3 different motifs. These motifs have 3 different underlying patterns of non-vaccination and outbreak potential converge, but when they are aggregated up to the quadrant level, they are identical. *<u>This shows how working from state-level data can mask different possible patterns of clustering that have different consequences for infectious disease transmission – and without access to that finer-scale data, it’s impossible to know how best to protect / design interventions within our communities.</u>*

### The more clustered the initial environment – the more <u>biased</u> the aggregated estimate will be.

We found that aggregating vaccination data consistently underestimated outbreak potential, but that the bias (i.e., how much that outbreak potential was underestimated) increased based on how clustered the original motif was.  
 

## What does this mean for how we conduct surveillance and use vaccination data?
Our results show that failing to account for fine-scale spatial clustering in susceptibility (i.e. the distribution of non-vaccinators) can result in overly optimistic estimates of outbreak potential. **This calls out how potentially dangerous the assumptions of homogeneous mixing which underlie herd immunity calculations can be.** We found that even at 99% overall vaccination coverage, clustering allowed outbreaks to occur – this means that we really must rethink whether or not herd immunity is meaningful when applied at large spatial scales like at the state or country levels. 

Additionally, aggregating data strongly biases predicted outbreak size and potential because it *obscures this fine-scale clustering*. This has immediate implications for vaccine-coverage surveillance in the US, highlighting that finer-scale data are needed to fully understand community susceptibility to outbreaks of measles and other infectious, vaccine-preventable diseases. It’s important to note here that vaccination data is collected at the school-level for entry requirements, but publicly released data instead are typically aggregated at much higher levels – usually at the county or state level. This represents a significant lost opportunity for improving surveillance.  

## Strengths and Limitations
As with all studies, our research has both strengths and limitations. A major strength is that this simple, clear proof-of-concept helps to explain how clustering impacts outbreak potential, specifically when measured by high values of the isolation index. While the simplicity is a strength in communicating the value of this research, it also carries limitations; using a deterministic model doesn’t account for randomness present in the real world; our highly schematic environment does not represent what true cities and social networks look like. We also used a model without an incubation period, which wouldn’t change the total number of cases but doesn’t perfectly represent how measles is transmitted.  

## The Takeaways
1. The assumptions of spatially homogeneous vaccination coverage and contact used in calculating herd immunity thresholds result in significant underestimation of the true number of individuals who need to be vaccinated to prevent outbreaks. 
2. Fine-scale clustering, as measured by high isolation, produced scenarios with the greatest outbreak potential. 
3. Since fine-scale vaccination data is not broadly available in the US, it’s difficult to allocate resources, plan vaccination strategies, and respond to imported measles cases in a way that is responsive this type of localized clustering. 
4. This research motivates the collection of finer-scale vaccination data to create ‘susceptibility maps’ that can guide policy-makers and health practitioners to preferentially direct resources to those areas at highest risk of outbreaks.
