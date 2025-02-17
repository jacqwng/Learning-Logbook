---
title: "Tree phenology Analysis with R"
author: "Jacqueline Wingen"
date: "16 Februar 2025"
site: bookdown::bookdown_site
---

# Introduction

Hi, my name is Jacqueline. I’m a master’s student in Crop Sciences at the [University of Bonn](https://www.uni-bonn.de/de). This is my learning logbook for the module “Tree phenology analysis with R”. This module provides an overview of methods to study the impact of climate and climate change on tree phenology. It is designed for those who may not yet be familiar with phenology or how to analyze climate change effects, but it also aims to offer new insights for those with existing knowledge in these areas. Initially developed for M.Sc. students in Crop Science and Agricultural Science and Resource Management in the Tropics and Subtropics (ARTS) at the University of Bonn, the material is accessible to anyone interested.

The content begins with an introduction to phenology (with a special emphasis on dormancy) as well as an overview of climate change. It then focuses heavily on the practical application of the `chillR` package for R. This tool has been continuously developed since 2013 by [Prof. Dr. Eike Lüdeling](https://www.gartenbauwissenschaft.uni-bonn.de/author/prof.-dr.-eike-luedeling/), head of the HortiBonn research group at the [Institute of Crop Science and Resource Conservation (INRES)](https://www.inres.uni-bonn.de/de) at the University of Bonn, to support this type of analysis.

## Learning goals

This course will offer the following skills and experiences:

-   Knowledge about phenology

-   Knowledge about tree dormancy

-   Understanding of climate change impact projection methods

-   Appreciation for the importance of risks and uncertainty in climate change projection

-   Understanding of how to use some staple tools of R code development

-   Ability to use `chillR` functions for climate change impact projection

-   Ability to use `chillR` functions for tree phenology analysis

-   Understanding and ability to use the PhenoFlex dormancy analysis framework

<!--chapter:end:index.Rmd-->

# Tools

This course is designed to provide knowledge about tree phenology, climate change, and related topics, along with hands-on exercises to demonstrate the functionalities of the `chillR` package. It is recommended to document everything learned in a `learning logbook`. To engage in these practical components effectively, various tools are required. Since `chillR` is an [R](https://www.r-project.org/) package, using R, preferably through the [RStudio](https://posit.co/download/rstudio-desktop/) interface, will be necessary.

Although it is possible to run RStudio on a local computer and save files directly on the hard drive, this approach differs from the methods commonly used by professional programmers. To align with standard programming practices, familiarity with certain code development tools is essential. This course will therefore cover the basics of using [Git](https://git-scm.com/) and [GitHub](https://github.com/), which are valuable tools for organizing, securing, and sharing code. Additionally, proper documentation techniques in R will be introduced, focusing on creating well-structured, professional reports using [RMarkdown](https://rmarkdown.rstudio.com/). While these tools may seem complex at first, their usefulness is likely to become clearer as they are used throughout the module.

[Dr. Cory Whitney](https://inresgb-lehre.iaas.uni-bonn.de/author/dr.-cory-whitney/), a researcher at HortiBonn, has volunteered to create tutorial videos to provide an introduction to these tools.

## R and RStudio

The first video *Using R and RStudio* demonstrates how to install and run [R](https://www.r-project.org/) and [RStudio](https://posit.co/download/rstudio-desktop/):

<iframe src="https://www.youtube.com/embed/WT3tKlzCZgo" width="672" height="400px" data-external="1"></iframe>

## Git and Github

The next video Using *Git and Github* explores the programming version control environment [Git](https://git-scm.com/) and the interface [GitHub](https://github.com/), which is used to access these features:

<iframe src="https://www.youtube.com/embed/S98XJTyIVaY" width="672" height="400px" data-external="1"></iframe>

## Rmarkdown

In the last video *Using R Mardown*, [R Markdown](https://rmarkdown.rstudio.com/) will be examined, a powerful tool that enables the creation of sophisticated reports, websites, and more from R code:

<iframe src="https://www.youtube.com/embed/hh4wyP8tvkI" width="672" height="400px" data-external="1"></iframe>


<!--chapter:end:02-tools.Rmd-->

# Tree dormancy

This chapter is presented by [Dr. Erica Fadón](https://scholar.google.de/citations?hl=de&user=MTmTnnsAAAAJ), a researcher at [HortiBonn from 2018 to 2021](https://inresgb-lehre.iaas.uni-bonn.de/author/dr.-erica-fadon-adrian/), who explores dormancy in temperate fruit trees. This topic remains complex and has many unanswered questions. A central question for researchers is, “How do trees know when to flower?” Although it seems clear that trees bloom in spring, the reality is more complicated. This chapter provides a better understanding of dormancy and demonstrates how to use the `chillR` tool to predict flowering times, even in the face of challenges posed by global warming.

## Learning goals

-   Learn about dormancy in temperate fruit trees
-   Be able to identify the phenological stages of a fruit tree and understand phenology data sets
-   Describe and compare the two methodologies (empirical and statistical) to identify the chilling and forcing periods of a certain cultivar

## Introduction to dormancy

Tree dormancy is a state of reduced activity that occurs when environmental conditions are unfavorable, especially during winter. This state acts as a survival strategy, helping trees withstand extreme temperatures, water shortages, and other stress factors. During dormancy, trees slow down or stop their growth to conserve energy and avoid damage. Dormancy is a continuous process divided into three phases:

-   **Dormancy Establishment**
-   **Endo-Dormancy**
-   **Eco-Dormancy**

Dormancy establishment is the process where temperate trees transition from active growth in summer to a dormant state in autumn. This shift is mainly triggered by shorter daylight hours and decreasing temperatures, causing buds to form, growth to stop, and leaves to fall. The importance of these factors varies by species, with some trees responding more to day length and others to temperature.

Endo-dormancy is a phase of dormancy controlled by the plant's internal factors, where growth is suppressed even under favorable conditions. It requires a period of cold exposure (chilling) to release the buds from this state, preventing premature growth during temporary warm spells in winter. Low temperatures are the main trigger for breaking endo-dormancy, while the role of light (photoperiod) is still uncertain.

Eco-dormancy is the phase after endo-dormancy, where buds have regained their ability to grow but remain inactive due to unfavorable environmental conditions, mainly low temperatures. During this phase, growth is on hold until warmer temperatures trigger it. Heat accumulation is needed to resume growth. Eco-dormancy ends when enough heat has been accumulated, leading to visible growth changes, typically in late winter or early spring.

The below video *Introduction to dormancy* by [Dr. Erica Fadón](https://scholar.google.de/citations?hl=de&user=MTmTnnsAAAAJ) gives the basic knowledge of this dormancy phases and processes that regulate dormancy.

<iframe src="https://www.youtube.com/embed/qh9AZDmOm3o" width="672" height="400px" data-external="1"></iframe>

## Dormancy physiology

Dormancy as a whole is the result of complex interactions between numerous physiological processes that occur in different parts of the tree, such as buds, twigs, meristems, and vascular tissues. We divide these processes into four main themes:

-   **Transport:** occurs at both the whole-plant and cellular levels
-   **Phytohormone Dynamics:** behavior and levels of plant hormones during dormancy
-   **Genetic and Epigenetic Regulation:** how genetic factors and their modifications influence dormancy
-   **Dynamics of Nonstructural Carbohydrates:** changes in carbohydrate levels that affect dormancy

The following figure from the study ["A conceptual framework for Winter Dormancy in Deciduous Trees"](https://www.mdpi.com/2073-4395/10/2/241#) by Fadón et al. (2015) presents a conceptual framework of winter dormancy in deciduous trees and summarizes the three dormancy phases along with their respective physiological processes.

![Conceptual framework of winter dormancy in deciduous trees. The dormancy framework (gray background) indicates three main phases: (a) dormancy establishment (light gray), (b) endo-dormancy (dark gray), and (c) eco-dormancy (medium gray). For each phase (a–c), the dormancy-related physiological processes are represented by colored shapes and numbers (0 to 4).](images/framework.png)

All the processes depicted are explained in detail in the video below, *Dormancy Physiology* by [Dr. Erica Fadón](https://scholar.google.de/citations?hl=de&user=MTmTnnsAAAAJ).

<iframe src="https://www.youtube.com/embed/HriLSz77QEQ" width="672" height="400px" data-external="1"></iframe>

## Experimental and statistical determination of chilling and forcing periods

Dormancy consists of two phases where temperatures have opposite effects on flowering. During endodormancy, higher chill accumulation leads to earlier flowering, whereas similar cool temperatures during ecodormancy can delay flowering. The challenge lies in differentiating between these two phases, as the tree buds appear to be in the same developmental stage throughout. To address this, there are two methods available:

-   **Experimental method:** collecting buds periodically during winter, exposing them to favorable growth conditions, and evaluating bud break to determine when dormancy is overcome

-   **Statistical method:** uses long-term phenological data and temperature records to estimate the dates of chilling fulfillment and heat accumulation through partial least squares (PLS) regression analysis

The video *Dormancy determination* covers the experimental and statistical methods to determine the chilling and forcing periods for temperate fruit trees to overcome dormancy and initiate growth. It explains the concept of dormancy, its phases (endodormancy and ecodormancy), and the temperature requirements for breaking dormancy.

<iframe src="https://www.youtube.com/embed/hMM27ktlzBM" width="672" height="400px" data-external="1"></iframe>

## Phenology record and BBCH scale

Phenology is the study of periodic events in biological life cycles and how these are influenced by seasonal and interannual variations in climate. This module will involve working with phenology data sets, primarily focusing on a specific stage, usually budbreak, even though trees pass through various developmental stages during the year. These stages are typically identified by numerical codes.

To describe these growth stages systematically, the BBCH scale is employed. This internationally standardized system outlines the growth and developmental phases of plants. The BBCH scale consists of ten main stages, known as principal growth stages, which are numbered from 0 to 9. Each of these main stages is further divided into substages, enabling a more detailed description of a plant's development.

Principal growth stages:

| Stage | Description |
|----|----|
| 0 | Germination / sprouting / bud development |
| 1 | Leaf development (main shoot) |
| 2 | Formation of side shoots / tillering |
| 3 | Stem elongation or rosette growth / shoot development (main shoot) |
| 4 | Development of harvestable vegetative plant parts or vegetatively propagated organs / booting (main shoot) |
| 5 | Inflorescence emergence |
| 6 | Flowering (main shoot) |
| 7 | Development of fruit |
| 8 | Ripening or maturity of fruit and seed |
| 9 | Senescence, beginning of dormancy |

For a comprehensive overview of phenology and the BBCH scale, the video *Phenology* by [Dr. Erica Fadón](https://scholar.google.de/citations?hl=de&user=MTmTnnsAAAAJ) is recommended. In this video, Dr. Fadón explains the concept of phenology and how the BBCH scale uses numerical codes to represent the different developmental stages of trees, from budding and flowering to fruit ripening and leaf fall.

<iframe src="https://www.youtube.com/embed/Ssoe6Ahv88Y" width="672" height="400px" data-external="1"></iframe>

## `Excercises` on tree dormancy

1.  *Put yourself in the place of a breeder who wants to calculate the temperature requirements of a newly released cultivar. Which method will you use to calculate the chilling and forcing periods? Please justify your answer.*

As a breeder aiming to calculate the temperature requirements for the chilling and forcing periods of a newly released cultivar, I would use the experimental method to determine the chilling and forcing periods. Here's my justification:

-   **Direct measurement of bud response:** The experimental method allows me to directly observe when buds break under controlled temperature conditions. By regularly collecting buds during winter and placing them in ideal growth conditions, I can determine exactly when dormancy ends. This practical approach gives me quick and useful information about the specific cultivar

-   **Specific to the cultivar:** Each cultivar has its own unique chilling and forcing needs. The experimental method looks at the specific traits of the new cultivar, making sure the results are relevant and applicable to that variety

-   **Immediate results for breeding decisions:** The experimental method provides quick evaluations of bud break, allowing me to make faster decisions about breeding and managing the new cultivar

2.  *Which are the advantages (2) of the BBCH scale compared with earlier scales?*

-   **Standardization:** The BBCH scale provides a standardized framework for describing plant growth stages, enabling consistent communication and comparisons across studies
-   **Detailed Staging**: It offers a more granular categorization of developmental stages using a two-digit system, allowing for a better understanding of plant development and environmental impacts.

3.  *Classify the following phenological stages of sweet cherry according to the BBCH scale:*

![](images/pheno_stages.png)

-   **left image:** BBCH stage 55 (single flower buds visible (still closed), green scales slightly open)
-   **middle image:** BBCH stage 65 (full flowering: at least 50% of flowers open, first petals falling)
-   **right image:** BBCH stage 89 (fruit ripe for harvesting)

<!--chapter:end:03-tree-dormancy.Rmd-->

# Climate change and impact projection

Before using `chillR`, there's a brief overview of climate change, because the upcoming work will mainly focus on predicting how global warming might affect phenology-related metrics.

Climate change refers to long-term changes in temperatures and weather patterns. While these changes can occur naturally — such as fluctuations in solar activity — since the 19th century, climate change has primarily been driven by human activities, particularly the burning of fossil fuels like coal, oil, and natural gas.

## The drivers of climate change

To understand what's happening to our planet, it's important to know the main causes of climate change. This helps us spot false claims that things like the sun, cities, or natural changes in the climate are the main reasons for global warming. The truth is simple: human-made greenhouse gas emissions are heating up our planet, and the only way to stop this is to greatly reduce these emissions.

The video below, titled *Climate Change 1 - Drivers of Climate Change*, is the first in a series of four videos on the topic of climate change presented by [Eike Lüdeling](https://www.gartenbauwissenschaft.uni-bonn.de/author/prof.-dr.-eike-luedeling/). It provides a comprehensive overview of the primary drivers of global climate change, such as greenhouse gases, aerosols, solar radiation, ozone, and others.

<iframe src="https://www.youtube.com/embed/lFtc-Y5OYNs" width="672" height="400px" data-external="1"></iframe>

## What's already known

The next video, *Climate Change 2 - Recent Warming*, explores climatic changes that have already occurred or for which there is substantial evidence. It demonstrates that the planet has experienced significant warming for several decades, almost globally.

<iframe src="https://www.youtube.com/embed/sLmfKcvsWow" width="672" height="400px" data-external="1"></iframe>

## Future scenarios

When it comes to climate change, the most severe impacts are still ahead. This is largely due to the significantly higher rate of greenhouse gas emissions observed over the past few decades, with no signs of a slowdown in the near future. As a result, the human-induced 'forcing' effect on our climate has reached unprecedented levels, making it likely that future changes will occur even more rapidly than those we have already witnessed. The next video *Climate Change 3 - Future scenarios* introduces the methods that climate scientists employ to forecast future conditions and presents climate scenarios developed by these scientists, which researchers in other fields can use to project the impacts of climate change on ecological and agricultural systems.

<iframe src="https://www.youtube.com/embed/PX6fAxBEkCE" width="672" height="400px" data-external="1"></iframe>

## Impact projections approaches

Having robust climate scenarios is essential, but they only take us partway toward reliable assessments of climate change impacts. A potentially greater challenge lies in translating these climate scenarios into biological consequences. To achieve this, we need impact models or other methods to derive the impacts of climate change. The last video *Climate change 4 - impact projection approaches* introduces various methods for projecting climate impacts.

<iframe src="https://www.youtube.com/embed/3Q8HF4E7rkM" width="672" height="400px" data-external="1"></iframe>

## `Exercises` on climate change

1.  *List the main drivers of climate change at the decade to century scale, and briefly explain the mechanism through which the currently most important driver affects our climate.*

The main drivers of climate change on a decade-to-century scale include:

-   **Greenhouse Gases (GHGs):** GHGs like carbon dioxide (CO₂), methane (CH₄), and nitrous oxide (N₂O) trap heat in the atmosphere, leading to the greenhouse effect, which raises Earth's temperature. The increase in these gases is primarily due to human activities, such as burning fossil fuels, industrial processes, and deforestation

-   **Aerosols:** Particles in the atmosphere that can cool the climate by reflecting sunlight. They come from both natural sources (e.g. sea salt, dust, volcanic eruptions, fires) and human activities (e.g.power plants, cars, fires and cook stove). They are major climate driver in industrial centers (e.g. China)

-   **Sun:** Solar radiation heats the Earth, with minor fluctuations occurring over time due to cycles in solar activity, such as sunspots. Although these variations contribute only a small portion to the current climate changes, they play a significant role in driving climate change over geological timescales

-   **Ozone:** Ozone in the stratosphere protects Earth from UV-B radiation, while tropospheric ozone acts as a greenhouse gas and contributes to warming

-   **Surface albedo:** The reflectivity of the Earth's surface affects how much solar energy is absorbed. Light surfaces (like ice) reflect more energy, while dark surfaces (like forests or oceans) absorb more, influencing the planet's heat balance. Changes in surface reflectivity, such as melting ice and snow, decrease the albedo effect, leading to more heat absorption and further warming

The currently most important driver of climate change is greenhouse gases, particularly CO₂. The mechanism through which CO₂ affects the climate involves the greenhouse effect: CO₂ molecules in the atmosphere absorb long-wave radiation emitted from the Earth's surface and re-radiate it in all directions, including back toward the surface. This process traps heat and increases global temperatures, driving many of the changes we observe in climate patterns.

2.  *Explain briefly what is special about temperature dynamics of recent decades, and why we have good reasons to be concerned.*

In recent decades, global temperatures have been rising at a faster rate than at any other time in human history. This trend is evident from the fact that the hottest years on record have all occurred within the last few decades. One striking example is the extreme heat in Siberia in the spring of 2020, where temperatures were up to 8°C above the recent average. This trend is particularly concerning because it is mainly driven by human activities, especially the emission of greenhouse gases. Unlike previous climate changes, which took place slowly over long periods, today’s fast rise in temperatures increases the risk of triggering dangerous effects, like melting permafrost and losing ice cover, which could make global warming even worse. Even a small increase of 1.5°C could seriously upset the balance of our climate, showing how important it is to take action against these human-caused changes.

3.  *What does the abbreviation ‘RCP’ stand for, how are RCPs defined, and what is their role in projecting future climates?*

RCP stands for Representative Concentration Pathways, which are essential scenarios used in climate modeling to project potential future greenhouse gas emissions and their impacts on the climate. RCPs are defined by the level of radiative forcing — measured in watts per square meter (W/m²) — that is expected by the end of the 21st century. Each pathway corresponds to a specific amount of greenhouse gas concentrations, which can significantly influence global temperatures. The role of RCPs is to serve as inputs for climate models, helping to produce future climate scenarios, which are essential for understanding the potential impacts of climate change and planning appropriate mitigation and adaptation strategies.

4.  *Briefly describe the 4 climate impact projection methods described in the fourth video.*

The four climate impact projection methods described in the fourth video are:

-   **Statistical models:** These models establish relationships between climate parameters and impact measures, such as crop yield. They use historical data to explain past trends and project future climate impacts. Their primary limitation is that the statistical relationships may not remain valid under future climate conditions, and they may overlook important factors

-   **Species Distribution Modeling:** Also known as ecological niche modeling, this method predicts the future distribution of species by relating current presence or absence data to climatic parameters. However, these models may assume species are in equilibrium with the climate, which is often not the case

-   **Process based models:** These models aim to represent all major system processes using equations, capturing the scientific knowledge of processes like crop growth, phenology or hydrology. However, they are limited by the lack of complete understanding of complex systems, and often require extensive parameterization or assumptions

-   **Climate Analogue models:** This method identifies current locations with climates similar to those expected in the future at another site, offering real-world examples that can guide adaptation strategies. However, they may be limited by differences in non-climatic factors and lack of suitable data, making it difficult to draw clear conditions

<!--chapter:end:04-climate.Rmd-->

# Winter chill projections

This section provides an overview of how winter chill can be modeled. It summarizes past studies on this topic, aiming to clarify the methodological aspects that lead to the analyses conducted. By the end of this lesson, most of the analyses presented in the discussed papers should be understandable.

## Learning goals

-   Be aware of past studies that have projected climate change impacts on winter chill
-   Get a rough idea of how such studies are done
-   Get curious about how to do such studies

## Winter chill in Oman

During his doctoral studies at the University of Kassel, [Prof. Dr. Eike Lüdeling](https://www.gartenbauwissenschaft.uni-bonn.de/author/prof.-dr.-eike-luedeling/) became interested in winter chill while participating in research on mountain oases in Oman. Initially focused on calculating nutrient budgets for the oases, particularly in the "Hanging Gardens" of Ash Sharayjah, the study shifted when many fruit trees failed to bear fruit. This led to the hypothesis that insufficient winter chill might be the issue, especially since the oases hosted temperate species such as pomegranates (*Punica granatum*), walnuts (*Juglans regia*), and apricots (*Prunus armeniaca*).

To investigate this, temperature loggers were placed in three oases at different levels of elevation, allowing for the study of chill accumulation along an elevation gradient. A map of the study area illustrates the locations of the oases:

![***Map of oasis systems in Al Jabal Al Akhdar, Oman***](images/Fig_01_gradient_map.jpg)

A nearby long-term weather station provided valuable data, although its location - 1000 meters above the lowest oasis - limited its representativeness. Since records were available from the oases, transfer functions were defined to derive oasis temperatures from the long-term data. These transfer functions were set up using PLS regression, which, in hindsight, wasn’t a very good idea, to directly calculate hourly temperatures in the oases from the daily records of the official station at Saiq.

![**Regression between temperature at Saiq and temperature in three oases, Al Jabal Al Akhdar, Oman**](images/Luedeling_JPG_Figure_02_Hourly_regressions.jpg)

This approach facilitated the calculation of hourly temperatures, which were essential for assessing winter chill dynamics over several years.

![**Chill dynamics between 1983 and 2007, Al Jabal Al Akhdar, Oman**](images/Luedeling_JPG_Figure_09_chilling_hours.jpg)

The findings were submitted to the journal Climatic Change ([Luedeling et al., 2009b](https://link.springer.com/article/10.1007/s10584-009-9581-7)), where reviewers suggested incorporating future climate scenarios. To address this, the LARS-WG weather generator was employed to simulate plausible weather conditions for the oases under scenarios of 1°C and 2°C warming.

![**Chill prospects for 1°C and 2°C warming scenarios in Al Jabal Al Akhdar, Oman**](images/Luedeling_JPG_Figure_10_Future_chilling.jpg)

The results illustrated the potential impacts of climate change on winter chill, marking the beginning of a career focused on chill modeling.

## Chill model sensitivity

After completing a PhD at the University of Kassel, [Prof. Dr. Eike Lüdeling](https://www.gartenbauwissenschaft.uni-bonn.de/author/prof.-dr.-eike-luedeling/) became a Postdoctoral Scholar at the University of California at Davis, where his research focused on climate change impacts on winter chill in California's Central Valley, a key region for temperate fruit tree production.

Upon arriving in California, it became evident that the choice of chill model significantly impacts winter chill quantification. Initially, the simplest model was chosen due to a lack of programming skills, but further investigation highlighted the importance of model selection. Extensive library research revealed the need for a thorough examination of various chill models. Knowledge gained in Oman was utilized to create temperature scenarios for multiple locations, allowing for the analysis of how chill accumulation would likely change in the future.

The analysis focused on changes predicted by various models for the same locations and future scenarios. Here are the locations examined:

![**Weather station locations in California**](images/Luedeling_Figure_1.jpg)

The results revealed considerable variation in chill projections for these locations. The analysis illustrated significant differences in estimates of chill losses by 2050, indicating that not all models could accurately represent winter chill dynamics. Ultimately, the Dynamic Model emerged as the most reliable option, prompting its primary use in subsequent research.

![**Sensitivity of chill projections to model choice (CH - Chilling Hours; Utah - Utah Model; Utah+ - Positive Utah Model; Port. - Dynamic Model)**](images/Luedeling_Figure_2.jpg)

However, challenges arose with the complexity of the Dynamic Model, which required outdated Excel software for calculations. Additionally, the data processing steps necessary to generate credible temperature scenarios proved cumbersome and error-prone, highlighting the need to develop programming skills for more efficient analysis.

## Winter chill in California

The primary goal during the time in California was to create a winter chill projection for the Central Valley, an important region for fruit and nut production. Utilizing California's extensive network of weather stations, the plan involved using data from over 100 stations and generating multiple climate scenarios. To manage this complex task efficiently, a decision was made to automate most processes, leading to an exploration of programming.

The automation was implemented using JSL, a programming language associated with the statistics software JMP, which facilitated the handling of the data. Despite some challenges, the automation was largely successful, though running the weather generator manually for each station remained tedious. Ultimately, projections were generated for all stations, illustrating chill accumulation over 100 plausible winter seasons for each climate scenario.

To present the results effectively, a metric called 'Safe Winter Chill' was developed, defined as the 10th percentile of the chill distribution, indicating the minimum chill amount that would be exceeded in 90% of the years. Here’s an illustration of the Safe Winter Chill metric:

![**Illustration of the Safe Winter Chill concept**](images/Figure_2_Boxplots_Davis_chilling_hours_a2.jpg)

A method for spatially interpolating the station results was also established, leading to the creation of maps that depicted winter chill prospects for the Central Valley. Here’s one of the maps that resulted from this:

![**Winter chill prospects for California’s Central Valley**](images/Figure_4_Chill_Portions_Central_Valley_absolute.jpg)

This analysis was published in the journal PLOS ONE ([Luedeling et al., 2009d](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0006166)).

## Winter chill ratios

Following the automation of processing steps in JSL, attention turned to creating a global winter chill projection. The Global Summary of the Day database was identified as a valuable data source, featuring records from thousands of weather stations. The project proved challenging due to limited programming skills. Data processing was carried out on six computers operating around the clock for several weeks, likely a result of initial setup difficulties rather than the complexity of the analyses. In the end, data for about 5,000 weather stations were processed, generating multiple chill metrics.

This extensive dataset allowed for a comparison of chill models by calculating the ratios between various chill metrics at each station. If these ratios had been consistent worldwide (e.g., one Chill Portion always equating to ten Chilling Hours), any chill model could have been reliably used. However, significant variations in chill metric ratios were observed globally.

![**Chill metric ratios around the world**](images/Luedeling_Fig_4_all_ratios_map.jpg)

This study was published in the International Journal of Biometeorology ([Luedeling & Brown, 2011a](https://link.springer.com/article/10.1007/s00484-010-0352-y)).

## A global projection of future winter chill

Using the same analytical methods, a global projection of the potential impacts of climate change on winter chill was also generated:

![**Projected decline in available winter chill around the world**](images/Figure_5_Time_Comp.jpg)

The regions marked in red and orange on the lower two maps may experience significant impacts on fruit and nut production due to decreasing winter chill. With substantial chill losses, it is unlikely that growers will be able to sustain their current tree cultivars. Notably, the Mediterranean region is expected to be particularly affected.

![**Winter chill projection for the Mediterranean region**](images/Figure_6_regional_grids_Mediterranean.jpg)

This prompted collaboration with partners in the Mediterranean region and other countries with similar climates, such as South Africa and Chile.

## Winter chill in Germany

Germany is not highlighted as particularly vulnerable to chill losses, and an analysis of historical chilling trends from 1950 supports this observation:

![**Winter chill in Germany in 2010, and changes between 1950 and 2010**](images/Chilling_Germany.png)

## Winter chill in Tunisia

Prospects for orchards in Tunisia are particularly challenging due to the region being close to the warmest limits for many fruit and nut tree species. An assessment published in 2018 examined past and future trends in winter chill for an orchard in Central Tunisia, following a seven-year gap from earlier studies. This delay stemmed from other professional commitments and the difficulty of obtaining suitable future climate data for chill modeling.

While climate change data is widely available, much of it is presented as spatial grids, making it cumbersome to work with. Each climate scenario requires numerous grids for temperature and rainfall, leading to substantial data storage needs, sometimes exceeding 700 GB. Soon after establishing a processing structure for these datasets, the IPCC introduced the Representative Concentration Pathways (RCPs), rendering earlier scenarios outdated and complicating the analysis further, especially given the limited data transfer capabilities while based in Kenya.

Collaboration with colleagues in Tunisia, particularly [Haifa Benmoussa](https://scholar.google.de/citations?hl=de&user=DdV9jsAAAAAJ), revealed that tree crops like almonds and pistachios are highly vulnerable to climate change impacts. Fortunately, a new climate database specifically for Africa, called AFRICLIM, was developed, facilitating the acquisition and processing of relevant climate scenarios. This allowed for the incorporation of new functions in `chillR` to sample from AFRICLIM grids and produce the necessary climate projections.

![**Winter chill analysis for an orchard near Sfax in Central Tunisia (blue bars indicate approximate chilling requirements of pistachios and two types of almonds)**](images/Tunisia_2018_Fig_1.jpg)

The figure, which is to be created by the end of the semester, illustrates the historical development of chill accumulation at a specific location, with observed values represented by red dots and typical chill distributions shown as boxplots. These data were generated using a weather generator that is calibrated with historical weather data and produces artificial annual weather records. The generator was also used to create future scenarios based on the AFRICLIM database.

The analysis indicates that in none of the future scenarios does the cultivation of pistachios or high-chill almonds remain viable. This conclusion is supported by observations in Tunisia, where, after the warm winter of 2015/16, many pistachio trees barely developed any flowers, leading to crop failures.

![**Pistachio tree near Sfax, Central Tunisia, in April of 2016**](images/Tunisia_pistachios.png)

## Winter chill in Chile

AFRICLIM addressed the challenge of obtaining future climate data for Africa but did not fully meet the needs for integrating climate change projections into `chillR`. It was limited to African data, and users seeking information for single locations had to download large datasets, which was inefficient. A more effective solution was needed to access data quickly for individual weather stations globally.

An early resource was ClimateWizard, developed by [Evan Girvetz](https://scholar.google.de/citations?user=Yh2sQY4AAAAJ&hl=de), which initially provided gridded data but later included a script for extracting information for specific locations. This functionality was eventually made available through an API at CIAT, allowing access to outputs from 15 climate models for the latest RCP scenarios. This advancement enabled [Eduardo Fernández](https://scholar.google.de/citations?hl=de&user=ibSma_AAAAAJ) to analyze past and future chill development across nine locations in Chile, expanding the geographic scope of the research.

![**Map of fruit growing locations in Chile**](images/Chile_chill_map.png)

The following diagram illustrates the assessment of past and future winter chill across nine locations in Chile:

![**Assessment of past and future winter chill for 9 locations across Chile**](images/Chile_chill_all.png)

Eduardo preferred a different plot design and utilized the `ggplot2` package, a robust plotting tool for R, to redesign it. The complexity of having data from multiple sites made interpretation challenging, prompting Eduardo to creatively summarize key information for each scenario. He presented this information as a heat map, simplifying the visualization.

![**Heatmap showing Safe Winter Chill (10% quantile of chill distribution) for nine locations in Chile**](images/Chile_chill_heatmap.png)

## Chill projection for Patagonia

Certain regions may become more suitable for agriculture as the climate changes. An analysis was conducted to assess the climatic suitability for fruit and nut trees in Patagonia, southern Argentina, which is located at the southern frontier of agriculture:

![**Map of parts of Patagonia in Argentina, showing locations that were analyzed in this study** ](images/Patagonia_map.png)

Weather station records for all locations on the map were obtained, enabling the calibration of a weather generator and the download of climate projections from the ClimateWizard database. This facilitated the creation of past and future temperature scenarios for all stations, as well as the computation of winter chill and other agroclimatic metrics. However, the results of the winter chill calculations were not particularly noteworthy, as minimal changes were projected.

![**Heatmap showing Safe Winter Chill (10% quantile of chill distribution) for eleven locations in Patagonia**](images/Patagonia_heatmap.png)

Climate change could potentially enhance land suitability for fruit trees by providing increased summer heat:

![**Past and projected future heat availability for four exemplary locations in Patagonia**](images/Patagonia_heat.png)

A further beneficial development is a likely reduction in the number of frost hours:

![**Past and projected frost risk for four exemplary locations in Patagonia**](images/Patagonia_frost.png)

While the changes observed may appear minor, they are likely to shift many locations from a climate that is too cool for agriculture, particularly for fruit trees, to a more optimal situation. This presents a rare instance of potentially positive news related to climate change, though it is important to acknowledge that these changes could have negative consequences for natural ecosystems and other agricultural systems.

## Chill model comparison

Eduardo Fernandez recently utilized the climate change analysis framework to enhance previous chill model comparisons, significantly building on earlier work. He compiled a collection of 13 methods for quantifying chill accumulation from existing literature and applied these models to datasets from several locations in Germany, Tunisia, and Chile, which are part of the PASIT project. A map illustrates the locations included in this analysis.

![**Locations used for comparing predictions by a total of 13 chill models across different climates**](images/Model_comp_map.png)

The expectation was that the models would show significant differences in the extent of changes they predicted, and this anticipation was indeed fulfilled:

![**Chill change projections by a total of 13 chill models across different climate scenarios**](images/Model_comp_results.png)

The figure illustrates the changes predicted by 13 different models across various sites and climate scenarios, categorized into three groups: warm, moderate, and cool. Eduardo’s analysis reveals significant discrepancies among the models, highlighting the risks of selecting the most convenient model for predictions. The variation in predictions is evident in the color distribution across the rows of the panels, with a uniform color indicating consistency among models—something that is not observed here.

For locations in Tunisia and Chile, the predictions mainly concern the extent of chill losses, ranging from mild to alarming. In Germany, the situation is even less clear, with some models predicting increases in chill and others predicting decreases.

These findings underscore the importance of model choice, as many models may be arbitrary and can be disregarded, yet uncertainties remain regarding which models accurately represent future conditions. This area of research offers opportunities for further exploration and innovation.

## Chill projection for all of Tunisia

The study projected climate change impacts on winter chill for an orchard near Sfax in Central Tunisia, but the region is not the most favorable for temperate fruit and nut tree cultivation. Tunisia is climatically diverse, featuring mountains, plains, coastal areas, and interior deserts, leading to significant variation in historical and future chill availability across the country.

Under the leadership of [Haifa Benmoussa](https://scholar.google.de/citations?hl=de&user=DdV9jsAAAAAJ), the team mapped chill accumulation throughout Tunisia using a framework previously developed. This analysis utilized data from 20 weather stations in Tunisia and neighboring countries. By applying the established analytical framework to each location, they were able to interpolate results and create chill maps that illustrate the trends in chill availability in Tunisia over the past few decades:

![**Chill availability maps for Tunisia for several past scenarios**](images/Figure_1_Tunisia_historic.png)

The process of interpolating site-specific results into a comprehensive map for Tunisia involves some areas for improvement. Currently, the methodology uses site-specific predictions of Safe Winter Chill, defined as the 10th percentile of the chill distribution derived from annual temperature dynamics generated by the weather model. This information is then interpolated using the Kriging technique.

In addition, the elevations of the locations where chill was modeled are also considered. A linear model is fitted to establish a relationship between chill accumulation and elevation. Using a Digital Elevation Model (DEM), the differences between the model-derived elevations from weather stations and the actual elevations of each location are calculated. This difference, not accounted for in the initial chill surface derived from weather station data, is corrected using the established elevation-chill relationship.

While this method seems reasonable for Tunisia, it may not be suitable for cooler regions like Germany, where the relationship between elevation and chill availability may not be linear. The resulting projection of future chill for Tunisia is displayed in the following map:

![**Chill availability for Tunisia for various plausible scenarios of future climate**](images/Figure_2_Tunisia_all_scenarios.png)

The projections reveal significant concern regarding winter chill in Tunisia. The Dynamic Model, which is regarded as a reliable predictor, indicates substantial decreases in Chill Portions, the units used by the model. This trend poses serious challenges for much of the country. Even in areas where some winter chill is expected to persist, farmers will need to adapt their practices, as the tree species currently cultivated are suited to past climate conditions. Adaptation strategies may include shifting to tree cultivars with lower chilling requirements, provided such options are available.

## Revisiting chill accumulation in Oman

After a decade of exploration in other regions, the analysis turned back to Oman, where there was a desire to enhance the initial study of chill accumulation. The first assessment had limitations, particularly concerning model selection and a lack of adequate future climate data. With encouragement from [Prof. Dr. Andreas Bürkert](https://scholar.google.de/citations?user=ZNvcJJ8AAAAJ&hl=de), a more robust evaluation became possible using the climate change analysis framework. This involved incorporating new methods to convert daily temperatures into hourly data. Updated assessments of past winter chill and future forecasts for the oases of Al Jabal Al Akhdar were produced, with the findings published in *Climatic Change* ([Buerkert et al., 2020](https://link.springer.com/article/10.1007/s10584-020-02862-8)).

## `Exercises` on past chill projections

1.  *Sketch out three data access and processing challenges that had to be overcome in order to produce chill projections with state-of-the-art methodology.*

-   **Accessing Climate Data for Specific Locations**:\
    Previous climate datasets like AFRICLIM and ClimateWizard only provided large-scale data. To get weather data for specific locations without downloading too much extra information, an API was created to quickly access data for single sites

-   **Converting Daily to Hourly Temperature Data**:\
    Chill models need hourly temperature data, but many databases only give daily averages. Early methods for converting daily to hourly data weren't very good, especially in areas with unique temperatures. Improved algorithms were developed to estimate hourly temperatures more accurately from daily data

-   **Handling Large Volumes of Climate Model Outputs**:\
    Studying different climate futures involves dealing with a lot of data from many climate models, which can be hard to manage. To handle this large amount of data effectively, workflows were streamlined and selective processing techniques were used

2.  *Outline, in your understanding, the basic steps that are necessary to make such projections.*

To make climate-based chill projections for specific regions, here are the essential steps typically involved:

-   **Data Collection and Calibration:** collect historical weather data and use it to calibrate a weather generator for realistic temperature simulations

-   **Model Selection and Scenario Setup:** choose relevant climate models and emission scenarios to explore various future climates

-   **Generate Temperature Projections:** downscale climate data, converting it to daily or hourly temperatures as needed for chill calculations

-   **Chill Calculation:** apply chill models to estimate chill accumulation across different climate scenarios

-   **Analysis and Visualization:** compare chill projections across models and scenarios and visualize the findings

-   **Interpretation:** validate projections with observed data where possible and assess agricultural impacts and adaptation needs

<!--chapter:end:05-winter-chill.Rmd-->

# Manual chill

This chapter explains how to calculate Chilling Hours using R and the `chillR` package. Chilling Hours measure the number of hours where temperatures are between 0°C and 7.2°C, which is important for certain plants to meet their cold requirements during dormancy and grow properly.

## Learning goals

-   Learn about some basic R operations we need for calculating Chilling Hours
-   Be able to calculate Chilling Hours
-   Understand what an R function is
-   Be able to write your own basic function

## Chilling hours calculation using chillR

Basic models like the Chilling Hours Model are simple and can be calculated manually, especially if familiar with R or spreadsheet software. This example will show how to understand and use the functions in the `chillR` package to calculate these chill hours.

### **Data Requirements**

The Chilling Hours Model is relatively simple but requires hourly temperature data. A common challenge is the unavailability of such data, though approximations can be made from daily records using `chillR` tools. For this example, a sample dataset, `Winters_hours_gaps`, provided within `chillR`, was used. It contains hourly temperature data recorded in 2008 from a walnut orchard in Winters, California, and is structured with columns for year, month, day, hour, and temperature.

### Loading and Preparing Data

To work with `chillR`, the package was loaded using `library(chillR)`. The data can also be imported via `read.table()` or `read.csv()` for external datasets. The `Winters_hours_gaps` dataset was filtered to retain only the essential columns: year, month, day, hour, and temperature. This cleaned version, stored in a new dataframe called `hourtemps`, ensures the data is in the correct format for calculating Chilling Hours:




``` r
hourtemps <- Winters_hours_gaps[,c("Year",
                                   "Month",
                                   "Day",
                                   "Hour",
                                   "Temp")]
```



<table class="table table-striped table-hover" style="font-size: 15px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Temp </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 15.127 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 17.153 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 18.699 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 18.699 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 18.842 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 19.508 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 19.318 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 17.701 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 15.414 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 12.727 </td>
  </tr>
</tbody>
</table>

### **Manual Calculation of Chilling Hours**

Chilling Hours are defined as any hour where the temperature falls between 0°C and 7.2°C. A logical comparison was used in R to identify whether each hour met this criterion:


``` r
hourtemps[, "Chilling_Hour"] <- hourtemps$Temp >= 0 & hourtemps$Temp <= 7.2
```

<table class="table table-striped table-hover" style="font-size: 15px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Temp </th>
   <th style="text-align:center;"> Chilling_Hour </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 15.127 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 17.153 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 18.842 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 19.508 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 19.318 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 17.701 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 15.414 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 12.727 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
</tbody>
</table>

A new column, `Chilling_Hour`, was created, indicating whether a given hour was a valid Chilling Hour (TRUE or FALSE). These values can then be summed to calculate the total number of Chilling Hours for any period using the `sum()` function.

### Automation with Functions

A function is a tool that automates a particular procedure. It consists of a name, some arguments that are passed to the function, and some code that should be executed. To avoid repeating manual calculations, a reusable function called `CH` was created to automate the addition of a `Chilling_Hour` column:


``` r
CH <- function(hourtemps) {
  hourtemps[, "Chilling_Hour"] <- hourtemps$Temp >= 0 & hourtemps$Temp <= 7.2
  return(hourtemps)
}
```

This function applies to any appropriately structured dataset. Additionally, a more complex function, `sum_CH`, was developed to calculate the total Chilling Hours between two specific dates:


``` r
sum_CH <- function(hourtemps, Start_Year,
                              Start_Month,
                              Start_Day, 
                              Start_Hour, 
                              End_Year, 
                              End_Month, 
                              End_Day, 
                              End_Hour) 
  
{hourtemps[,"Chilling_Hour"] <- hourtemps$Temp > 0 &
                                hourtemps$Temp  <= 7.2

  Start_Date <- which(hourtemps$Year == Start_Year & 
                      hourtemps$Month == Start_Month &
                      hourtemps$Day == Start_Day &
                      hourtemps$Hour == Start_Hour)
  
  End_Date <- which(hourtemps$Year == End_Year &
                    hourtemps$Month == End_Month &
                    hourtemps$Day == End_Day & 
                    hourtemps$Hour == End_Hour)
  
  CHs <- sum(hourtemps$Chilling_Hour[Start_Date:End_Date])
  return(CHs)
}
```

This function calculates Chilling Hours for a user-defined date range, using the `which()` function to identify the relevant rows in the dataset corresponding to the start and end dates.

To simplify the parameter passing, compact strings in the format `YEARMODAHO` (year, month, day, and hour as consecutive numbers) can be used instead of individual parameters for year, month, day, and hour. The start and end times are now passed as strings, from which the required values are extracted using the `substr()` function and converted to numeric values with `as.numeric()`.


``` r
sum_CH <- function(hourtemps, 
                   startYEARMODAHO,
                   endYEARMODAHO)
{hourtemps[,"Chilling_Hour"] <- hourtemps$Temp > 0 &
  hourtemps$Temp <= 7.2

startYear <- as.numeric(substr(startYEARMODAHO, 1, 4))
startMonth <- as.numeric(substr(startYEARMODAHO, 5, 6))
startDay <- as.numeric(substr(startYEARMODAHO, 7, 8))
startHour <- as.numeric(substr(startYEARMODAHO, 9, 10))

endYear <- as.numeric(substr(endYEARMODAHO, 1, 4))
endMonth <- as.numeric(substr(endYEARMODAHO, 5, 6))
endDay <- as.numeric(substr(endYEARMODAHO, 7, 8))
endHour <- as.numeric(substr(endYEARMODAHO, 9, 10))


Start_row <- which(hourtemps$Year == startYear &
                   hourtemps$Month == startMonth &
                   hourtemps$Day == startDay &
                   hourtemps$Hour == startHour
)
End_row <- which(hourtemps$Year == endYear &
                 hourtemps$Month == endMonth &
                 hourtemps$Day == endDay &
                 hourtemps$Hour == endHour
)

CHs <- sum(hourtemps$Chilling_Hour[Start_row:End_row])
return(CHs)

}
```

### Application Example

The functions created allow for efficient calculation of Chilling Hours. For instance, using the `sum_CH()` function, it was calculated that between April 1st and October 11th, 2008, the walnut orchard experienced 77 Chilling Hours:


``` r
sum_CH(hourtemps, startYEARMODAHO =2008040100,
                  endYEARMODAHO = 2008101100)
```

```
## [1] 77
```

## `Exercises` on basic chill modeling

1.  *Write a basic function that calculates warm hours (\>25°C).*


``` r
WH <- function(data)
  {data[, "Warm_Hour"] <- data$Temp > 25
  return(data)
}
```

2.  *Apply this function to the* `Winters_hours_gaps` *dataset.*


``` r
WH(Winters_hours_gaps)
```

<table class="table table-striped table-hover" style="font-size: 15px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Temp_gaps </th>
   <th style="text-align:center;"> Temp </th>
   <th style="text-align:center;"> Warm_Hour </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 15.127 </td>
   <td style="text-align:center;"> 15.127 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 17.153 </td>
   <td style="text-align:center;"> 17.153 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> 18.699 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 18.842 </td>
   <td style="text-align:center;"> 18.842 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 19.508 </td>
   <td style="text-align:center;"> 19.508 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 19.318 </td>
   <td style="text-align:center;"> 19.318 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 17.701 </td>
   <td style="text-align:center;"> 17.701 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 15.414 </td>
   <td style="text-align:center;"> 15.414 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 12.727 </td>
   <td style="text-align:center;"> 12.727 </td>
   <td style="text-align:center;"> FALSE </td>
  </tr>
</tbody>
</table>

3.  *Extend this function, so that it can take start and end dates as inputs and sums up warm hours between these dates.*


``` r
sum_WH <- function(data, 
                   startYEARMODAHO,
                   endYEARMODAHO)
  
{data[,"Warm_Hour"] <- data$Temp > 25

startYear <- as.numeric(substr(startYEARMODAHO, 1, 4))
startMonth <- as.numeric(substr(startYEARMODAHO, 5, 6))
startDay <- as.numeric(substr(startYEARMODAHO, 7, 8))
startHour <- as.numeric(substr(startYEARMODAHO, 9, 10))

endYear <- as.numeric(substr(endYEARMODAHO, 1, 4))
endMonth <- as.numeric(substr(endYEARMODAHO, 5, 6))
endDay <- as.numeric(substr(endYEARMODAHO, 7, 8))
endHour <- as.numeric(substr(endYEARMODAHO, 9, 10))


Start_Date <- which(data$Year == startYear &
                    data$Month == startMonth &
                    data$Day == startDay &
                    data$Hour == startHour)

End_Date <- which(data$Year == endYear &
                  data$Month == endMonth &
                  data$Day == endDay &
                  data$Hour == endHour)

WHs <- sum(data$Warm_Hour[Start_Date:End_Date])
return(WHs)
}
```

Application Example:


``` r
sum_WH(Winters_hours_gaps, startYEARMODAHO = 2008080100, 
                           endYEARMODAHO = 2008083100)
```

```
## [1] 283
```

During the month of August 2008, from the 1st to the 31st, the walnut orchard experienced a total of 283 warm hours (defined as hours when the temperature exceeded 25°C).

<!--chapter:end:06-manual-chill.Rmd-->

# Chill

In this chapter, various chill models will be explored using the `chillR` package in R, which simplifies the calculation of chilling hours and other dormancy-related metrics based on temperature data.

## Learning goals

-   Learn how to run chill models using `chillR`
-   Learn how to produce your own temperature response model in `chillR`

## `Chilling_Hours()` function

The `Chilling_Hours()` function calculates the time during which temperatures fall within a key range for chill accumulation. It takes hourly temperature data as input and, by default, provides the cumulative amount of chilling accumulated over time.




``` r
Chilling_Hours(Winters_hours_gaps$Temp)[1:100]
```

```
##   [1]  0  0  0  0  0  0  0  0  0  0  0  0  0  0  1  2  2  2  3  4  5  6  6  6  6  6  6  6  6  6
##  [31]  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6  6
##  [61]  6  7  8  9 10 11 12 13 14 15 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 17 18 19 20 21
##  [91] 22 23 24 25 25 25 25 25 25 25
```

The result will show the first 100 values, where the cumulative chilling hours increase as the temperature falls within the specified range.

## Utah Model

The Utah Model assigns different weights to various temperature ranges, reflecting their impact on chill accumulation. The `Utah_Model()` function in `chillR` calculates these weighted chilling contributions for each hour of temperature data. The output will show the Utah model values for the first 100 hours, where positive, zero, and negative weights are applied based on the temperature:


``` r
Utah_Model(Winters_hours_gaps$Temp)[1:100]
```

```
##   [1]  0.0 -0.5 -1.5 -2.5 -3.5 -4.5 -5.5 -6.0 -6.0 -6.0 -5.5 -5.0 -4.0 -3.0 -2.0 -1.0  0.0  0.5
##  [19]  1.5  2.5  3.5  4.5  5.0  5.0  5.0  4.0  3.0  2.0  1.0  0.0 -1.0 -2.0 -2.5 -2.5 -2.0 -1.5
##  [37] -1.0 -0.5  0.5  1.0  1.5  2.0  2.0  2.5  3.0  3.5  4.0  4.0  4.0  3.5  2.5  1.5  0.5 -0.5
##  [55] -1.5 -2.5 -3.0 -3.0 -2.5 -1.5 -0.5  0.5  1.5  2.5  3.5  4.5  5.5  6.5  7.5  8.5  9.5 10.0
##  [73] 10.0  9.5  9.0  8.5  8.0  7.5  7.0  6.5  6.5  7.0  7.5  8.5  9.5 10.5 11.5 12.5 13.5 14.5
##  [91] 15.5 16.5 17.5 18.5 19.0 19.0 19.0 18.5 17.5 16.5
```

## Creating Custom Chill Models with `step_model()`

The `step_model()` function, part of the `chillR` package, enables the creation of custom chill models based on temperature thresholds and weights. This process involves defining a data frame that specifies temperature ranges and their corresponding weights. Here’s an example of a data frame that defines temperature ranges and their corresponding weights:


``` r
df <- data.frame(
  lower = c(-1000, 1, 2, 3, 4, 5,    6),
  upper = c(    1, 2, 3, 4, 5, 6, 1000),
  weight = c(   0, 1, 2, 3, 2, 1,    0))
```

<table class="table table-striped table-hover" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> lower </th>
   <th style="text-align:center;"> upper </th>
   <th style="text-align:center;"> weight </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> -1000 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 3 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 1000 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
</tbody>
</table>

A function called `custom()` implements a chill model based on this data frame. This function is then applied to the `Winters_hours_gaps` dataset to calculate the chilling contributions:


``` r
custom <- function(x) step_model(x, df)
custom(Winters_hours_gaps$Temp)[1:100]
```

```
##   [1]  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  1  4  7  7  7  7  7  7  7  7  7
##  [31]  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7  7
##  [61]  7  7  7  7  8 10 13 16 19 22 22 22 22 22 22 22 22 22 22 22 22 22 22 22 22 22 22 23 25 27
##  [91] 29 31 34 37 37 37 37 37 37 37
```

## Dynamic model

The Dynamic Model provides a more complex and reliable approach to calculating chill, with the `Dynamic_Model()` function handling the intricate equations involved. This function can be easily applied to the `Winters_hours_gaps` dataset, producing output that displays dynamic chill values for the first 100 hours, reflecting the underlying physiological processes:


``` r
Dynamic_Model(Winters_hours_gaps$Temp)[1:100]
```

```
##   [1] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [10] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [19] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [28] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [37] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [46] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [55] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000
##  [64] 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.0000000 0.9698435
##  [73] 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435
##  [82] 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435
##  [91] 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435 0.9698435
## [100] 0.9698435
```

## `Chilling` and `tempResponse` functions

The `chillR` package offers several functions for analyzing hourly temperature data, including wrapper functions that enable the computation of chill between specific start and end dates. The `chilling()` function automatically calculates various basic metrics, including Chilling Hours, Utah Model, Dynamic Model, and Growing Degree Hours. It is important to use the `make_JDay()` function to add Julian dates (which count the days of the year) to the dataset, ensuring proper functionality.


``` r
chill_output <- chilling(make_JDay(Winters_hours_gaps), Start_JDay = 90, End_JDay = 100)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Season </th>
   <th style="text-align:center;"> End_year </th>
   <th style="text-align:center;"> Season_days </th>
   <th style="text-align:center;"> Data_days </th>
   <th style="text-align:center;"> Perc_complete </th>
   <th style="text-align:center;"> Chilling_Hours </th>
   <th style="text-align:center;"> Utah_Model </th>
   <th style="text-align:center;"> Chill_portions </th>
   <th style="text-align:center;"> GDH </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 100 </td>
   <td style="text-align:center;"> 40 </td>
   <td style="text-align:center;"> 15.5 </td>
   <td style="text-align:center;"> 2.009147 </td>
   <td style="text-align:center;"> 2406.52 </td>
  </tr>
</tbody>
</table></div>

However, there may be instances where not all metrics are desired, or there is a need for different metrics altogether. In such cases, the `tempResponse` function can be employed. This function is similar to `chilling()` but offers the flexibility to take a list of specific temperature models to be computed as input.


``` r
chill_output <- tempResponse(make_JDay(Winters_hours_gaps), 
                       Start_JDay = 90, 
                       End_JDay = 100, 
                       models = list(Chill_Portions = Dynamic_Model, GDH = GDH))
```

<table class="table table-striped table-hover table-responsive" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Season </th>
   <th style="text-align:center;"> End_year </th>
   <th style="text-align:center;"> Season_days </th>
   <th style="text-align:center;"> Data_days </th>
   <th style="text-align:center;"> Perc_complete </th>
   <th style="text-align:center;"> Chill_Portions </th>
   <th style="text-align:center;"> GDH </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 100 </td>
   <td style="text-align:center;"> 2.009147 </td>
   <td style="text-align:center;"> 2406.52 </td>
  </tr>
</tbody>
</table>

This will return only the Dynamic Model and Growing Degree Hours (GDH**)** values for the specified period.

## `Exercises` on chill models

1.  *Run the* `chilling()` *function on the* `Winters_hours_gap` *dataset.*


``` r
august <- chilling(make_JDay(Winters_hours_gaps), Start_JDay = 214, End_JDay = 244)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; "><table class="table table-striped table-hover table-responsive" style="font-size: 14px; color: black; width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Season </th>
   <th style="text-align:center;"> End_year </th>
   <th style="text-align:center;"> Season_days </th>
   <th style="text-align:center;"> Data_days </th>
   <th style="text-align:center;"> Perc_complete </th>
   <th style="text-align:center;"> Chilling_Hours </th>
   <th style="text-align:center;"> Utah_Model </th>
   <th style="text-align:center;"> Chill_portions </th>
   <th style="text-align:center;"> GDH </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 31 </td>
   <td style="text-align:center;"> 31 </td>
   <td style="text-align:center;"> 100 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> -569.5 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 9933.327 </td>
  </tr>
</tbody>
</table></div>

2.  *Create your own temperature-weighting chill model using the* `step_model()` *function.*


``` r
df <- data.frame(
  lower = c(-1000, 0,  5, 10, 15, 20,   25),  
  upper = c(    0, 5, 10, 15, 20, 25, 1000), 
  weight = c(   0, 1,  2,  3,  2,  1,    0))

custom <- function(x) step_model(x, df)
```

<table class="table table-striped table-hover" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> lower </th>
   <th style="text-align:center;"> upper </th>
   <th style="text-align:center;"> weight </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> -1000 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 3 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 25 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 25 </td>
   <td style="text-align:center;"> 1000 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
</tbody>
</table>

3.  *Run this model on the* `Winters_hours_gaps` *dataset using the* `tempResponse()` *function.*


``` r
models <- list(
  Chilling_Hours = Chilling_Hours,
  Utah_Chill_Units = Utah_Model,
  Chill_Portions = Dynamic_Model,
  GDH = GDH,
  custom = custom)

result <- tempResponse(make_JDay(Winters_hours_gaps), 
                       Start_JDay = 214, 
                       End_JDay = 244, 
                       models)
```

<div style="border: 1px solid #ddd; padding: 5px; overflow-x: scroll; width:100%; "><table class="table table-striped table-hover table-responsive" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Season </th>
   <th style="text-align:center;"> End_year </th>
   <th style="text-align:center;"> Season_days </th>
   <th style="text-align:center;"> Data_days </th>
   <th style="text-align:center;"> Perc_complete </th>
   <th style="text-align:center;"> Chilling_Hours </th>
   <th style="text-align:center;"> Utah_Chill_Units </th>
   <th style="text-align:center;"> Chill_Portions </th>
   <th style="text-align:center;"> GDH </th>
   <th style="text-align:center;"> custom </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 31 </td>
   <td style="text-align:center;"> 31 </td>
   <td style="text-align:center;"> 100 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> -569.5 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 9933.327 </td>
   <td style="text-align:center;"> 838 </td>
  </tr>
</tbody>
</table></div>

<!--chapter:end:07-chill.Rmd-->

# Making hourly temperatures

## Learning goals

-   Understand why we often need hourly temperature data and why we need ways of making them out of daily data
-   Understand some basic algorithms for making hourly data from daily minimum and maximum temperatures
-   Understand how we can make use of observed hourly temperatures to produce our own empirical transfer function that can make hourly from daily data
-   Be able to use the respective `chillR` functions that implement these steps

## Generating hourly temperatures

With the Chilling Hours function developed, the next challenge arises from the limited availability of hourly temperature data, as most sources provide only daily minimum and maximum temperatures. This limitation complicates the direct calculation of Chilling Hours. Various methods have been employed to address this issue, including relating Chilling Hours to minimum temperatures (Crossa-Raynaud, 1955) or using complex equations.

With better computing tools, some researchers started to assume that daily minimum and maximum temperatures occur at specific times and used linear interpolation for the hours in between, creating a triangular shape for daily temperature patterns ([Baldocchi & Wong, 2008](https://link.springer.com/article/10.1007/s10584-007-9367-8)).

<img src="bookdownproj_files/figure-html/triangular-1.png" width="80%" height="50%" />

While assuming a triangular temperature pattern may serve as a rough approximation, it is not entirely realistic. The rate of temperature increase in the morning differs from the rate of decrease in the evening. Additionally, the timing of the lowest daily temperature varies significantly throughout the year, particularly outside of equatorial regions. Therefore, it is important to take these variations into account.

## Idealized daily temperature curves

A major breakthrough in modeling daily temperature curves was made when [Dale E. Linvill](https://journals.ashs.org/hortsci/view/journals/hortsci/25/1/article-p14.xml) from Clemson University published a paper in 1990. He combined two mathematical equations: a sine curve to represent warming during the day and a logarithmic decay function for cooling at night. The times for sunrise and sunset defined the transition between these phases, and the length of each phase was linked to the amount of daylight. This method allowed for more accurate daily temperature curves than previous approaches, but not all researchers adopted these equations due to a lack of awareness or data processing skills.

One challenge with Linvill's equations was their dependence on local sunrise and sunset times. While these can be calculated from observations, having a general method would help researchers. Fortunately, for areas without major geographical features, sunrise and sunset times can be calculated based on solar system geometry. Although agricultural scientists may not be familiar with this, they can use insights from other fields. The `chillR` package uses equations from [Spencer (1971)](https://www.mail-archive.com/sundial@uni-koeln.de/msg01050.html) and [Almorox et al. (2005)](https://www.sciencedirect.com/science/article/abs/pii/S0196890404001992). [Prof. Dr. Eike Lüdeling](https://inresgb-lehre.iaas.uni-bonn.de/author/prof.-dr.-eike-luedeling/) only needed to understand these equations once to code them into an R function for future use.

Bringing together these functions is similar to how the `CH()` function was developed and used in the `sum_CH` function, though the components were more complex. The result is a function that can create realistic daily temperature curves based on the latitude of a location. The provided code illustrates how to use the `daylength` function to create plots showing sunrise time, sunset time, and daylength for Klein-Altendorf (Latitude: 50.4°N) throughout the year:




``` r
Days <- daylength(latitude = 50.4, JDay = 1:365)
Days_df <-
  data.frame(
    JDay = 1:365,
    Sunrise = Days$Sunrise,
    Sunset = Days$Sunset,
    Daylength = Days$Daylength
  )
Days_df <- pivot_longer(Days_df, cols = c(Sunrise:Daylength))

ggplot(Days_df, aes(JDay, value)) +
  geom_line(lwd = 1.5) +
  facet_grid(cols = vars(name)) +
  ylab("Time of Day / Daylength (Hours)") +
  theme_bw(base_size = 15)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-94-1.png" width="672" />

In this context, JDay refers to the Julian Date, which represents the Day of the Year. For example, January 1st is JDay 1, while December 31st is JDay 365 in regular years and JDay 366 in leap years. The `ggplot2` package is used for creating attractive plots, and the ideal input for it is a data frame. Therefore, the outputs from the `daylength()` function were first converted into a data frame. Additionally, the three time series - Sunrise, Sunset, and Daylength - were organized into a stacked format using the `pivot_longer` command from the `tidyr` package.

The `stack_hourly_temps()` function in the `chillR` package integrates these daily dynamics. This function requires a dataset containing daily minimum and maximum temperatures, specifically with columns labeled `Tmin`, `Tmax`, `Year`, `Month`, and `Day`. The latitude of the location must also be provided. Using these inputs, the function applies the previously discussed equations to calculate hourly temperatures, and it can also output sunrise and sunset times if desired.

To demonstrate this process, another dataset included with `chillR`, called `KA_weather`, will be used. This data frame contains temperature data from the University of Bonn’s experimental station at Klein-Altendorf. The first 10 rows of the `KA_weather` dataset will be shown for illustration:

<table class="table table-striped table-hover" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Tmax </th>
   <th style="text-align:center;"> Tmin </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 8.2 </td>
   <td style="text-align:center;"> 5.1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 9.1 </td>
   <td style="text-align:center;"> 5.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 10.4 </td>
   <td style="text-align:center;"> 3.3 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 8.4 </td>
   <td style="text-align:center;"> 4.5 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 12.0 </td>
   <td style="text-align:center;"> 6.9 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 11.2 </td>
   <td style="text-align:center;"> 8.6 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 13.9 </td>
   <td style="text-align:center;"> 8.5 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 14.5 </td>
   <td style="text-align:center;"> 3.6 </td>
  </tr>
</tbody>
</table>

The following process describes how hourly temperatures can be calculated based on the idealized daily temperature curve:


``` r
stack_hourly_temps(KA_weather, latitude = 50.4)
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Tmax </th>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> JDay </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Temp </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 4.844164 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 4.746566 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 4.656244 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 4.572187 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 4.493583 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 4.569464 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 5.384001 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 6.139939 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 6.787169 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 7.282787 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 7.593939 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 7.700000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 7.593939 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 7.282787 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 6.591821 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 6.168074 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 5.870570 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 5.641106 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 21 </td>
   <td style="text-align:center;"> 5.454280 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 22 </td>
   <td style="text-align:center;"> 5.296704 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 7.7 </td>
   <td style="text-align:center;"> 4.5 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 23 </td>
   <td style="text-align:center;"> 5.160445 </td>
  </tr>
</tbody>
</table>

And here’s a plot of the data:

<img src="bookdownproj_files/figure-html/idealized-1.png" width="80%" height="50%" />

## Empirical daily temperature curves

In some locations, idealized daily temperature curves are ineffective, particularly in areas with rugged topography where temperate fruit trees may be shaded for part of the day. For example, in the Jabal Al Akhdar region of Oman, where [Prof. Dr. Eike Lüdeling](https://inresgb-lehre.iaas.uni-bonn.de/author/prof.-dr.-eike-luedeling/) initially studied winter chill, various oases in the deeply incised Wadi Muaydin canyon were investigated. Trees near the top of the canyon receive significantly more sunlight than those at the bottom, which is about 1000 meters lower.

![**Terraced oasis fields at Ash Sharayjah**](images/IMG_8487.jpg)

Even in the absence of mountains, the temperature curve in an orchard may not closely resemble the curve proposed by [Linvill (1990)](https://journals.ashs.org/hortsci/view/journals/hortsci/25/1/article-p14.xml) due to its unique microclimate, featuring shaded and sunny spots, dew-covered grass, and bare ground.

In the initial study on Omani oases ([Luedeling et al., 2009b](https://link.springer.com/article/10.1007/s10584-009-9581-7)), this issue was not adequately addressed. However, a recent revisit to the location aimed to improve this aspect ([Buerkert et al., 2020](https://link.springer.com/article/10.1007/s10584-020-02862-8)).

To analyze the temperature patterns, a dataset of hourly temperature data for the relevant location is needed, ideally covering an entire year or multiple years. For this exercise, the `Winters_hours_gaps` dataset from a walnut orchard near Winters, California, will be used, as the temperature logger was directly attached to a tree branch, making it unlikely for the data to exactly match the standard daily temperature curve.

The `Empirical_daily_temperature_curve()` function will be employed to determine the typical hourly temperature patterns for each month of the year, although this method could potentially be enhanced by allowing for continuous analysis instead of monthly breakdowns.


``` r
empi_curve <- Empirical_daily_temperature_curve(Winters_hours_gaps)
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Prediction_coefficient </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0.1774859 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 0.1550693 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 0.1285651 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 0.1145597 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 0.0696064 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 0.0339583 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 0.0313115 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 0.3121959 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 0.4953232 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 0.6819674 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 0.8227423 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 0.9506491 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 0.9662604 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 0.9915996 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 1.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 0.9490319 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 0.8483098 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 0.6864529 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 0.4945415 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 0.3636642 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 21 </td>
   <td style="text-align:center;"> 0.2972377 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 22 </td>
   <td style="text-align:center;"> 0.2360349 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 23 </td>
   <td style="text-align:center;"> 0.1794802 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0.1960789 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 0.1407018 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 0.1283250 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 0.0819307 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 0.0541415 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 0.0188241 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 0.1697052 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 0.4442722 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 0.5939797 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 0.7363923 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 0.8399804 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 0.9245702 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 0.9770693 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 0.9963131 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 1.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 0.9568107 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 0.8698369 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 0.7343896 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 0.5330597 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 0.3941038 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 21 </td>
   <td style="text-align:center;"> 0.3186075 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 22 </td>
   <td style="text-align:center;"> 0.2594569 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 23 </td>
   <td style="text-align:center;"> 0.2114486 </td>
  </tr>
</tbody>
</table>


``` r
ggplot(data = empi_curve[1:96, ], aes(Hour, Prediction_coefficient)) +
  geom_line(lwd = 1.3, 
            col = "red") + 
  facet_grid(rows = vars(Month)) + 
  xlab("Hour of the day") +
  ylab("Prediction coefficient") +
  theme_bw(base_size = 15)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-100-1.png" width="672" />

The set of coefficients can now be applied to a daily dataset from the same location, allowing for the creation of a reasonable hourly temperature record for the orchard. This is accomplished using the `Empirical_hourly_temperatures` function, which requires a set of hourly coefficients and a daily temperature record that includes `Tmin` and `Tmax` columns.

Additionally, the `?` operator can be used to access help on how to use any function, such as `?Empirical_hourly_temperatures`.

The process also involves using the `make_all_day_table` function, which fills gaps in daily or hourly temperature records and summarizes hourly data into daily minimum and maximum temperatures.


``` r
coeffs <- Empirical_daily_temperature_curve(Winters_hours_gaps)
Winters_daily <-
  make_all_day_table(Winters_hours_gaps, input_timestep = "hour")
Winters_hours <- Empirical_hourly_temperatures(Winters_daily, coeffs)
```

The next step is to plot the results to visualize the hourly temperature data. This allows for a comparison between the results from the empirical method, the triangular function, and the idealized temperature curve. Additionally, actual observed temperatures will be used to validate the results. To facilitate this process, the data will first be simplified for easier handling:


``` r
Winters_hours <- Winters_hours[, c("Year", "Month", "Day", "Hour", "Temp")]
colnames(Winters_hours)[ncol(Winters_hours)] <- "Temp_empirical"
Winters_ideal <-
  stack_hourly_temps(Winters_daily, latitude = 38.5)$hourtemps
Winters_ideal <- Winters_ideal[, c("Year", "Month", "Day", "Hour", "Temp")]
colnames(Winters_ideal)[ncol(Winters_ideal)] <- "Temp_ideal"
```

The next step involves creating the 'triangular' dataset. Understanding the process behind this construction is essential.


``` r
Winters_triangle <- Winters_daily
Winters_triangle[, "Hour"] <- 0
Winters_triangle$Hour[nrow(Winters_triangle)] <- 23
Winters_triangle[, "Temp"] <- 0
Winters_triangle <-
  make_all_day_table(Winters_triangle, timestep = "hour")
colnames(Winters_triangle)[ncol(Winters_triangle)] <-
  "Temp_triangular"

# with the following loop, we fill in the daily Tmin and Tmax values for every
# hour of the dataset

for (i in 2:nrow(Winters_triangle))
{
  if (is.na(Winters_triangle$Tmin[i]))
    Winters_triangle$Tmin[i] <- Winters_triangle$Tmin[i - 1]
  if (is.na(Winters_triangle$Tmax[i]))
    Winters_triangle$Tmax[i] <- Winters_triangle$Tmax[i - 1]
}
Winters_triangle$Temp_triangular <- NA

# now we assign the daily Tmin value to the 6th hour of every day

Winters_triangle$Temp_triangular[which(Winters_triangle$Hour == 6)] <-
  Winters_triangle$Tmin[which(Winters_triangle$Hour == 6)]

# we also assign the daily Tmax value to the 18th hour of every day

Winters_triangle$Temp_triangular[which(Winters_triangle$Hour == 18)] <-
  Winters_triangle$Tmax[which(Winters_triangle$Hour == 18)]

# in the following step, we use the chillR function "interpolate_gaps"
# to fill in all the gaps in the hourly record with straight lines

Winters_triangle$Temp_triangular <-
  interpolate_gaps(Winters_triangle$Temp_triangular)$interp
Winters_triangle <-
  Winters_triangle[, c("Year", "Month", "Day", "Hour", "Temp_triangular")]
```

The next step is to merge all the data frames to facilitate easier display and comparison of the datasets.


``` r
Winters_temps <-
  merge(Winters_hours_gaps,
        Winters_hours,
        by = c("Year", "Month", "Day", "Hour"))
Winters_temps <-
  merge(Winters_temps,
        Winters_triangle,
        by = c("Year", "Month", "Day", "Hour"))
Winters_temps <-
  merge(Winters_temps,
        Winters_ideal,
        by = c("Year", "Month", "Day", "Hour"))
```

The dataset now includes observed temperatures along with the three approximations: triangular, idealized curve, and empirical curve. To plot this data effectively, the `Year`, `Month`, `Day`, and `Hour` columns will be converted into R's date format using `ISOdate`, and the data frame will be reorganized for better usability.


``` r
Winters_temps[, "DATE"] <-
  ISOdate(Winters_temps$Year,
          Winters_temps$Month,
          Winters_temps$Day,
          Winters_temps$Hour)


Winters_temps_to_plot <-
  Winters_temps[, c("DATE",
                    "Temp",
                    "Temp_empirical",
                    "Temp_triangular",
                    "Temp_ideal")]
Winters_temps_to_plot <- Winters_temps_to_plot[100:200, ]
Winters_temps_to_plot <- pivot_longer(Winters_temps_to_plot, cols=Temp:Temp_ideal)
colnames(Winters_temps_to_plot) <- c("DATE", "Method", "Temperature")


ggplot(data = Winters_temps_to_plot, aes(DATE, Temperature, colour = Method)) +
  geom_line(lwd = 1.3) + ylab("Temperature (°C)") + xlab("Date")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-105-1.png" width="672" />

The plot indicates that the triangular curve deviates significantly from the observed data, while the `Temp_empirical` and `Temp_ideal` curves appear quite similar and are difficult to differentiate.

To compare these curves more thoroughly, the Root Mean Square Error (RMSE) can be calculated, as it is useful for quantifying the alignment between predicted and observed values. The `chillR` package includes a function to perform this calculation.


``` r
# here's the RMSE for the triangular method:
RMSEP(Winters_temps$Temp_triangular, Winters_temps$Temp)
```

```
## [1] 4.695289
```


``` r
# here's the RMSE for the idealized-curve method:
RMSEP(Winters_temps$Temp_ideal, Winters_temps$Temp)
```

```
## [1] 1.630714
```


``` r
# and here's the RMSE for the empirical-curve method:
RMSEP(Winters_temps$Temp_empirical, Winters_temps$Temp)
```

```
## [1] 1.410625
```

The results show an RMSE of 4.7 for the triangular method, 1.63 for the idealized curve method, and 1.41 for the empirical curve method. Since a lower RMSE indicates better accuracy, these results demonstrate that calibrating the prediction function with observed hourly data significantly improves accuracy, especially compared to the triangular method.

While it might be questioned how much this affects chill accumulation modeling, it is often found to make a considerable difference.

## `Exercises` on hourly temperatures

1.  *Choose a location of interest, find out its latitude and produce plots of daily sunrise, sunset and daylength.*

The Yakima Valley in Washington State, USA, is located at about 46.6° N latitude. This region has a continental climate with cold winters and hot, dry summers, creating ideal conditions for growing fruit trees. The valley is well known for producing a variety of fruits, including apples, cherries, pears, and grapes, which benefit from its distinct seasonal changes. Using the `daylength()` function, you could create plots showing daily sunrise, sunset, and day length times.




``` r
Yakima <- daylength(latitude = 46.6, JDay = 1:365)

Yakima_df <-
  data.frame(
    JDay = 1:365,
    Sunrise = Yakima$Sunrise,
    Sunset = Yakima$Sunset,
    Daylength = Yakima$Daylength
  )

Yakima_df_longer <- pivot_longer(Yakima_df, cols = c(Sunrise:Daylength))

ggplot(Yakima_df_longer, aes(JDay, value)) +
  geom_line(lwd = 1.5) +
  facet_grid(cols = vars(name)) +
  ylab("Time of Day / Daylength (Hours)") +
  theme_bw(base_size = 15)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-110-1.png" width="672" />

2.  *Produce an hourly dataset, based on idealized daily curves, for the* `KA_weather` *dataset* *(included in* `chillR`*)*


``` r
KA_hourly <- stack_hourly_temps(KA_weather, latitude = 50.4)
```

Based on idealized daily curves, the hourly dataset for Julian Day 6 (January 6th) is shown below:

<table class="table table-striped" style="font-size: 15px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Tmax </th>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> JDay </th>
   <th style="text-align:center;"> Hour </th>
   <th style="text-align:center;"> Temp </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 4.990741 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 4.881232 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 4.782253 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 4.691956 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 4.608939 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 4.532117 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 4.460628 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 4.393780 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 4.491337 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 5.430950 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 6.302486 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 7.048391 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 7.619410 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> 7.977836 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> 8.100000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 7.977836 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 7.619410 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 7.419674 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> 7.318918 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> 7.248287 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> 7.193854 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 21 </td>
   <td style="text-align:center;"> 7.149557 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 22 </td>
   <td style="text-align:center;"> 7.112208 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 8.1 </td>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 23 </td>
   <td style="text-align:center;"> 7.079920 </td>
  </tr>
</tbody>
</table>

3.  *Produce empirical temperature curve parameters for the* `Winters_hours_gaps` *dataset, and use them to predict hourly values from daily temperatures (this is very similar to the example above, but please make sure you understand what’s going on).*

-   Generating empirical daily temperature curve from observed hourly data:


``` r
empi_curve <- Empirical_daily_temperature_curve(Winters_hours_gaps)
```

-   Filling gaps in daily or hourly temperature data:


``` r
Winters_daily <- make_all_day_table(Winters_hours_gaps, input_timestep = "hour")
```

-   Using empirical coefficients to predict hourly temperatures based on daily temperatures:


``` r
Winters_hours <- Empirical_hourly_temperatures(Winters_daily, empi_curve)
```


``` r
Winters_hours <- Winters_hours[, c("Year", "Month", "Day", "Hour", "Temp")]
colnames(Winters_hours)[ncol(Winters_hours)] <- "Temp_empirical"
```


``` r
Winters_temps <-
  merge(Winters_hours_gaps,
        Winters_hours,
        by = c("Year", "Month", "Day", "Hour"))
```


``` r
Winters_temps[, "DATE"] <-
  ISOdate(Winters_temps$Year,
          Winters_temps$Month,
          Winters_temps$Day,
          Winters_temps$Hour)

Winters_temps_to_plot <-
  Winters_temps[, c("DATE",
                    "Temp",
                    "Temp_empirical")]
Winters_temps_to_plot <- Winters_temps_to_plot[100:200, ]
Winters_temps_to_plot <- pivot_longer(Winters_temps_to_plot, cols=Temp:Temp_empirical)
colnames(Winters_temps_to_plot) <- c("DATE", "Method", "Temperature")

ggplot(data = Winters_temps_to_plot, aes(DATE, Temperature, colour = Method)) +
  geom_line(lwd = 1.3) + ylab("Temperature (°C)") + xlab("Date")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-118-1.png" width="672" />

<!--chapter:end:08-making-temp.Rmd-->

# Some useful tools in R

## Learning goals

-   Get to know some neat tools in R that can make coding more elegant - and easier
-   Get introduced to the `tidyverse`
-   Learn about loops
-   Get to know the `apply` function family

## An evolving language - and a lifelong learning process

The R universe is constantly evolving, offering much more now than the original base functions. Over time, modern tools and more elegant programming styles have become integral. In the upcoming chapters, some of these new tools will be introduced, along with the basics needed to use them effectively.

## The `tidyverse`

Many of the tools introduced here come from the `tidyverse` - a collection of packages developed by [Hadley Wickham](https://en.wikipedia.org/wiki/Hadley_Wickham) and his team. This collection offers many ways to improve programming skills. In this book, only the functions that are directly used will be covered. A big advantage of the tidyverse is that, with just one command - `library(tidyverse)` - all functions in the package collection become available.

## The `ggplot2` package

The `ggplot2` package, first released by [Hadley Wickham](https://en.wikipedia.org/wiki/Hadley_Wickham) in 2007, has become one of the most popular R packages because it greatly simplifies the creation of attractive graphics. The history of the package can be found [here](https://en.wikipedia.org/wiki/Ggplot2), and an introduction along with links to various tutorials is available [here](https://ggplot2.tidyverse.org/).

## The `tibble` package

A `tibble` is an enhanced version of a `data.frame` that offers several improvements. The most notable improvement is that `tibbles` avoid the common `data.frame` behavior of unexpectedly converting strings into factors. Although `tibbles` are relatively new here, they will be used throughout the rest of the book.

To create a `tibble` from a regular `data.frame` (or a similar structure), the `as_tibble` command can be used:




``` r
dat <- data.frame(a = c(1, 2, 3), b = c(4, 5, 6))
d <- as_tibble(dat)
d
```

```
## # A tibble: 3 × 2
##       a     b
##   <dbl> <dbl>
## 1     1     4
## 2     2     5
## 3     3     6
```

## The `magrittr` package - pipes

`Magrittr` helps organize steps applied to the same dataset by using the pipe operator `%>%`. This operator links multiple operations on a data structure, such as a `tlibbe`, making it easier to perform tasks like calculating the sum of all numbers in the dataset:


``` r
d %>% sum()
```

```
## [1] 21
```

After the pipe operator `%>%`, the next function automatically takes the piped-in data as its first input, so it’s unnecessary to specify it explicitly. Additional commands can be chained by adding more pipes. This approach allows for building more complex workflows, as shown in examples later.

## The `tidyr` package

The `tidyr` package offers helpful functions for organizing data. The `KA_weather` dataset from `chillR` will be used here to illustrate some of these functions:




``` r
KAw <- as_tibble(KA_weather[1:10,])
KAw
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1     1   8.2   5.1
##  2  1998     1     2   9.1   5  
##  3  1998     1     3  10.4   3.3
##  4  1998     1     4   8.4   4.5
##  5  1998     1     5   7.7   4.5
##  6  1998     1     6   8.1   4.4
##  7  1998     1     7  12     6.9
##  8  1998     1     8  11.2   8.6
##  9  1998     1     9  13.9   8.5
## 10  1998     1    10  14.5   3.6
```

### `pivot_longer`

The `pivot_longer` function, introduced previously, is useful for reshaping data from separate columns (like `Tmin` and `Tmax`) into individual rows. In this setup, each day’s record will have a row for `Tmin` and another for `Tmax`. This transformation is often necessary for tasks like plotting data with the `ggplot2` package. The function can be combined with a pipe for a streamlined workflow:


``` r
KAwlong <- KAw %>% pivot_longer(cols = Tmax:Tmin)
KAwlong
```

```
## # A tibble: 20 × 5
##     Year Month   Day name  value
##    <int> <int> <int> <chr> <dbl>
##  1  1998     1     1 Tmax    8.2
##  2  1998     1     1 Tmin    5.1
##  3  1998     1     2 Tmax    9.1
##  4  1998     1     2 Tmin    5  
##  5  1998     1     3 Tmax   10.4
##  6  1998     1     3 Tmin    3.3
##  7  1998     1     4 Tmax    8.4
##  8  1998     1     4 Tmin    4.5
##  9  1998     1     5 Tmax    7.7
## 10  1998     1     5 Tmin    4.5
## 11  1998     1     6 Tmax    8.1
## 12  1998     1     6 Tmin    4.4
## 13  1998     1     7 Tmax   12  
## 14  1998     1     7 Tmin    6.9
## 15  1998     1     8 Tmax   11.2
## 16  1998     1     8 Tmin    8.6
## 17  1998     1     9 Tmax   13.9
## 18  1998     1     9 Tmin    8.5
## 19  1998     1    10 Tmax   14.5
## 20  1998     1    10 Tmin    3.6
```

In this example, it was necessary to specify the columns to stack. The `pivot_longer` function serves a similar purpose to the `melt` function from the `reshape2` package, which was used previously and in earlier book editions. However, `pivot_longer` is more intuitive, so it will be used throughout the remaining chapters.

### `pivot_wider`

The `pivot_wider` function allows for the opposite transformation of `pivot_longer`, converting rows back into separate columns:


``` r
KAwwide <- KAwlong %>% pivot_wider(names_from = name) 
KAwwide
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1     1   8.2   5.1
##  2  1998     1     2   9.1   5  
##  3  1998     1     3  10.4   3.3
##  4  1998     1     4   8.4   4.5
##  5  1998     1     5   7.7   4.5
##  6  1998     1     6   8.1   4.4
##  7  1998     1     7  12     6.9
##  8  1998     1     8  11.2   8.6
##  9  1998     1     9  13.9   8.5
## 10  1998     1    10  14.5   3.6
```

The `names_from` argument in `pivot_wider` specifies the column that will provide the headers for the new columns. In some cases, `pivot_wider` might work without this argument, but it’s generally recommended to include it for clarity and to ensure that the function behaves as expected, especially with more complex datasets.

### `select`

The `select` function allows users to choose a subset of columns from a `data.frame` or `tibble`:


``` r
KAw %>% select(c(Month, Day, Tmax))
```

```
## # A tibble: 10 × 3
##    Month   Day  Tmax
##    <int> <int> <dbl>
##  1     1     1   8.2
##  2     1     2   9.1
##  3     1     3  10.4
##  4     1     4   8.4
##  5     1     5   7.7
##  6     1     6   8.1
##  7     1     7  12  
##  8     1     8  11.2
##  9     1     9  13.9
## 10     1    10  14.5
```

### `filter`

The `filter` function reduces a `data.frame` or `tibble` to just the rows that fulfill certain conditions:


``` r
KAw %>% filter(Tmax > 10)
```

```
## # A tibble: 5 × 5
##    Year Month   Day  Tmax  Tmin
##   <int> <int> <int> <dbl> <dbl>
## 1  1998     1     3  10.4   3.3
## 2  1998     1     7  12     6.9
## 3  1998     1     8  11.2   8.6
## 4  1998     1     9  13.9   8.5
## 5  1998     1    10  14.5   3.6
```

### `mutate`

The `mutate` function is essential for creating, modifying, and deleting columns in a `data.frame` or `tibble`. For example, it can be used to add new columns, such as converting `Tmin` and `Tmax` to Kelvin:


``` r
KAw_K <- KAw %>% mutate(Tmax_K = Tmax + 273.15, Tmin_K = Tmin + 273.15)
KAw_K
```

```
## # A tibble: 10 × 7
##     Year Month   Day  Tmax  Tmin Tmax_K Tmin_K
##    <int> <int> <int> <dbl> <dbl>  <dbl>  <dbl>
##  1  1998     1     1   8.2   5.1   281.   278.
##  2  1998     1     2   9.1   5     282.   278.
##  3  1998     1     3  10.4   3.3   284.   276.
##  4  1998     1     4   8.4   4.5   282.   278.
##  5  1998     1     5   7.7   4.5   281.   278.
##  6  1998     1     6   8.1   4.4   281.   278.
##  7  1998     1     7  12     6.9   285.   280.
##  8  1998     1     8  11.2   8.6   284.   282.
##  9  1998     1     9  13.9   8.5   287.   282.
## 10  1998     1    10  14.5   3.6   288.   277.
```

To delete the columns created with `mutate`, you can set them to `NULL`. This effectively removes the specified columns from the `data.frame` or `tibble`:


``` r
KAw_K %>% mutate(Tmin_K = NULL, Tmax_K = NULL)
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1     1   8.2   5.1
##  2  1998     1     2   9.1   5  
##  3  1998     1     3  10.4   3.3
##  4  1998     1     4   8.4   4.5
##  5  1998     1     5   7.7   4.5
##  6  1998     1     6   8.1   4.4
##  7  1998     1     7  12     6.9
##  8  1998     1     8  11.2   8.6
##  9  1998     1     9  13.9   8.5
## 10  1998     1    10  14.5   3.6
```

Next, the original temperature values will be replaced directly with their corresponding Kelvin values. The following code will make these modifications to the specified columns:


``` r
KAw %>% mutate(Tmin = Tmin + 273.15, Tmax = Tmax + 273.15)
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1     1  281.  278.
##  2  1998     1     2  282.  278.
##  3  1998     1     3  284.  276.
##  4  1998     1     4  282.  278.
##  5  1998     1     5  281.  278.
##  6  1998     1     6  281.  278.
##  7  1998     1     7  285.  280.
##  8  1998     1     8  284.  282.
##  9  1998     1     9  287.  282.
## 10  1998     1    10  288.  277.
```

### `arrange`

`arrange` is a function to sort data in `data.frames` or `tibbles`:


``` r
KAw %>% arrange(Tmax, Tmin)
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1     5   7.7   4.5
##  2  1998     1     6   8.1   4.4
##  3  1998     1     1   8.2   5.1
##  4  1998     1     4   8.4   4.5
##  5  1998     1     2   9.1   5  
##  6  1998     1     3  10.4   3.3
##  7  1998     1     8  11.2   8.6
##  8  1998     1     7  12     6.9
##  9  1998     1     9  13.9   8.5
## 10  1998     1    10  14.5   3.6
```

It is also possible to sort a `data.frame` or `tibble` in descending order:


``` r
KAw %>% arrange(desc(Tmax), Tmin)
```

```
## # A tibble: 10 × 5
##     Year Month   Day  Tmax  Tmin
##    <int> <int> <int> <dbl> <dbl>
##  1  1998     1    10  14.5   3.6
##  2  1998     1     9  13.9   8.5
##  3  1998     1     7  12     6.9
##  4  1998     1     8  11.2   8.6
##  5  1998     1     3  10.4   3.3
##  6  1998     1     2   9.1   5  
##  7  1998     1     4   8.4   4.5
##  8  1998     1     1   8.2   5.1
##  9  1998     1     6   8.1   4.4
## 10  1998     1     5   7.7   4.5
```

## Loops

In addition to the `tidyverse` functions, understanding loops is essential for efficient coding. Loops enable the repetition of operations multiple times without needing to retype or copy and paste code. They also allow for modifications to be made with each iteration. While detailed explanations on loops can be found elsewhere, the basics will be covered here.

There are two primary types of loops: **for loops** and **while loops**. For both types, it is necessary to provide instructions that determine how many times the loop will run, as well as what actions to perform during each iteration.

### *For* loops

In a for loop, explicit instructions dictate how many times the code inside the loop should be executed. This is typically done by providing a vector or list of elements, directing R to run the code for each of these elements. As a result, the number of executions corresponds to the number of elements in the vector or list. A counter is needed to track the current iteration, commonly referred to as `i`, though it can be any variable name:


``` r
for (i in 1:3) print("Hello")
```

```
## [1] "Hello"
## [1] "Hello"
## [1] "Hello"
```

This command executed the code three times, producing the same output with each iteration. The structure can be made more complex by including multiple lines of code within curly brackets:


``` r
addition <- 1

for (i in 1:3)
{
  addition <- addition + 1
  print(addition)
}
```

```
## [1] 2
## [1] 3
## [1] 4
```

The code in this loop incremented an initial value of 1 by 1 in each iteration and printed the resulting value. It is important to note that R may require explicit instructions to `print` these values when the operation is embedded within a loop.

By utilizing the index `i` within the code block, additional flexibility can be introduced to the operations performed in each iteration:


``` r
addition <- 1

for (i in 1:3)
{
  addition <- addition + i
  print(addition)
}
```

```
## [1] 2
## [1] 4
## [1] 7
```

In this iteration, the respective value of `i` was added to the initial element during each run. Additionally, `i` can be utilized in more creative ways within the loop to enhance the operations being performed:


``` r
names <- c("Paul", "Mary", "John")

for (i in 1:3)
{
  print(paste("Hello", names[i]))
}
```

```
## [1] "Hello Paul"
## [1] "Hello Mary"
## [1] "Hello John"
```

The counter in a loop does not have to be numeric; it can take on various forms, including strings. By using this flexibility, the same output as generated in the previous code block can be achieved with a different formulation:


``` r
for (i in c("Paul", "Mary", "John"))
{
  print(paste("Hello", i))
}
```

```
## [1] "Hello Paul"
## [1] "Hello Mary"
## [1] "Hello John"
```

### *While* loops

A loop can also be controlled using a `while` statement, which executes the code until a specified condition is no longer met. This approach is meaningful only if the condition can change based on the operations performed within the loop:


``` r
cond <- 5

while (cond > 0)
{
  print(cond)
  cond <- cond - 1
}
```

```
## [1] 5
## [1] 4
## [1] 3
## [1] 2
## [1] 1
```

Once `cond` reaches 0, the starting condition is no longer satisfied, and the code will not execute again. It is important to note that while loops can lead to issues if the condition remains true regardless of the code block's execution. In such cases, the code may become stuck and will need to be manually interrupted.

## `apply` functions

In addition to loops, R offers a more efficient way to perform operations on multiple elements simultaneously. This method, which is often faster, utilizes functions from the **apply** family: `apply`, `lapply`, and `sapply`. These functions require two key arguments: the list of items to which the operation will be applied and the operation itself.

### `sapply`

When the goal is to apply an operation to a vector of elements, the simplest function to use is `sapply`. It requires two arguments: the vector (`X`) and the function to be applied (`FUN`). For illustration, a simple function called `func` will be created, which adds 1 to an input object:


``` r
func <- function(x)
  x + 1

sapply(1:5, func)
```

```
## [1] 2 3 4 5 6
```

The output is a vector of numbers that are each 1 greater than the corresponding elements of the input vector. When this function is applied to a list of numbers, the output becomes a matrix, although the values remain the same:


``` r
sapply(list(1:5), func)
```

```
##      [,1]
## [1,]    2
## [2,]    3
## [3,]    4
## [4,]    5
## [5,]    6
```

### `lapply`

To obtain a list as the output, the `lapply` function can be used. This function treats the input element `X` as a list and returns a new list containing the same number of elements as the input. Each element in the output list corresponds to the result of applying `FUN` to the respective element of the input list:


``` r
lapply(1:5, func)
```

```
## [[1]]
## [1] 2
## 
## [[2]]
## [1] 3
## 
## [[3]]
## [1] 4
## 
## [[4]]
## [1] 5
## 
## [[5]]
## [1] 6
```

If the input element `X` is a list, `lapply` treats the entire list as a single input element, applying `FUN` to the whole list and returning the result as one element in the output list. An example can help clarify this behavior:


``` r
lapply(list(1:5), func)
```

```
## [[1]]
## [1] 2 3 4 5 6
```

### `apply`

The basic `apply` function is designed for applying functions to arrays, allowing operations to be performed either on the rows (`MARGIN = 1`) or on the columns (`MARGIN = 2`) of the array. While this function may not be used frequently, here are some simple examples of its functionality. For further information, it is advisable to consult the help file or explore online resources, as there are many helpful materials available.


``` r
mat <- matrix(c(1, 1, 1, 2, 2, 2, 3, 3, 3), c(3, 3))
mat
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    1    2    3
## [3,]    1    2    3
```


``` r
apply(mat, MARGIN = 1, sum) # adding up all the data in each row
```

```
## [1] 6 6 6
```


``` r
apply(mat, MARGIN = 2, sum) # adding up all the data in each column
```

```
## [1] 3 6 9
```

## `Exercises` on useful R tools

1.  *Based on the* `Winters_hours_gaps` *dataset, use* `magrittr` *pipes and functions of the* `tidyverse` *to accomplish the following:*

-   

    a)  *Convert the dataset into a* `tibble`

-   

    b)  *Select only the top 10 rows of the dataset*




``` r
WHG <- as_tibble(Winters_hours_gaps[1:10, ])
WHG
```

```
## # A tibble: 10 × 6
##     Year Month   Day  Hour Temp_gaps  Temp
##    <int> <int> <int> <int>     <dbl> <dbl>
##  1  2008     3     3    10      15.1  15.1
##  2  2008     3     3    11      17.2  17.2
##  3  2008     3     3    12      18.7  18.7
##  4  2008     3     3    13      18.7  18.7
##  5  2008     3     3    14      18.8  18.8
##  6  2008     3     3    15      19.5  19.5
##  7  2008     3     3    16      19.3  19.3
##  8  2008     3     3    17      17.7  17.7
##  9  2008     3     3    18      15.4  15.4
## 10  2008     3     3    19      12.7  12.7
```

-   

    c)  *Convert the* `tibble` *to a* `long` *format, with separate rows for* `Temp_gaps` *and* `Temp`

To see the difference between the columns `Temp_gaps` and `Temp`, rows 279 to 302 (Julian Day 15) are used below:


``` r
WHG <- as_tibble(Winters_hours_gaps[279:302, ])
WHGlong <- WHG %>% pivot_longer(cols = Temp_gaps:Temp)
WHGlong
```

```
## # A tibble: 48 × 6
##     Year Month   Day  Hour name      value
##    <int> <int> <int> <int> <chr>     <dbl>
##  1  2008     3    15     0 Temp_gaps  6.76
##  2  2008     3    15     0 Temp       6.76
##  3  2008     3    15     1 Temp_gaps  6.48
##  4  2008     3    15     1 Temp       6.48
##  5  2008     3    15     2 Temp_gaps  5.51
##  6  2008     3    15     2 Temp       5.51
##  7  2008     3    15     3 Temp_gaps  6.89
##  8  2008     3    15     3 Temp       6.89
##  9  2008     3    15     4 Temp_gaps  6.10
## 10  2008     3    15     4 Temp       6.10
## # ℹ 38 more rows
```

-   

    d)  *Use* `ggplot2` *to plot* `Temp_gaps` *and* `Temp` *as facets (point or line plot)*


``` r
ggplot(WHGlong, aes(Hour, value)) +
  geom_line(lwd = 1.5) +
  facet_grid(cols = vars(name)) +
  ylab("Temperature (°C)") +
  theme_bw(base_size = 15)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-149-1.png" width="672" />

-   

    e)  *Convert the dataset back to the* `wide` *format*


``` r
WHGwide <- WHGlong %>% pivot_wider(names_from = name)
WHGwide
```

```
## # A tibble: 24 × 6
##     Year Month   Day  Hour Temp_gaps  Temp
##    <int> <int> <int> <int>     <dbl> <dbl>
##  1  2008     3    15     0      6.76  6.76
##  2  2008     3    15     1      6.48  6.48
##  3  2008     3    15     2      5.51  5.51
##  4  2008     3    15     3      6.89  6.89
##  5  2008     3    15     4      6.10  6.10
##  6  2008     3    15     5     NA     6.91
##  7  2008     3    15     6     NA     6.10
##  8  2008     3    15     7     NA     5.98
##  9  2008     3    15     8     NA     8.99
## 10  2008     3    15     9     10.8  10.8 
## # ℹ 14 more rows
```

-   

    f)  *Select only the following columns:* `Year`, `Month`, `Day` *and* `Temp`


``` r
WHG %>% select(c(Year, Month, Day, Temp))
```

```
## # A tibble: 24 × 4
##     Year Month   Day  Temp
##    <int> <int> <int> <dbl>
##  1  2008     3    15  6.76
##  2  2008     3    15  6.48
##  3  2008     3    15  5.51
##  4  2008     3    15  6.89
##  5  2008     3    15  6.10
##  6  2008     3    15  6.91
##  7  2008     3    15  6.10
##  8  2008     3    15  5.98
##  9  2008     3    15  8.99
## 10  2008     3    15 10.8 
## # ℹ 14 more rows
```

-   

    g)  *Sort the dataset by the* `Temp` *column, in descending order*


``` r
WHG %>% arrange(desc(Temp))
```

```
## # A tibble: 24 × 6
##     Year Month   Day  Hour Temp_gaps  Temp
##    <int> <int> <int> <int>     <dbl> <dbl>
##  1  2008     3    15    13      NA    15.2
##  2  2008     3    15    16      14.5  14.5
##  3  2008     3    15    14      NA    14.2
##  4  2008     3    15    12      NA    14.2
##  5  2008     3    15    15      14.1  14.1
##  6  2008     3    15    11      NA    13.6
##  7  2008     3    15    17      13.3  13.3
##  8  2008     3    15    18      12.1  12.1
##  9  2008     3    15    10      12.0  12.0
## 10  2008     3    15     9      10.8  10.8
## # ℹ 14 more rows
```

2.  *For the* `Winter_hours_gaps` *dataset, write a* `for` *loop to convert all temperatures* *(*`Temp` *column) to degrees Fahrenheit*

So that the execution of the following code does not take too long, only Julian Day 15 (rows 279 to 302) is used here. To convert the entire `Temp` column to Fahrenheit, just omit `[279:302]`


``` r
Temp <- Winters_hours_gaps$Temp[279:302]

for (i in Temp)
{
  Fahrenheit <- i * 1.8 + 32 
  print(Fahrenheit)
}
```

```
## [1] 44.1734
## [1] 43.6712
## [1] 41.9252
## [1] 44.4002
## [1] 42.9836
## [1] 44.4452
## [1] 42.9836
## [1] 42.755
## [1] 48.182
## [1] 51.3698
## [1] 53.69
## [1] 56.4692
## [1] 57.506
## [1] 59.4446
## [1] 57.5492
## [1] 57.3332
## [1] 58.1522
## [1] 55.9058
## [1] 53.8196
## [1] 49.4708
## [1] 47.6474
## [1] 47.3342
## [1] 48.182
## [1] 47.7806
```

3.  *Execute the same operation with a function from the* `apply` *family*

Here it is the same as in 2, just omit `[279:302]` to convert the entire `Temp` column


``` r
x <- Winters_hours_gaps$Temp

fahrenheit <- function(x)
  x * 1.8 + 32

sapply(x[279:302], fahrenheit)
```

```
##  [1] 44.1734 43.6712 41.9252 44.4002 42.9836 44.4452 42.9836 42.7550 48.1820 51.3698 53.6900
## [12] 56.4692 57.5060 59.4446 57.5492 57.3332 58.1522 55.9058 53.8196 49.4708 47.6474 47.3342
## [23] 48.1820 47.7806
```

4.  *Now use the* `tidyverse` *function* `mutate` *to achieve the same outcome*


``` r
WHG_F <- WHG %>% mutate(Temp_F = Temp * 1.8 + 32)
WHG_F
```

```
## # A tibble: 24 × 7
##     Year Month   Day  Hour Temp_gaps  Temp Temp_F
##    <int> <int> <int> <int>     <dbl> <dbl>  <dbl>
##  1  2008     3    15     0      6.76  6.76   44.2
##  2  2008     3    15     1      6.48  6.48   43.7
##  3  2008     3    15     2      5.51  5.51   41.9
##  4  2008     3    15     3      6.89  6.89   44.4
##  5  2008     3    15     4      6.10  6.10   43.0
##  6  2008     3    15     5     NA     6.91   44.4
##  7  2008     3    15     6     NA     6.10   43.0
##  8  2008     3    15     7     NA     5.98   42.8
##  9  2008     3    15     8     NA     8.99   48.2
## 10  2008     3    15     9     10.8  10.8    51.4
## # ℹ 14 more rows
```

<!--chapter:end:09-tools-in-R.Rmd-->

# Getting temperature data

## Learning goals for this lesson

-   Appreciate the need for daily temperature data
-   Know how to get a list of promising weather stations contained in an international database
-   Be able to download weather data using `chillR` functions
-   Know how to convert downloaded data into `chillR` format

## Temperature data needs

Temperature data is essential for phenology and chill modeling, as it serves as a key input for these models. Although weather data might seem easily accessible, it is often challenging to obtain. Many countries have official weather stations that record the necessary information, but access to these data is frequently restricted and expensive, despite likely being funded by taxpayers. While such costs may be manageable for small-scale studies, they quickly become prohibitive for larger analyses.

Given the urgent need to understand climate change impacts, these access limitations are a barrier to effective climate research. Such restrictions may also reduce the quality of studies that rely on comprehensive data. Ideally, high-quality, localized datasets would be available, but in their absence, some alternative databases can be used. Currently, `chillR` connects to one global and one California-specific database, with the potential to expand as more data sources become accessible.

## The Global Summary of the Day database

The [National Centers for Environmental Information (NCEI)](https://www.ncei.noaa.gov/), formerly known as the National Climatic Data Center (NCDC), offers valuable temperature data through its [Global Summary of the Day (GSOD) database](https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-day). While accessing this data can be challenging, the bulk download section provides weather records for each station and year. However, finding specific stations can be time-consuming.

A list of weather stations is available on NOAA's website, and the process of downloading and organizing the data can be automated using the `chillR` tool. A previous user, [Adrian Fülle](https://www.gartenbauwissenschaft.uni-bonn.de/author/adrian-fulle/), developed a faster and more efficient method for this task. The `chillR` function `handle_gsod()` simplifies the process by guiding users through the necessary steps.

### `action=list_stations`

When used with this action, the `handle_gsod()` function retrieves a list of weather stations and sorts them by their proximity to specified coordinates. For example, stations near Bonn (Latitude: 50.73, Longitude: 7.10) can be identified. Additionally, a time interval, such as 1990-2020, can be set to limit the search to data from those specific years:


``` r
library(chillR)
station_list<-handle_gsod(action="list_stations",
                          location=c(7.10,50.73),
                          time_interval=c(1990,2020))
```




``` r
require(kableExtra)

kable(station_list) %>%
  kable_styling("striped", position = "left", font_size = 8)
```

<table class="table table-striped" style="font-size: 8px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:right;"> chillR_code </th>
   <th style="text-align:left;"> STATION.NAME </th>
   <th style="text-align:left;"> CTRY </th>
   <th style="text-align:right;"> Lat </th>
   <th style="text-align:right;"> Long </th>
   <th style="text-align:right;"> BEGIN </th>
   <th style="text-align:right;"> END </th>
   <th style="text-align:right;"> Distance </th>
   <th style="text-align:right;"> Overlap_years </th>
   <th style="text-align:right;"> Perc_interval_covered </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 10517099999 </td>
   <td style="text-align:left;"> BONN/FRIESDORF(AUT) </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.700 </td>
   <td style="text-align:right;"> 7.150 </td>
   <td style="text-align:right;"> 19360102 </td>
   <td style="text-align:right;"> 19921231 </td>
   <td style="text-align:right;"> 4.86 </td>
   <td style="text-align:right;"> 3.00 </td>
   <td style="text-align:right;"> 10 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10518099999 </td>
   <td style="text-align:left;"> BONN-HARDTHOEHE </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.700 </td>
   <td style="text-align:right;"> 7.033 </td>
   <td style="text-align:right;"> 19750523 </td>
   <td style="text-align:right;"> 19971223 </td>
   <td style="text-align:right;"> 5.78 </td>
   <td style="text-align:right;"> 7.98 </td>
   <td style="text-align:right;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10519099999 </td>
   <td style="text-align:left;"> BONN-ROLEBER </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.733 </td>
   <td style="text-align:right;"> 7.200 </td>
   <td style="text-align:right;"> 20010705 </td>
   <td style="text-align:right;"> 20081231 </td>
   <td style="text-align:right;"> 7.05 </td>
   <td style="text-align:right;"> 7.49 </td>
   <td style="text-align:right;"> 24 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10513099999 </td>
   <td style="text-align:left;"> KOLN BONN </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.866 </td>
   <td style="text-align:right;"> 7.143 </td>
   <td style="text-align:right;"> 19310101 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 15.44 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10509099999 </td>
   <td style="text-align:left;"> BUTZWEILERHOF(BAFB) </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.983 </td>
   <td style="text-align:right;"> 6.900 </td>
   <td style="text-align:right;"> 19780901 </td>
   <td style="text-align:right;"> 19950823 </td>
   <td style="text-align:right;"> 31.48 </td>
   <td style="text-align:right;"> 5.64 </td>
   <td style="text-align:right;"> 18 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10502099999 </td>
   <td style="text-align:left;"> NORVENICH </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.831 </td>
   <td style="text-align:right;"> 6.658 </td>
   <td style="text-align:right;"> 19730101 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 33.08 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10514099999 </td>
   <td style="text-align:left;"> MENDIG </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.366 </td>
   <td style="text-align:right;"> 7.315 </td>
   <td style="text-align:right;"> 19730102 </td>
   <td style="text-align:right;"> 19971231 </td>
   <td style="text-align:right;"> 43.28 </td>
   <td style="text-align:right;"> 8.00 </td>
   <td style="text-align:right;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10506099999 </td>
   <td style="text-align:left;"> NUERBURG-BARWEILER </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.367 </td>
   <td style="text-align:right;"> 6.867 </td>
   <td style="text-align:right;"> 19950401 </td>
   <td style="text-align:right;"> 19971231 </td>
   <td style="text-align:right;"> 43.64 </td>
   <td style="text-align:right;"> 2.75 </td>
   <td style="text-align:right;"> 9 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10508099999 </td>
   <td style="text-align:left;"> BLANKENHEIM </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.450 </td>
   <td style="text-align:right;"> 6.650 </td>
   <td style="text-align:right;"> 19781002 </td>
   <td style="text-align:right;"> 19840504 </td>
   <td style="text-align:right;"> 44.53 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10510099999 </td>
   <td style="text-align:left;"> NUERBURG </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.333 </td>
   <td style="text-align:right;"> 6.950 </td>
   <td style="text-align:right;"> 19300901 </td>
   <td style="text-align:right;"> 19921231 </td>
   <td style="text-align:right;"> 45.45 </td>
   <td style="text-align:right;"> 3.00 </td>
   <td style="text-align:right;"> 10 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10515099999 </td>
   <td style="text-align:left;"> BENDORF </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.417 </td>
   <td style="text-align:right;"> 7.583 </td>
   <td style="text-align:right;"> 19310102 </td>
   <td style="text-align:right;"> 20030816 </td>
   <td style="text-align:right;"> 48.79 </td>
   <td style="text-align:right;"> 13.62 </td>
   <td style="text-align:right;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10504099999 </td>
   <td style="text-align:left;"> EIFEL </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.650 </td>
   <td style="text-align:right;"> 6.283 </td>
   <td style="text-align:right;"> 20040501 </td>
   <td style="text-align:right;"> 20040501 </td>
   <td style="text-align:right;"> 58.30 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10526099999 </td>
   <td style="text-align:left;"> BAD MARIENBERG </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.667 </td>
   <td style="text-align:right;"> 7.967 </td>
   <td style="text-align:right;"> 19730101 </td>
   <td style="text-align:right;"> 20030816 </td>
   <td style="text-align:right;"> 61.54 </td>
   <td style="text-align:right;"> 13.62 </td>
   <td style="text-align:right;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10613099999 </td>
   <td style="text-align:left;"> BUCHEL </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.174 </td>
   <td style="text-align:right;"> 7.063 </td>
   <td style="text-align:right;"> 19730101 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 61.95 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10503099999 </td>
   <td style="text-align:left;"> AACHEN/MERZBRUCK </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.817 </td>
   <td style="text-align:right;"> 6.183 </td>
   <td style="text-align:right;"> 19780901 </td>
   <td style="text-align:right;"> 19971212 </td>
   <td style="text-align:right;"> 65.28 </td>
   <td style="text-align:right;"> 7.95 </td>
   <td style="text-align:right;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10419099999 </td>
   <td style="text-align:left;"> LUDENSCHEID       &amp; </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.233 </td>
   <td style="text-align:right;"> 7.600 </td>
   <td style="text-align:right;"> 19270906 </td>
   <td style="text-align:right;"> 20030306 </td>
   <td style="text-align:right;"> 66.06 </td>
   <td style="text-align:right;"> 13.18 </td>
   <td style="text-align:right;"> 43 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10400099999 </td>
   <td style="text-align:left;"> DUSSELDORF </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.289 </td>
   <td style="text-align:right;"> 6.767 </td>
   <td style="text-align:right;"> 19310102 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 66.46 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10616299999 </td>
   <td style="text-align:left;"> SIEGERLAND </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.708 </td>
   <td style="text-align:right;"> 8.083 </td>
   <td style="text-align:right;"> 20040510 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 69.33 </td>
   <td style="text-align:right;"> 16.65 </td>
   <td style="text-align:right;"> 54 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10418099999 </td>
   <td style="text-align:left;"> LUEDENSCHEID </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.250 </td>
   <td style="text-align:right;"> 7.650 </td>
   <td style="text-align:right;"> 19940301 </td>
   <td style="text-align:right;"> 19971231 </td>
   <td style="text-align:right;"> 69.54 </td>
   <td style="text-align:right;"> 3.84 </td>
   <td style="text-align:right;"> 12 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10437499999 </td>
   <td style="text-align:left;"> MONCHENGLADBACH </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.230 </td>
   <td style="text-align:right;"> 6.504 </td>
   <td style="text-align:right;"> 19960715 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 69.59 </td>
   <td style="text-align:right;"> 24.47 </td>
   <td style="text-align:right;"> 79 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10403099999 </td>
   <td style="text-align:left;"> MOENCHENGLADBACH </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.233 </td>
   <td style="text-align:right;"> 6.500 </td>
   <td style="text-align:right;"> 19381001 </td>
   <td style="text-align:right;"> 19421031 </td>
   <td style="text-align:right;"> 70.03 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10501099999 </td>
   <td style="text-align:left;"> AACHEN </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 50.783 </td>
   <td style="text-align:right;"> 6.100 </td>
   <td style="text-align:right;"> 19280101 </td>
   <td style="text-align:right;"> 20030816 </td>
   <td style="text-align:right;"> 70.67 </td>
   <td style="text-align:right;"> 13.62 </td>
   <td style="text-align:right;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6496099999 </td>
   <td style="text-align:left;"> ELSENBORN (MIL) </td>
   <td style="text-align:left;"> BE </td>
   <td style="text-align:right;"> 50.467 </td>
   <td style="text-align:right;"> 6.183 </td>
   <td style="text-align:right;"> 19840501 </td>
   <td style="text-align:right;"> 20241102 </td>
   <td style="text-align:right;"> 71.10 </td>
   <td style="text-align:right;"> 31.00 </td>
   <td style="text-align:right;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6495099999 </td>
   <td style="text-align:left;"> BOTRANGE (MOUNT) </td>
   <td style="text-align:left;"> BE </td>
   <td style="text-align:right;"> 50.500 </td>
   <td style="text-align:right;"> 6.100 </td>
   <td style="text-align:right;"> 19510201 </td>
   <td style="text-align:right;"> 20011015 </td>
   <td style="text-align:right;"> 75.13 </td>
   <td style="text-align:right;"> 11.79 </td>
   <td style="text-align:right;"> 38 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10409099999 </td>
   <td style="text-align:left;"> ESSEN/MUELHEIM </td>
   <td style="text-align:left;"> GM </td>
   <td style="text-align:right;"> 51.400 </td>
   <td style="text-align:right;"> 6.967 </td>
   <td style="text-align:right;"> 19300414 </td>
   <td style="text-align:right;"> 19431231 </td>
   <td style="text-align:right;"> 75.17 </td>
   <td style="text-align:right;"> 0.00 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>

The list provided contains the 25 closest weather stations to the specified location, ordered by their distance to the target coordinates, which is shown in the `distance` column. The `Overlap_years` column indicates the number of years for which data is available, while the `Perc_interval_covered` column shows the percentage of the target time period that is covered by the data. It's important to note that this is based solely on the start and end dates in the table. The dataset may have gaps, and these gaps can sometimes cover almost the entire record.

### `action="download_weather"`

When used with this option, the `handle_gsod()` function downloads the weather data for a specific station, using its unique `chillR_code`, which is displayed in the respective column of the station list. Instead of manually entering the code, the function can reference the code from the station list. To download the data, the code for the 4th station in the list can be used, as it appears to cover most of the desired time period.


``` r
weather<-handle_gsod(action="download_weather",
                     location=station_list$chillR_code[4],
                     time_interval=c(1990,2020))
```

The result of this operation is a list with two elements. The first element (`weather[[1]]`) indicates the source of the database from which the data was retrieved. The second element (`weather[[2]]`) contains the actual weather dataset, which can be viewed here.


``` r
weather[[1]][1:20,]
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:right;"> X </th>
   <th style="text-align:left;"> DATE </th>
   <th style="text-align:left;"> Date </th>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:right;"> Month </th>
   <th style="text-align:right;"> Day </th>
   <th style="text-align:right;"> Tmin </th>
   <th style="text-align:right;"> Tmax </th>
   <th style="text-align:right;"> Tmean </th>
   <th style="text-align:right;"> Prec </th>
   <th style="text-align:right;"> YEARMODA </th>
   <th style="text-align:left;"> Tmin_source </th>
   <th style="text-align:left;"> Tmax_source </th>
   <th style="text-align:left;"> no_Tmin </th>
   <th style="text-align:left;"> no_Tmax </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> 1990-01-01 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-01 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900101 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:left;"> 1990-01-02 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-02 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900102 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> 1990-01-03 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-03 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> -0.389 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 0.722 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900103 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> 1990-01-04 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-04 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> -1.111 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> -0.056 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900104 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> 1990-01-05 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-05 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> -1.111 </td>
   <td style="text-align:right;"> 3.111 </td>
   <td style="text-align:right;"> 1.556 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900105 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> 1990-01-06 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-06 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 2.389 </td>
   <td style="text-align:right;"> 1.333 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900106 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:left;"> 1990-01-07 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-07 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> -0.111 </td>
   <td style="text-align:right;"> 4.278 </td>
   <td style="text-align:right;"> 1.056 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900107 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> 1990-01-08 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-08 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> -0.111 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 3.278 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900108 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> 1990-01-09 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-09 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:right;"> 3.778 </td>
   <td style="text-align:right;"> 8.000 </td>
   <td style="text-align:right;"> 5.333 </td>
   <td style="text-align:right;"> 0.508 </td>
   <td style="text-align:right;"> 19900109 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> 1990-01-10 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-10 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 3.000 </td>
   <td style="text-align:right;"> 6.000 </td>
   <td style="text-align:right;"> 4.556 </td>
   <td style="text-align:right;"> 1.016 </td>
   <td style="text-align:right;"> 19900110 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> 1990-01-11 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-11 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:right;"> 3.278 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 5.167 </td>
   <td style="text-align:right;"> 0.254 </td>
   <td style="text-align:right;"> 19900111 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:left;"> 1990-01-12 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-12 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 5.222 </td>
   <td style="text-align:right;"> 1.778 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900112 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:left;"> 1990-01-13 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-13 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:right;"> -1.278 </td>
   <td style="text-align:right;"> 4.000 </td>
   <td style="text-align:right;"> 1.389 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900113 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:left;"> 1990-01-14 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-14 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:right;"> -0.222 </td>
   <td style="text-align:right;"> 5.000 </td>
   <td style="text-align:right;"> 3.167 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900114 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:left;"> 1990-01-15 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-15 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:right;"> 0.889 </td>
   <td style="text-align:right;"> 9.000 </td>
   <td style="text-align:right;"> 4.556 </td>
   <td style="text-align:right;"> 1.016 </td>
   <td style="text-align:right;"> 19900115 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:left;"> 1990-01-16 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-16 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 6.222 </td>
   <td style="text-align:right;"> 11.000 </td>
   <td style="text-align:right;"> 9.944 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900116 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:left;"> 1990-01-17 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-17 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 11.000 </td>
   <td style="text-align:right;"> 8.500 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900117 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:left;"> 1990-01-18 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-18 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 2.722 </td>
   <td style="text-align:right;"> 0.254 </td>
   <td style="text-align:right;"> 19900118 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:left;"> 1990-01-19 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-19 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 7.111 </td>
   <td style="text-align:right;"> 4.611 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 19900119 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 20 </td>
   <td style="text-align:left;"> 1990-01-20 12:00:00 </td>
   <td style="text-align:left;"> 1990-01-20 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 20 </td>
   <td style="text-align:right;"> 4.000 </td>
   <td style="text-align:right;"> 8.500 </td>
   <td style="text-align:right;"> 6.056 </td>
   <td style="text-align:right;"> 2.286 </td>
   <td style="text-align:right;"> 19900120 </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> original </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> FALSE </td>
  </tr>
</tbody>
</table>

The data appears complicated and includes unnecessary information. To simplify this, `chillR` provides a function that streamlines the record. However, this process removes several variables, including quality flags, which may indicate unreliable data. While these have been overlooked so far, there is potential for improvement.

### downloaded weather as `action` argument

This method of calling `handle_gsod()` cleans the dataset and converts it into a format that `chillR` can easily process.


``` r
cleaned_weather<-handle_gsod(weather)
```


``` r
cleaned_weather[[1]][1:20,]
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:left;"> Date </th>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:right;"> Month </th>
   <th style="text-align:right;"> Day </th>
   <th style="text-align:right;"> Tmin </th>
   <th style="text-align:right;"> Tmax </th>
   <th style="text-align:right;"> Tmean </th>
   <th style="text-align:right;"> Prec </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 1990-01-01 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-02 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-03 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> -0.389 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 0.722 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-04 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> -1.111 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> -0.056 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-05 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> -1.111 </td>
   <td style="text-align:right;"> 3.111 </td>
   <td style="text-align:right;"> 1.556 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-06 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 2.389 </td>
   <td style="text-align:right;"> 1.333 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-07 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:right;"> -0.111 </td>
   <td style="text-align:right;"> 4.278 </td>
   <td style="text-align:right;"> 1.056 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-08 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> -0.111 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 3.278 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-09 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:right;"> 3.778 </td>
   <td style="text-align:right;"> 8.000 </td>
   <td style="text-align:right;"> 5.333 </td>
   <td style="text-align:right;"> 0.508 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-10 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 3.000 </td>
   <td style="text-align:right;"> 6.000 </td>
   <td style="text-align:right;"> 4.556 </td>
   <td style="text-align:right;"> 1.016 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-11 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:right;"> 3.278 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 5.167 </td>
   <td style="text-align:right;"> 0.254 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-12 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 5.222 </td>
   <td style="text-align:right;"> 1.778 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-13 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:right;"> -1.278 </td>
   <td style="text-align:right;"> 4.000 </td>
   <td style="text-align:right;"> 1.389 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-14 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:right;"> -0.222 </td>
   <td style="text-align:right;"> 5.000 </td>
   <td style="text-align:right;"> 3.167 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-15 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:right;"> 0.889 </td>
   <td style="text-align:right;"> 9.000 </td>
   <td style="text-align:right;"> 4.556 </td>
   <td style="text-align:right;"> 1.016 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-16 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;"> 6.222 </td>
   <td style="text-align:right;"> 11.000 </td>
   <td style="text-align:right;"> 9.944 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-17 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 17 </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 11.000 </td>
   <td style="text-align:right;"> 8.500 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-18 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:right;"> -1.000 </td>
   <td style="text-align:right;"> 7.000 </td>
   <td style="text-align:right;"> 2.722 </td>
   <td style="text-align:right;"> 0.254 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-19 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 19 </td>
   <td style="text-align:right;"> 2.000 </td>
   <td style="text-align:right;"> 7.111 </td>
   <td style="text-align:right;"> 4.611 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1990-01-20 12:00:00 </td>
   <td style="text-align:right;"> 1990 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 20 </td>
   <td style="text-align:right;"> 4.000 </td>
   <td style="text-align:right;"> 8.500 </td>
   <td style="text-align:right;"> 6.056 </td>
   <td style="text-align:right;"> 2.286 </td>
  </tr>
</tbody>
</table>

The strange numbers in the dataset are due to the original database storing temperatures in degrees Fahrenheit. These values were then converted to degrees Celsius using the formula:

$Temperature[°C]=(Temperature[°F]-32)\cdot\frac{5}{9}$

This conversion process can result in awkward numbers, but it's straightforward to apply. After this conversion, the temperature records are now in a more usable format for working with `chillR`.

However, upon closer inspection, the dataset reveals significant gaps, including entire years with missing data. This issue will be addressed in the lesson on filling gaps in temperature records.

Additionally, `chillR` has a similar function for downloading data from the [California Irrigation Management Information System (CIMIS)](https://cimis.water.ca.gov/), and there is potential for more data sources to be integrated into `chillR`.

Finally, the files generated in this process will be saved for use in upcoming chapters:


``` r
write.csv(station_list,"data/station_list.csv",row.names=FALSE)
write.csv(weather[[1]],"data/Bonn_raw_weather.csv",row.names=FALSE)
write.csv(cleaned_weather[[1]],"data/Bonn_chillR_weather.csv",row.names=FALSE)
```

## `Exercises` on getting temperature data

Please document all results of the following assignments in your `learning logbook`.

1)  *Choose a location of interest and find the 25 closest weather stations using the* `handle_gsod` *function*




``` r
station_list_Yakima <- handle_gsod(action = "list_stations",
                                   location = c(long = -120.50, lat = 46.60), 
                                   time_interval = c(1990, 2020))
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> chillR_code </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STATION.NAME </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> CTRY </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Lat </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Long </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> BEGIN </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> END </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Distance </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Overlap_years </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_interval_covered </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> YAKIMA AIR TERMINAL/MCALSR FIELD AP </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.564 </td>
   <td style="text-align:center;"> -120.535 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 4.82 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924243 </td>
   <td style="text-align:center;"> YAKIMA AIR TERMINAL </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.568 </td>
   <td style="text-align:center;"> -120.543 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19721231 </td>
   <td style="text-align:center;"> 4.85 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781399999 </td>
   <td style="text-align:center;"> VAGABOND AAF / YAKIMA TRAINING CENTER WASHINGTON USA </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.667 </td>
   <td style="text-align:center;"> -120.454 </td>
   <td style="text-align:center;"> 20030617 </td>
   <td style="text-align:center;"> 20081110 </td>
   <td style="text-align:center;"> 8.25 </td>
   <td style="text-align:center;"> 5.40 </td>
   <td style="text-align:center;"> 17 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72056299999 </td>
   <td style="text-align:center;"> RANGE OP 13 / YAKIMA TRAINING CENTER </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.800 </td>
   <td style="text-align:center;"> -120.167 </td>
   <td style="text-align:center;"> 20080530 </td>
   <td style="text-align:center;"> 20170920 </td>
   <td style="text-align:center;"> 33.79 </td>
   <td style="text-align:center;"> 9.31 </td>
   <td style="text-align:center;"> 30 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788399999 </td>
   <td style="text-align:center;"> BOWERS FLD </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.033 </td>
   <td style="text-align:center;"> -120.531 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 48.26 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788324220 </td>
   <td style="text-align:center;"> BOWERS FIELD AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.034 </td>
   <td style="text-align:center;"> -120.531 </td>
   <td style="text-align:center;"> 19880106 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 48.37 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924220 </td>
   <td style="text-align:center;"> ELLENSBURG BOWERS FI </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.034 </td>
   <td style="text-align:center;"> -120.530 </td>
   <td style="text-align:center;"> 19480601 </td>
   <td style="text-align:center;"> 19550101 </td>
   <td style="text-align:center;"> 48.37 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784094187 </td>
   <td style="text-align:center;"> HANFORD AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.567 </td>
   <td style="text-align:center;"> -119.600 </td>
   <td style="text-align:center;"> 20060101 </td>
   <td style="text-align:center;"> 20130326 </td>
   <td style="text-align:center;"> 68.96 </td>
   <td style="text-align:center;"> 7.23 </td>
   <td style="text-align:center;"> 23 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784099999 </td>
   <td style="text-align:center;"> HANFORD </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.567 </td>
   <td style="text-align:center;"> -119.600 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 68.96 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782594239 </td>
   <td style="text-align:center;"> PANGBORN MEMORIAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.397 </td>
   <td style="text-align:center;"> -120.201 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 91.58 </td>
   <td style="text-align:center;"> 21.00 </td>
   <td style="text-align:center;"> 68 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782599999 </td>
   <td style="text-align:center;"> PANGBORN MEM </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.399 </td>
   <td style="text-align:center;"> -120.207 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 91.69 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788499999 </td>
   <td style="text-align:center;"> RICHLAND AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.306 </td>
   <td style="text-align:center;"> -119.304 </td>
   <td style="text-align:center;"> 19810203 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 97.39 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781524237 </td>
   <td style="text-align:center;"> STAMPASS PASS FLTWO </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.277 </td>
   <td style="text-align:center;"> -121.337 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 98.63 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924237 </td>
   <td style="text-align:center;"> STAMPEDE PASS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.277 </td>
   <td style="text-align:center;"> -121.337 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19721231 </td>
   <td style="text-align:center;"> 98.63 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72790024141 </td>
   <td style="text-align:center;"> EPHRATA MUNICIPAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.516 </td>
   <td style="text-align:center;"> 20050101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 108.64 </td>
   <td style="text-align:center;"> 16.00 </td>
   <td style="text-align:center;"> 52 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782624141 </td>
   <td style="text-align:center;"> EPHRATA MUNICIPAL </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.515 </td>
   <td style="text-align:center;"> 19420101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 108.69 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924141 </td>
   <td style="text-align:center;"> EPHRATA AP FCWOS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.515 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19550101 </td>
   <td style="text-align:center;"> 108.69 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782724110 </td>
   <td style="text-align:center;"> GRANT COUNTY INTL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.193 </td>
   <td style="text-align:center;"> -119.315 </td>
   <td style="text-align:center;"> 19430610 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 111.73 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782799999 </td>
   <td style="text-align:center;"> MOSES LAKE/GRANT CO </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.200 </td>
   <td style="text-align:center;"> -119.317 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 112.06 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784524163 </td>
   <td style="text-align:center;"> TRI-CITIES AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.270 </td>
   <td style="text-align:center;"> -119.118 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 112.21 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784599999 </td>
   <td style="text-align:center;"> TRI CITIES </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.267 </td>
   <td style="text-align:center;"> -119.117 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 112.40 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924163 </td>
   <td style="text-align:center;"> PASCO NAS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.267 </td>
   <td style="text-align:center;"> -119.117 </td>
   <td style="text-align:center;"> 19450401 </td>
   <td style="text-align:center;"> 19460601 </td>
   <td style="text-align:center;"> 112.40 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72698824219 </td>
   <td style="text-align:center;"> MUNICIPAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.619 </td>
   <td style="text-align:center;"> -121.166 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 120.70 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924219 </td>
   <td style="text-align:center;"> THE DALLES MUNICIPAL ARPT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.619 </td>
   <td style="text-align:center;"> -121.166 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19650101 </td>
   <td style="text-align:center;"> 120.70 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72688399999 </td>
   <td style="text-align:center;"> HERMISTON MUNI </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.828 </td>
   <td style="text-align:center;"> -119.259 </td>
   <td style="text-align:center;"> 19980514 </td>
   <td style="text-align:center;"> 20051231 </td>
   <td style="text-align:center;"> 128.55 </td>
   <td style="text-align:center;"> 7.64 </td>
   <td style="text-align:center;"> 25 </td>
  </tr>
</tbody>
</table></div>

2)  *Download weather data for the most promising station on the list*


``` r
weather_Yakima <- handle_gsod(action = "download_weather",
                              location = station_list_Yakima$chillR_code[1],
                              time_interval = c(1990, 2020))
```

```
## Loading data for 31 years from station 'YAKIMA AIR TERMINAL/MCALSR FIELD AP'
## ===============================================================================================
```


``` r
weather_Yakima[[1]][1:20,]
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STATION </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> DATE </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> LATITUDE </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> LONGITUDE </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> ELEVATION </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> NAME </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> TEMP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> TEMP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> DEWP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> DEWP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> SLP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> SLP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> VISIB </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> VISIB_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> WDSP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> WDSP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> MXSPD </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> GUST </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> MAX </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> MAX_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> MIN </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> MIN_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> PRCP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> PRCP_ATTRIBUTES </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> SNDP </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> FRSHTT </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-01 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 31.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 30.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1014.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 975.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 2.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 4.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 7.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 35.1 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 28.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 100000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-02 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 32.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 23.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1015.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 975.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 24.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 12.0 </td>
   <td style="text-align:center;"> 18.1 </td>
   <td style="text-align:center;"> 43.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 21.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 100000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-03 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 32.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 24.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1023.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 983.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 21.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 3.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 46.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 21.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-04 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 36.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 29.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1020.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 980.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 21.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 15.9 </td>
   <td style="text-align:center;"> 24.1 </td>
   <td style="text-align:center;"> 57.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 26.1 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-05 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 36.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 27.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1022.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 983.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 21.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 5.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 18.1 </td>
   <td style="text-align:center;"> 25.1 </td>
   <td style="text-align:center;"> 57.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 26.1 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-06 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 43.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 34.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1016.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 977.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 25.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 22.9 </td>
   <td style="text-align:center;"> 28.0 </td>
   <td style="text-align:center;"> 53.1 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 26.1 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 10000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-07 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 48.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 39.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1005.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 967.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 27.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 9.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 15.9 </td>
   <td style="text-align:center;"> 26.0 </td>
   <td style="text-align:center;"> 53.1 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 28.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.12 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 10000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-08 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 44.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 37.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1005.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 966.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 27.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 7.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 18.1 </td>
   <td style="text-align:center;"> 27.0 </td>
   <td style="text-align:center;"> 54.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 37.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.38 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 10000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-09 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 39.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 36.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1010.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 971.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 10.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 5.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 15.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 52.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 34.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.62 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 110000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-10 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 44.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 29.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1019.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 980.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 29.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 18.1 </td>
   <td style="text-align:center;"> 22.0 </td>
   <td style="text-align:center;"> 54.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 34.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.11 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 10000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-11 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 37.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 26.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1030.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 990.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 25.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 11.1 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 46.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 32.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 1000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-12 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 37.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 27.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1020.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 980.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 25.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 10.1 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 43.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 32.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.01 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 11000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-13 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 33.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 29.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1010.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 971.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 17.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 3.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 43.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 27.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.01 </td>
   <td style="text-align:center;"> G </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 10000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-14 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 31.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 28.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1015.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 975.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 16.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 3.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 41.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 25.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-15 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 33.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 30.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1021.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 981.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 2.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 3.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 7.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 39.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 25.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 100000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-16 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 38.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 33.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1016.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 977.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 11.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 5.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.9 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 45.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 30.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 110000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-17 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 34.0 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 25.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1023.9 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 984.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 30.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 10.1 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 46.0 </td>
   <td style="text-align:center;"> * </td>
   <td style="text-align:center;"> 24.1 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-18 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 27.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 21.6 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1028.8 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 988.5 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 26.1 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 5.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.9 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 46.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 18.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-19 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 32.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 27.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1024.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 984.2 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 21.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 5.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 8.9 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 37.9 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 18.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> 1990-01-20 </td>
   <td style="text-align:center;"> 46.56398 </td>
   <td style="text-align:center;"> -120.5349 </td>
   <td style="text-align:center;"> 321 </td>
   <td style="text-align:center;"> YAKIMA AIRPORT, WA US </td>
   <td style="text-align:center;"> 33.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 26.4 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1027.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 987.7 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 14.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 1.3 </td>
   <td style="text-align:center;"> 24 </td>
   <td style="text-align:center;"> 6.0 </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 36.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 28.0 </td>
   <td style="text-align:center;">  </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> D </td>
   <td style="text-align:center;"> 999.9 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
</tbody>
</table></div>

3)  *Convert the weather data into* `chillR` *format*


``` r
cleaned_weather_Yakima <- handle_gsod(weather_Yakima) 
```


``` r
cleaned_weather_Yakima[[1]][1:20,]
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Date </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Month </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Day </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Tmean </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Prec </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1990-01-01 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> -1.722 </td>
   <td style="text-align:center;"> 1.722 </td>
   <td style="text-align:center;"> -0.500 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-02 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> -5.611 </td>
   <td style="text-align:center;"> 6.111 </td>
   <td style="text-align:center;"> 0.056 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-03 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> -5.611 </td>
   <td style="text-align:center;"> 7.778 </td>
   <td style="text-align:center;"> 0.056 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-04 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> -3.278 </td>
   <td style="text-align:center;"> 13.889 </td>
   <td style="text-align:center;"> 2.444 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-05 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> -3.278 </td>
   <td style="text-align:center;"> 13.889 </td>
   <td style="text-align:center;"> 2.556 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-06 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> -3.278 </td>
   <td style="text-align:center;"> 11.722 </td>
   <td style="text-align:center;"> 6.222 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-07 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> -2.222 </td>
   <td style="text-align:center;"> 11.722 </td>
   <td style="text-align:center;"> 9.000 </td>
   <td style="text-align:center;"> 3.048 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-08 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 2.778 </td>
   <td style="text-align:center;"> 12.222 </td>
   <td style="text-align:center;"> 6.722 </td>
   <td style="text-align:center;"> 9.652 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-09 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 1.111 </td>
   <td style="text-align:center;"> 11.111 </td>
   <td style="text-align:center;"> 4.111 </td>
   <td style="text-align:center;"> 15.748 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-10 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 1.111 </td>
   <td style="text-align:center;"> 12.222 </td>
   <td style="text-align:center;"> 7.167 </td>
   <td style="text-align:center;"> 2.794 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-11 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 0.000 </td>
   <td style="text-align:center;"> 8.278 </td>
   <td style="text-align:center;"> 2.778 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-12 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 0.000 </td>
   <td style="text-align:center;"> 6.111 </td>
   <td style="text-align:center;"> 2.833 </td>
   <td style="text-align:center;"> 0.254 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-13 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> -2.778 </td>
   <td style="text-align:center;"> 6.111 </td>
   <td style="text-align:center;"> 0.944 </td>
   <td style="text-align:center;"> 0.254 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-14 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> -3.889 </td>
   <td style="text-align:center;"> 5.000 </td>
   <td style="text-align:center;"> -0.111 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-15 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> -3.889 </td>
   <td style="text-align:center;"> 4.389 </td>
   <td style="text-align:center;"> 0.889 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-16 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> -0.611 </td>
   <td style="text-align:center;"> 7.222 </td>
   <td style="text-align:center;"> 3.556 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-17 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> -4.389 </td>
   <td style="text-align:center;"> 7.778 </td>
   <td style="text-align:center;"> 1.111 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-18 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 18 </td>
   <td style="text-align:center;"> -7.778 </td>
   <td style="text-align:center;"> 8.278 </td>
   <td style="text-align:center;"> -2.667 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-19 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 19 </td>
   <td style="text-align:center;"> -7.778 </td>
   <td style="text-align:center;"> 3.278 </td>
   <td style="text-align:center;"> 0.389 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990-01-20 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 20 </td>
   <td style="text-align:center;"> -2.222 </td>
   <td style="text-align:center;"> 2.222 </td>
   <td style="text-align:center;"> 0.778 </td>
   <td style="text-align:center;"> 0.000 </td>
  </tr>
</tbody>
</table></div>


``` r
dir.create("Yakima")
write.csv(station_list_Yakima,"Yakima/station_list.csv", row.names = FALSE)
write.csv(weather_Yakima[[1]],"Yakima/raw_weather.csv", row.names = FALSE)
write.csv(cleaned_weather_Yakima[[1]],"Yakima/chillR_weather.csv", row.names = FALSE)
```

<!--chapter:end:10-temp-data.Rmd-->

# Filling gaps in temperature records

## Learning goals

-   see why having gaps in records can be quite problematic
-   learn about (too?) simple ways to fill gaps in daily temperature records
-   learn how to use data from auxiliary weather stations to fill gaps in daily temperature records
-   learn about a creative way to close gaps in hourly temperature records

## Gaps

There is a wealth of weather data, but it often contains gaps due to issues like equipment malfunctions, power outages, and storage problems. These gaps pose challenges for modeling agroclimatic conditions, as many scientific methods struggle with missing data. Therefore, effective gap-filling methods are necessary.

## Filling short gaps in daily records

Weather records are mostly complete, though some daily maximum or minimum temperatures may be missing. For short gaps, simple linear interpolation can estimate values by averaging the last known and first known measurements around the gap. This approach can work for gaps of 2-3 days, though accuracy declines with longer gaps. For extended absences of several weeks or more, linear interpolation may miss significant temperature trends, and for gaps as long as a year, it could entirely overlook seasonal patterns, leading to large errors. Nonetheless, the `chillR` package provides a function, `interpolate_gaps()`, to perform this basic interpolation:




``` r
weather <- KA_weather %>% make_all_day_table()

Tmin_int <- interpolate_gaps(weather[,"Tmin"])

weather <- weather %>% mutate(Tmin = Tmin_int$interp,
                              Tmin_interpolated = Tmin_int$missing)

Tmax_int <- interpolate_gaps(weather[,"Tmax"])

weather <- weather %>% mutate(Tmax = Tmax_int$interp,
                              Tmax_interpolated = Tmax_int$missing)
```

The `fix_weather()` function in `chillR` uses linear interpolation to fill gaps in minimum and maximum temperature data by default. If any entire days are missing, it adds rows for these dates using `make_all_day_table()`. Users can also customize the function by setting the range of years (with `start_year` and `end_year`), specifying specific dates (using `start_date` and `end_date` in Julian days), and choosing column names if they differ from `Tmin` and `Tmax`.


``` r
# add an extra day to the KA_weather dataset that is not connected to the days that are already there.
# this creates a large gap, which we can then interpolate
KA_weather_gap <- rbind(KA_weather, c(Year = 2011,
                                      Month = 3,
                                      Day = 3,
                                      Tmax = 26,
                                      Tmin = 14)) 

# fill in the gaps between Julian date 300 (late October) and 100 (early April), only returning data between 2000 and 2011
fixed_winter_days <- KA_weather_gap %>% fix_weather(start_year = 2000,
                                                    end_year = 2011,
                                                    start_date = 300,
                                                    end_date = 100)

# fill in all gaps
fixed_all_days <- KA_weather_gap %>% fix_weather()
```

The `fix_weather()` function returns a list with two components:

1.  `weather`: A `data.frame` containing the interpolated weather data. It includes two additional columns, `no_Tmin` and `no_Tmax`, which mark rows where minimum or maximum temperatures were originally missing (indicated as `TRUE`, otherwise `FALSE`).
2.  `QC:` A quality control object that summarizes the number of interpolated values for each season.

These QC elements provide an overview of the data quality and interpolation extent for each dataset processed:


``` r
fixed_winter_days$QC
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> End_year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Data_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Incomplete_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_complete </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1999/2000 </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 100 </td>
   <td style="text-align:center;"> 66 </td>
   <td style="text-align:center;"> 66 </td>
   <td style="text-align:center;"> 66 </td>
   <td style="text-align:center;"> 60.2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2000/2001 </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2001/2002 </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2002/2003 </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2003/2004 </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2004/2005 </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2005/2006 </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2006/2007 </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008/2009 </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 167 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2009/2010 </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2010/2011 </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 128 </td>
   <td style="text-align:center;"> 165 </td>
   <td style="text-align:center;"> 165 </td>
   <td style="text-align:center;"> 165 </td>
   <td style="text-align:center;"> 0.6 </td>
  </tr>
</tbody>
</table></div>


``` r
fixed_all_days$QC
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> End_year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Data_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Incomplete_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_complete </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1997/1998 </td>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998/1999 </td>
   <td style="text-align:center;"> 1999 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1999/2000 </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2000/2001 </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2001/2002 </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2002/2003 </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2003/2004 </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2004/2005 </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2005/2006 </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2006/2007 </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008/2009 </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2009/2010 </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 214 </td>
   <td style="text-align:center;"> 214 </td>
   <td style="text-align:center;"> 214 </td>
   <td style="text-align:center;"> 41.4 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2010/2011 </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 62 </td>
   <td style="text-align:center;"> 364 </td>
   <td style="text-align:center;"> 364 </td>
   <td style="text-align:center;"> 364 </td>
   <td style="text-align:center;"> 0.3 </td>
  </tr>
</tbody>
</table></div>

As mentioned, linear interpolation works reasonably well for short gaps in data but becomes less reliable as the gaps lengthen. Below is a simple demonstration of this effect:


``` r
gap_weather <- KA_weather[200:305, ]
gap_weather[ ,"Tmin_observed"] <- gap_weather$Tmin
gap_weather$Tmin[c(2, 4:5, 7:9, 11:14, 16:20, 22:27, 29:35, 
                   37:44, 46:54, 56:65, 67:77, 79:90, 92:104)] <- NA
fixed_gaps <- fix_weather(gap_weather)$weather

ggplot(data = fixed_gaps,
       aes(DATE, Tmin_observed)) +
  geom_line(lwd = 1.3) +
  xlab("Date") +
  ylab("Daily minimum temperature (°C)") +
  geom_line(data = fixed_gaps, aes(DATE, Tmin), col = "red", lwd = 1.3)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-175-1.png" width="672" />

The plot illustrates original temperature measurements (in black) alongside interpolated values (in red). To simulate gaps, values were removed incrementally from the dataset - starting with single missing values on the left and increasing up to 13 consecutive missing values on the right. The results show that for shorter gaps (left side), interpolation closely follows the temperature trends. However, as gaps grow longer (right side), the interpolated values deviate more significantly, failing to capture the actual temperature dynamics accurately. This visual demonstrates the diminishing reliability of linear interpolation as gaps increase in size.


``` r
fixed_gaps[,"error"] <- abs(fixed_gaps$Tmin - fixed_gaps$Tmin_observed)

ggplot(data = fixed_gaps,
       aes(DATE, error)) +
  geom_line(lwd = 1.3) +
  xlab("Date") +
  ylab("Error introduced by interpolation (°C)") +
  geom_point(data = fixed_gaps[which(!fixed_gaps$no_Tmin),],
             aes(DATE, error),col = "red", cex = 3)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-176-1.png" width="672" />

The size of interpolation errors depends on temperature variation during the missing periods - high variation leads to larger errors. As gap sizes increase, errors tend to grow, especially in the middle of large gaps, where interpolated values can be far from actual conditions. While errors are zero at points where data exists, larger gaps clearly require a more advanced method for accurate estimation.

## Filling long gaps in daily records

Long gaps in temperature records are a persistent issue because actual temperatures at specific times and locations are unknown if no measurements were taken. While linear interpolation can provide reasonable estimates for short gaps, longer gaps require more reliable approaches. Instead of using complex interpolation algorithms, an effective solution can be to incorporate additional data from nearby weather stations in climatically similar settings.

Typically, if another station close to the target site has a similar climate, its data can be used to fill in gaps. For example, this method is used in the [CIMIS](https://cimis.water.ca.gov/) network in California, where data from nearby stations is often used to address missing values. However, this approach has limitations, as even small differences in elevation or unique landscape features (like lakes, forests, or coastlines) can lead to climate variations that make nearby stations less accurate proxies.

In `chillR`, the `patch_weather()` function addresses these limitations by using data from auxiliary stations to fill gaps. It can detect certain biases, adjust for mean temperature biases, and apply the corrected data to the location of interest, thus providing a more refined way to handle missing temperature records.

To fill gaps in the temperature dataset for Bonn, downloaded in the *Getting temperature data* lesson, the following steps should be taken:


``` r
Bonn <- read.csv("data/Bonn_chillR_weather.csv")
Bonn_QC <- fix_weather(Bonn)$QC
```


``` r
Bonn_QC
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> End_year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Data_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Incomplete_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_complete </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1989/1990 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990/1991 </td>
   <td style="text-align:center;"> 1991 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1991/1992 </td>
   <td style="text-align:center;"> 1992 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1992/1993 </td>
   <td style="text-align:center;"> 1993 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1993/1994 </td>
   <td style="text-align:center;"> 1994 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1994/1995 </td>
   <td style="text-align:center;"> 1995 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1995/1996 </td>
   <td style="text-align:center;"> 1996 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1996/1997 </td>
   <td style="text-align:center;"> 1997 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1997/1998 </td>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 98.9 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998/1999 </td>
   <td style="text-align:center;"> 1999 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1999/2000 </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2000/2001 </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2001/2002 </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2002/2003 </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 316 </td>
   <td style="text-align:center;"> 316 </td>
   <td style="text-align:center;"> 316 </td>
   <td style="text-align:center;"> 13.4 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2003/2004 </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2004/2005 </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2005/2006 </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2006/2007 </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008/2009 </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2009/2010 </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2010/2011 </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2011/2012 </td>
   <td style="text-align:center;"> 2012 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2012/2013 </td>
   <td style="text-align:center;"> 2013 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2013/2014 </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2014/2015 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015/2016 </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2016/2017 </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2017/2018 </td>
   <td style="text-align:center;"> 2018 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2018/2019 </td>
   <td style="text-align:center;"> 2019 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2019/2020 </td>
   <td style="text-align:center;"> 2020 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
</tbody>
</table></div>

The dataset for Bonn has significant gaps between 1998 and 2004, as well as in 2008 (where almost all values are missing), along with shorter gaps in 2015, 2018, and 2020.

To address these gaps, data from nearby weather stations is required. The `handle_gsod()` function can be used to find relevant stations in the surrounding area.


``` r
station_list <- handle_gsod(action = "list_stations",
                            location = c(7.10, 50.73),
                            time_interval = c(1990, 2020))
```


``` r
station_list
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> chillR_code </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STATION.NAME </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> CTRY </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Lat </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Long </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> BEGIN </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> END </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Distance </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Overlap_years </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_interval_covered </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 10517099999 </td>
   <td style="text-align:center;"> BONN/FRIESDORF(AUT) </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.700 </td>
   <td style="text-align:center;"> 7.150 </td>
   <td style="text-align:center;"> 19360102 </td>
   <td style="text-align:center;"> 19921231 </td>
   <td style="text-align:center;"> 4.86 </td>
   <td style="text-align:center;"> 3.00 </td>
   <td style="text-align:center;"> 10 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10518099999 </td>
   <td style="text-align:center;"> BONN-HARDTHOEHE </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.700 </td>
   <td style="text-align:center;"> 7.033 </td>
   <td style="text-align:center;"> 19750523 </td>
   <td style="text-align:center;"> 19971223 </td>
   <td style="text-align:center;"> 5.78 </td>
   <td style="text-align:center;"> 7.98 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10519099999 </td>
   <td style="text-align:center;"> BONN-ROLEBER </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.733 </td>
   <td style="text-align:center;"> 7.200 </td>
   <td style="text-align:center;"> 20010705 </td>
   <td style="text-align:center;"> 20081231 </td>
   <td style="text-align:center;"> 7.05 </td>
   <td style="text-align:center;"> 7.49 </td>
   <td style="text-align:center;"> 24 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10513099999 </td>
   <td style="text-align:center;"> KOLN BONN </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.866 </td>
   <td style="text-align:center;"> 7.143 </td>
   <td style="text-align:center;"> 19310101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 15.44 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10509099999 </td>
   <td style="text-align:center;"> BUTZWEILERHOF(BAFB) </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.983 </td>
   <td style="text-align:center;"> 6.900 </td>
   <td style="text-align:center;"> 19780901 </td>
   <td style="text-align:center;"> 19950823 </td>
   <td style="text-align:center;"> 31.48 </td>
   <td style="text-align:center;"> 5.64 </td>
   <td style="text-align:center;"> 18 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10502099999 </td>
   <td style="text-align:center;"> NORVENICH </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.831 </td>
   <td style="text-align:center;"> 6.658 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 33.08 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10514099999 </td>
   <td style="text-align:center;"> MENDIG </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.366 </td>
   <td style="text-align:center;"> 7.315 </td>
   <td style="text-align:center;"> 19730102 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 43.28 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10506099999 </td>
   <td style="text-align:center;"> NUERBURG-BARWEILER </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.367 </td>
   <td style="text-align:center;"> 6.867 </td>
   <td style="text-align:center;"> 19950401 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 43.64 </td>
   <td style="text-align:center;"> 2.75 </td>
   <td style="text-align:center;"> 9 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10508099999 </td>
   <td style="text-align:center;"> BLANKENHEIM </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.450 </td>
   <td style="text-align:center;"> 6.650 </td>
   <td style="text-align:center;"> 19781002 </td>
   <td style="text-align:center;"> 19840504 </td>
   <td style="text-align:center;"> 44.53 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10510099999 </td>
   <td style="text-align:center;"> NUERBURG </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.333 </td>
   <td style="text-align:center;"> 6.950 </td>
   <td style="text-align:center;"> 19300901 </td>
   <td style="text-align:center;"> 19921231 </td>
   <td style="text-align:center;"> 45.45 </td>
   <td style="text-align:center;"> 3.00 </td>
   <td style="text-align:center;"> 10 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10515099999 </td>
   <td style="text-align:center;"> BENDORF </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.417 </td>
   <td style="text-align:center;"> 7.583 </td>
   <td style="text-align:center;"> 19310102 </td>
   <td style="text-align:center;"> 20030816 </td>
   <td style="text-align:center;"> 48.79 </td>
   <td style="text-align:center;"> 13.62 </td>
   <td style="text-align:center;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10504099999 </td>
   <td style="text-align:center;"> EIFEL </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.650 </td>
   <td style="text-align:center;"> 6.283 </td>
   <td style="text-align:center;"> 20040501 </td>
   <td style="text-align:center;"> 20040501 </td>
   <td style="text-align:center;"> 58.30 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10526099999 </td>
   <td style="text-align:center;"> BAD MARIENBERG </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.667 </td>
   <td style="text-align:center;"> 7.967 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20030816 </td>
   <td style="text-align:center;"> 61.54 </td>
   <td style="text-align:center;"> 13.62 </td>
   <td style="text-align:center;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10613099999 </td>
   <td style="text-align:center;"> BUCHEL </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.174 </td>
   <td style="text-align:center;"> 7.063 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 61.95 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10503099999 </td>
   <td style="text-align:center;"> AACHEN/MERZBRUCK </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.817 </td>
   <td style="text-align:center;"> 6.183 </td>
   <td style="text-align:center;"> 19780901 </td>
   <td style="text-align:center;"> 19971212 </td>
   <td style="text-align:center;"> 65.28 </td>
   <td style="text-align:center;"> 7.95 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10419099999 </td>
   <td style="text-align:center;"> LUDENSCHEID       &amp; </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.233 </td>
   <td style="text-align:center;"> 7.600 </td>
   <td style="text-align:center;"> 19270906 </td>
   <td style="text-align:center;"> 20030306 </td>
   <td style="text-align:center;"> 66.06 </td>
   <td style="text-align:center;"> 13.18 </td>
   <td style="text-align:center;"> 43 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10400099999 </td>
   <td style="text-align:center;"> DUSSELDORF </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.289 </td>
   <td style="text-align:center;"> 6.767 </td>
   <td style="text-align:center;"> 19310102 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 66.46 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10616299999 </td>
   <td style="text-align:center;"> SIEGERLAND </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.708 </td>
   <td style="text-align:center;"> 8.083 </td>
   <td style="text-align:center;"> 20040510 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 69.33 </td>
   <td style="text-align:center;"> 16.65 </td>
   <td style="text-align:center;"> 54 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10418099999 </td>
   <td style="text-align:center;"> LUEDENSCHEID </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.250 </td>
   <td style="text-align:center;"> 7.650 </td>
   <td style="text-align:center;"> 19940301 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 69.54 </td>
   <td style="text-align:center;"> 3.84 </td>
   <td style="text-align:center;"> 12 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10437499999 </td>
   <td style="text-align:center;"> MONCHENGLADBACH </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.230 </td>
   <td style="text-align:center;"> 6.504 </td>
   <td style="text-align:center;"> 19960715 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 69.59 </td>
   <td style="text-align:center;"> 24.47 </td>
   <td style="text-align:center;"> 79 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10403099999 </td>
   <td style="text-align:center;"> MOENCHENGLADBACH </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.233 </td>
   <td style="text-align:center;"> 6.500 </td>
   <td style="text-align:center;"> 19381001 </td>
   <td style="text-align:center;"> 19421031 </td>
   <td style="text-align:center;"> 70.03 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10501099999 </td>
   <td style="text-align:center;"> AACHEN </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 50.783 </td>
   <td style="text-align:center;"> 6.100 </td>
   <td style="text-align:center;"> 19280101 </td>
   <td style="text-align:center;"> 20030816 </td>
   <td style="text-align:center;"> 70.67 </td>
   <td style="text-align:center;"> 13.62 </td>
   <td style="text-align:center;"> 44 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 06496099999 </td>
   <td style="text-align:center;"> ELSENBORN (MIL) </td>
   <td style="text-align:center;"> BE </td>
   <td style="text-align:center;"> 50.467 </td>
   <td style="text-align:center;"> 6.183 </td>
   <td style="text-align:center;"> 19840501 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 71.10 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 06495099999 </td>
   <td style="text-align:center;"> BOTRANGE (MOUNT) </td>
   <td style="text-align:center;"> BE </td>
   <td style="text-align:center;"> 50.500 </td>
   <td style="text-align:center;"> 6.100 </td>
   <td style="text-align:center;"> 19510201 </td>
   <td style="text-align:center;"> 20011015 </td>
   <td style="text-align:center;"> 75.13 </td>
   <td style="text-align:center;"> 11.79 </td>
   <td style="text-align:center;"> 38 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10409099999 </td>
   <td style="text-align:center;"> ESSEN/MUELHEIM </td>
   <td style="text-align:center;"> GM </td>
   <td style="text-align:center;"> 51.400 </td>
   <td style="text-align:center;"> 6.967 </td>
   <td style="text-align:center;"> 19300414 </td>
   <td style="text-align:center;"> 19431231 </td>
   <td style="text-align:center;"> 75.17 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
</tbody>
</table></div>

Many of the stations listed may not be useful, as they only overlap with the existing record for a few years, or not at all. As a result, it's unlikely that any single station will be able to fill all the gaps in Bonn’s temperature data. However, by combining data from multiple auxiliary stations, it may be possible to fill in the missing values. Promising stations include **BONN-HARDTHOEHE**, **BONN-ROLEBER**, and **NORVENICH**. These stations will be downloaded and stored in a list.

In `chillR` version 0.74 and later, the `handle_gsod()` function can download multiple station records at once, returning them as a named list. This function will be used to download the records for the selected stations (positions 2, 3, and 6 in the station list).


``` r
patch_weather <-
      handle_gsod(action = "download_weather",
                  location = as.character(station_list$chillR_code[c(2, 3, 6)]),
                  time_interval = c(1990, 2020)) %>%
  handle_gsod()
```

```
## Loading data for 31 years from station 'NORVENICH'
## ===============================================================================================
## 
## Loading data for 31 years from station 'BONN-HARDTHOEHE'
## ===============================================================================================
## 
## Loading data for 31 years from station 'BONN-ROLEBER'
## ===============================================================================================
```

With the list of potentially useful weather records now available, the next step is to use the `patch_daily_temperatures()` function. This function will integrate the data from the selected auxiliary stations to fill the missing temperature values in the Bonn dataset:


``` r
patched <- patch_daily_temperatures(weather = Bonn,
                                    patch_weather = patch_weather)
```

The results can be reviewed by examining the statistics element of the patched object, accessed using `patched$statistics`. This will provide an overview of how the gaps were filled and the adjustments made using the auxiliary station data.


``` r
# Patch statistics for NORVENICH
patched$statistics[[1]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -0.307 </td>
   <td style="text-align:center;"> 1.304 </td>
   <td style="text-align:center;"> 2146 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 0.202 </td>
   <td style="text-align:center;"> 1.154 </td>
   <td style="text-align:center;"> 2146 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>


``` r
# Patch statistics for BONN-HARDTHOEHE
patched$statistics[[2]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -1.871 </td>
   <td style="text-align:center;"> 2.080 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 1.466 </td>
   <td style="text-align:center;"> 1.427 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>


``` r
# Patch statistics for BONN-ROLEBER
patched$statistics[[3]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -0.546 </td>
   <td style="text-align:center;"> 1.186 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 1.314 </td>
   <td style="text-align:center;"> 1.089 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>

The analysis provides insight into the similarity between the temperature records from the auxiliary stations and the target station in Bonn, specifically for both `Tmin` and `Tmax`. It includes the following statistics:

1.  `filled`: The number of days for which data was successfully transferred from each auxiliary station.
2.  `gaps_remain`: The number of gaps still present after the patching process.

Additionally, two quality statistics are provided:

-   **Mean Bias (**`mean_bias`**)**: The average temperature difference between the auxiliary station and the Bonn station. This can be easily addressed by adjusting daily temperature values when transferring data between stations, and the `patch_daily_temperatures()` function automatically corrects for this.

-   **Standard Deviation of Daily Differences (**`stdev_bias`**)**: This indicates the variability in the differences between the stations. A high stdev_bias suggests that the temperature differences are not systematic and may not be easily corrected. If the stdev_bias exceeds a certain threshold, it may be best to exclude that station from the data transfer.

To address these metrics, limits can be set for both. The `mean_bias` can be capped at 1°C, and the `stdev_bias` can be capped at 2°C. These thresholds will be passed as parameters (`max_mean_bias` and `max_stdev_bias`) to the `patch_daily_temperatures()` function. After setting these limits, the statistics should be reviewed again to ensure the quality of the patching process.


``` r
patched <- patch_daily_temperatures(weather = Bonn,
                                    patch_weather = patch_weather,
                                    max_mean_bias = 1,
                                    max_stdev_bias = 2)
```


``` r
# Patch statistics for NORVENICH
patched$statistics[[1]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -0.307 </td>
   <td style="text-align:center;"> 1.304 </td>
   <td style="text-align:center;"> 2146 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 0.202 </td>
   <td style="text-align:center;"> 1.154 </td>
   <td style="text-align:center;"> 2146 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>


``` r
# Patch statistics for BONN-HARDTHOEHE
patched$statistics[[2]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -1.871 </td>
   <td style="text-align:center;"> 2.080 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 1.466 </td>
   <td style="text-align:center;"> 1.427 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>


``` r
# Patch statistics for BONN-ROLEBER
patched$statistics[[3]]
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">  </th>
   <th style="text-align:center;"> mean_bias </th>
   <th style="text-align:center;"> stdev_bias </th>
   <th style="text-align:center;"> filled </th>
   <th style="text-align:center;"> gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Tmin </td>
   <td style="text-align:center;"> -0.546 </td>
   <td style="text-align:center;"> 1.186 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Tmax </td>
   <td style="text-align:center;"> 1.314 </td>
   <td style="text-align:center;"> 1.089 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
</tbody>
</table>

After applying the filters, all records from **BONN-HARDTHOEHE** and the `Tmax` records from **BONN-ROLEBER** were rejected because they did not meet the mean_bias threshold. However, the data from **NORVENICH** were deemed suitable, allowing us to fill 2,146 gaps for both `Tmin` and `Tmax`, leaving just 1 gap remaining for each.

To identify where the remaining gaps are, the next step is to use the `fix_weather()` function. This will allow us to examine the dataset and pinpoint the exact locations of the remaining gaps in both `Tmin` and `Tmax`.


``` r
post_patch_stats <- fix_weather(patched)$QC
```


``` r
post_patch_stats
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> End_year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Data_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Incomplete_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_complete </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1989/1990 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990/1991 </td>
   <td style="text-align:center;"> 1991 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1991/1992 </td>
   <td style="text-align:center;"> 1992 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1992/1993 </td>
   <td style="text-align:center;"> 1993 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1993/1994 </td>
   <td style="text-align:center;"> 1994 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1994/1995 </td>
   <td style="text-align:center;"> 1995 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1995/1996 </td>
   <td style="text-align:center;"> 1996 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1996/1997 </td>
   <td style="text-align:center;"> 1997 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1997/1998 </td>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998/1999 </td>
   <td style="text-align:center;"> 1999 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 99.7 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1999/2000 </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2000/2001 </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2001/2002 </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2002/2003 </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2003/2004 </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2004/2005 </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2005/2006 </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2006/2007 </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008/2009 </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2009/2010 </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2010/2011 </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2011/2012 </td>
   <td style="text-align:center;"> 2012 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2012/2013 </td>
   <td style="text-align:center;"> 2013 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2013/2014 </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2014/2015 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015/2016 </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2016/2017 </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2017/2018 </td>
   <td style="text-align:center;"> 2018 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2018/2019 </td>
   <td style="text-align:center;"> 2019 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2019/2020 </td>
   <td style="text-align:center;"> 2020 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100.0 </td>
  </tr>
</tbody>
</table></div>

After patching the dataset, only a single day's data remains missing, which is a very short gap. Given its small size, it is reasonable to use linear interpolation to fill this remaining gap. The `fix_weather()` function can be used to interpolate this final missing value and complete the dataset.


``` r
Bonn_weather <- fix_weather(patched)
```

### Bias-correction for shorter intervals

In the `patch_daily_temperatures()` function, the bias correction is typically based on the average temperature difference between two weather stations over the entire year. However, this approach assumes that the bias between stations is constant throughout the year, which may not be true. In reality, the bias can vary across different seasons, meaning a station might be a good proxy for temperature data during certain times of the year but not others.

To address this, the `patch_daily_temps()` function (note the slight name difference) allows for seasonally adjusted bias correction. By default, this function evaluates temperature data on a monthly basis, making separate comparisons for each calendar month. It can then assess whether an auxiliary station is a reliable proxy for temperatures in each specific month and apply month-specific bias corrections, leading to more accurate estimations with smaller biases than if the entire year were used for comparison.


``` r
patched_monthly <- patch_daily_temps(weather = Bonn,
                                     patch_weather = patch_weather,
                                     max_mean_bias = 1,
                                     max_stdev_bias = 2,
                                     time_interval = "month")
```

The findings for minimum temperatures from the **NORVENICH** station can be summarized as follows:


``` r
patched_monthly$statistics$Tmin$NORVENICH
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; "><table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Interval </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Total_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Overlap_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Mean_bias </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Stdev_bias </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Gaps_before </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Filled </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Gaps_remain </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 773 </td>
   <td style="text-align:center;"> 0.184 </td>
   <td style="text-align:center;"> 1.260 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 185 </td>
   <td style="text-align:center;"> 1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 774 </td>
   <td style="text-align:center;"> 0.281 </td>
   <td style="text-align:center;"> 1.242 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 876 </td>
   <td style="text-align:center;"> 706 </td>
   <td style="text-align:center;"> 0.269 </td>
   <td style="text-align:center;"> 1.248 </td>
   <td style="text-align:center;"> 170 </td>
   <td style="text-align:center;"> 170 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 775 </td>
   <td style="text-align:center;"> 0.253 </td>
   <td style="text-align:center;"> 1.427 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 930 </td>
   <td style="text-align:center;"> 758 </td>
   <td style="text-align:center;"> 0.509 </td>
   <td style="text-align:center;"> 1.431 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 166 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 801 </td>
   <td style="text-align:center;"> 0.373 </td>
   <td style="text-align:center;"> 1.238 </td>
   <td style="text-align:center;"> 158 </td>
   <td style="text-align:center;"> 158 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> 930 </td>
   <td style="text-align:center;"> 749 </td>
   <td style="text-align:center;"> 0.396 </td>
   <td style="text-align:center;"> 1.210 </td>
   <td style="text-align:center;"> 180 </td>
   <td style="text-align:center;"> 180 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 781 </td>
   <td style="text-align:center;"> 0.480 </td>
   <td style="text-align:center;"> 1.305 </td>
   <td style="text-align:center;"> 179 </td>
   <td style="text-align:center;"> 179 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 774 </td>
   <td style="text-align:center;"> 0.529 </td>
   <td style="text-align:center;"> 1.302 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> 930 </td>
   <td style="text-align:center;"> 750 </td>
   <td style="text-align:center;"> 0.205 </td>
   <td style="text-align:center;"> 1.264 </td>
   <td style="text-align:center;"> 180 </td>
   <td style="text-align:center;"> 180 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> 961 </td>
   <td style="text-align:center;"> 775 </td>
   <td style="text-align:center;"> 0.098 </td>
   <td style="text-align:center;"> 1.307 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 186 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> 930 </td>
   <td style="text-align:center;"> 745 </td>
   <td style="text-align:center;"> 0.101 </td>
   <td style="text-align:center;"> 1.308 </td>
   <td style="text-align:center;"> 184 </td>
   <td style="text-align:center;"> 184 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
</tbody>
</table></div>

The analysis shows that the **mean bias** between the stations varies significantly throughout the year, indicating that a month-specific bias correction would likely improve the accuracy of the temperature data.

To implement this, the `time_interval` parameter in the `patch_daily_temps()` function allows for flexibility in the interval used for bias correction. Intervals can be set to `month`, `week`, or even custom durations like `10 days` or `2 weeks`. The function will start counting these intervals from January 1st of each year, which might result in shorter intervals toward the end of the year. This can generate warnings if the final interval is smaller than the selected period.

However, it's important to keep in mind that using smaller intervals reduces the amount of data available for bias determination. For short time series, very short intervals may not provide enough data, which could reduce the reliability of the bias correction. Therefore, selecting an appropriate interval size is crucial to balancing accuracy and data availability.


``` r
patched_2weeks <- patch_daily_temps(weather = Bonn,
                                    patch_weather = patch_weather,
                                    max_mean_bias = 1,
                                    max_stdev_bias = 2,
                                    time_interval = "2 weeks")
```

To demonstrate the effects, 5000 gaps will be created in the Bonn weather record and filled with proxy data using annual, monthly, and bi-weekly intervals for bias evaluation. The resulting errors will be visualized with a violin plot using `ggplot2`.


``` r
Gaps <- sample(seq(1:nrow(Bonn)), size = 5000, replace = FALSE)

Bonn_gaps <- Bonn %>% mutate(obs_Tmin=Tmin,
                             obs_Tmax=Tmax)
Bonn_gaps$Tmin[Gaps] <- NA
Bonn_gaps$Tmax[Gaps] <- NA

patch_annual <- patch_daily_temps(weather = Bonn_gaps,
                                  patch_weather = patch_weather,
                                  max_mean_bias = 1,
                                  max_stdev_bias = 2,
                                  time_interval = "year")
patch_month <- patch_daily_temps(weather = Bonn_gaps,
                                 patch_weather = patch_weather,
                                 max_mean_bias = 1,
                                 max_stdev_bias = 2,
                                 time_interval = "month")
patch_2weeks <- patch_daily_temps(weather = Bonn_gaps,
                                  patch_weather = patch_weather,
                                  max_mean_bias = 1,
                                  max_stdev_bias = 2,
                                  time_interval = "2 weeks")

Bonn_gaps[,"Tmin_annual"] <- Bonn_gaps$obs_Tmin - patch_annual$weather$Tmin
Bonn_gaps[,"Tmax_annual"] <- Bonn_gaps$obs_Tmax - patch_annual$weather$Tmax
Bonn_gaps[,"Tmin_month"] <- Bonn_gaps$obs_Tmin - patch_month$weather$Tmin
Bonn_gaps[,"Tmax_month"] <- Bonn_gaps$obs_Tmax - patch_month$weather$Tmax
Bonn_gaps[,"Tmin_2weeks"] <- Bonn_gaps$obs_Tmin - patch_2weeks$weather$Tmin
Bonn_gaps[,"Tmax_2weeks"] <- Bonn_gaps$obs_Tmax - patch_2weeks$weather$Tmax

Interval_eval <- Bonn_gaps %>%
  filter(is.na(Tmin)) %>%
  pivot_longer(Tmin_annual:Tmax_2weeks) %>%
  mutate(Type=factor(name,
                     levels = c("Tmin_annual",
                                "Tmin_month",
                                "Tmin_2weeks",
                                "Tmax_annual",
                                "Tmax_month",
                                "Tmax_2weeks")) )

ggplot(Interval_eval,
       aes(Type,value)) +
  geom_violin(draw_quantiles = c(0.25,0.5,0.75)) +
  xlab("Variable and bias evaluation interval") +
  ylab("Prediction error")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-206-1.png" width="672" />

It is also possible to evaluate the mean daily error:


``` r
error_eval <-
  data.frame(Variable = c(rep("Tmin",3),rep("Tmax",3)),
             Interval = rep(c("Year","Month","Two weeks"),2),
             Error = c(
             mean(abs(Bonn_gaps$Tmin_annual[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE),
             mean(abs(Bonn_gaps$Tmin_month[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE),
             mean(abs(Bonn_gaps$Tmin_2weeks[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE),
             mean(abs(Bonn_gaps$Tmax_annual[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE),
             mean(abs(Bonn_gaps$Tmax_month[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE),
             mean(abs(Bonn_gaps$Tmax_2weeks[is.na(Bonn_gaps$Tmin)]),na.rm=TRUE))
             )
```


``` r
error_eval
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Variable </th>
   <th style="text-align:center;"> Interval </th>
   <th style="text-align:center;"> Error </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> Tmin </td>
   <td style="text-align:center;"> Year </td>
   <td style="text-align:center;"> 0.9893948 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Tmin </td>
   <td style="text-align:center;"> Month </td>
   <td style="text-align:center;"> 0.9840705 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Tmin </td>
   <td style="text-align:center;"> Two weeks </td>
   <td style="text-align:center;"> 0.9856762 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Tmax </td>
   <td style="text-align:center;"> Year </td>
   <td style="text-align:center;"> 0.8432714 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Tmax </td>
   <td style="text-align:center;"> Month </td>
   <td style="text-align:center;"> 0.8198862 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> Tmax </td>
   <td style="text-align:center;"> Two weeks </td>
   <td style="text-align:center;"> 0.8214015 </td>
  </tr>
</tbody>
</table>

The improvement in the results was not very significant, likely because the stations used are relatively close to each other, and the weather conditions between them do not vary much.

### Saving the data for later

The dataset based on monthly intervals should be saved for later use. Before saving, the remaining missing day needs to be interpolated. Once this gap is filled, the dataset can be stored for future use.


``` r
monthly_bias_fixed <- fix_weather(patched_monthly)
```

The long-term record for Bonn, covering the period from 1990 to 2020, is now complete with no remaining gaps. This dataset can now be saved for future use.


``` r
write.csv(monthly_bias_fixed$weather,
          "data/Bonn_weather.csv")
```

Only the weather element, a `data.frame`, was saved, as it can be easily exported as a spreadsheet (`.csv` file). While it is also possible to save lists, such as the `QC` element, this requires a more complex process, so it will be saved at a later time.

## `Exercises` on filling gaps

1.  *Use* `chillR` *functions to find out how many gaps you have in your dataset (even if you have none, please still follow all further steps)*


``` r
Yakima <- read.csv("Yakima/chillR_weather.csv")
Yakima_QC <- fix_weather(Yakima)$QC
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> End_year </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Season_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Data_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmin </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Missing_Tmax </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Incomplete_days </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_complete </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1989/1990 </td>
   <td style="text-align:center;"> 1990 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1990/1991 </td>
   <td style="text-align:center;"> 1991 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1991/1992 </td>
   <td style="text-align:center;"> 1992 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1992/1993 </td>
   <td style="text-align:center;"> 1993 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1993/1994 </td>
   <td style="text-align:center;"> 1994 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1994/1995 </td>
   <td style="text-align:center;"> 1995 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1995/1996 </td>
   <td style="text-align:center;"> 1996 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1996/1997 </td>
   <td style="text-align:center;"> 1997 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1997/1998 </td>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998/1999 </td>
   <td style="text-align:center;"> 1999 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1999/2000 </td>
   <td style="text-align:center;"> 2000 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2000/2001 </td>
   <td style="text-align:center;"> 2001 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2001/2002 </td>
   <td style="text-align:center;"> 2002 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2002/2003 </td>
   <td style="text-align:center;"> 2003 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2003/2004 </td>
   <td style="text-align:center;"> 2004 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2004/2005 </td>
   <td style="text-align:center;"> 2005 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2005/2006 </td>
   <td style="text-align:center;"> 2006 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2006/2007 </td>
   <td style="text-align:center;"> 2007 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2007/2008 </td>
   <td style="text-align:center;"> 2008 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2008/2009 </td>
   <td style="text-align:center;"> 2009 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2009/2010 </td>
   <td style="text-align:center;"> 2010 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2010/2011 </td>
   <td style="text-align:center;"> 2011 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2011/2012 </td>
   <td style="text-align:center;"> 2012 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2012/2013 </td>
   <td style="text-align:center;"> 2013 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2013/2014 </td>
   <td style="text-align:center;"> 2014 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2014/2015 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015/2016 </td>
   <td style="text-align:center;"> 2016 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2016/2017 </td>
   <td style="text-align:center;"> 2017 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2017/2018 </td>
   <td style="text-align:center;"> 2018 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2018/2019 </td>
   <td style="text-align:center;"> 2019 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 365 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2019/2020 </td>
   <td style="text-align:center;"> 2020 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 366 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
</tbody>
</table></div>

2.  *Create a list of the 25 closest weather stations using the* `handle_gsod` *function*


``` r
station_list_Yakima <- handle_gsod(action = "list_stations",
                                   location = c(long = -120.50, lat = 46.60),
                                   time_interval = c(1990, 2020))
```

<div style="border: 1px solid #ddd; padding: 0px; overflow-y: scroll; height:300px; overflow-x: scroll; width:100%; "><table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> chillR_code </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> STATION.NAME </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> CTRY </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Lat </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Long </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> BEGIN </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> END </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Distance </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Overlap_years </th>
   <th style="text-align:center;position: sticky; top:0; background-color: #FFFFFF;"> Perc_interval_covered </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 72781024243 </td>
   <td style="text-align:center;"> YAKIMA AIR TERMINAL/MCALSR FIELD AP </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.564 </td>
   <td style="text-align:center;"> -120.535 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 4.82 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924243 </td>
   <td style="text-align:center;"> YAKIMA AIR TERMINAL </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.568 </td>
   <td style="text-align:center;"> -120.543 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19721231 </td>
   <td style="text-align:center;"> 4.85 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781399999 </td>
   <td style="text-align:center;"> VAGABOND AAF / YAKIMA TRAINING CENTER WASHINGTON USA </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.667 </td>
   <td style="text-align:center;"> -120.454 </td>
   <td style="text-align:center;"> 20030617 </td>
   <td style="text-align:center;"> 20081110 </td>
   <td style="text-align:center;"> 8.25 </td>
   <td style="text-align:center;"> 5.40 </td>
   <td style="text-align:center;"> 17 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72056299999 </td>
   <td style="text-align:center;"> RANGE OP 13 / YAKIMA TRAINING CENTER </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.800 </td>
   <td style="text-align:center;"> -120.167 </td>
   <td style="text-align:center;"> 20080530 </td>
   <td style="text-align:center;"> 20170920 </td>
   <td style="text-align:center;"> 33.79 </td>
   <td style="text-align:center;"> 9.31 </td>
   <td style="text-align:center;"> 30 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788399999 </td>
   <td style="text-align:center;"> BOWERS FLD </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.033 </td>
   <td style="text-align:center;"> -120.531 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 48.26 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788324220 </td>
   <td style="text-align:center;"> BOWERS FIELD AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.034 </td>
   <td style="text-align:center;"> -120.531 </td>
   <td style="text-align:center;"> 19880106 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 48.37 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924220 </td>
   <td style="text-align:center;"> ELLENSBURG BOWERS FI </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.034 </td>
   <td style="text-align:center;"> -120.530 </td>
   <td style="text-align:center;"> 19480601 </td>
   <td style="text-align:center;"> 19550101 </td>
   <td style="text-align:center;"> 48.37 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784094187 </td>
   <td style="text-align:center;"> HANFORD AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.567 </td>
   <td style="text-align:center;"> -119.600 </td>
   <td style="text-align:center;"> 20060101 </td>
   <td style="text-align:center;"> 20130326 </td>
   <td style="text-align:center;"> 68.96 </td>
   <td style="text-align:center;"> 7.23 </td>
   <td style="text-align:center;"> 23 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784099999 </td>
   <td style="text-align:center;"> HANFORD </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.567 </td>
   <td style="text-align:center;"> -119.600 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 68.96 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782594239 </td>
   <td style="text-align:center;"> PANGBORN MEMORIAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.397 </td>
   <td style="text-align:center;"> -120.201 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 91.58 </td>
   <td style="text-align:center;"> 21.00 </td>
   <td style="text-align:center;"> 68 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782599999 </td>
   <td style="text-align:center;"> PANGBORN MEM </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.399 </td>
   <td style="text-align:center;"> -120.207 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 91.69 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72788499999 </td>
   <td style="text-align:center;"> RICHLAND AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.306 </td>
   <td style="text-align:center;"> -119.304 </td>
   <td style="text-align:center;"> 19810203 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 97.39 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72781524237 </td>
   <td style="text-align:center;"> STAMPASS PASS FLTWO </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.277 </td>
   <td style="text-align:center;"> -121.337 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 98.63 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924237 </td>
   <td style="text-align:center;"> STAMPEDE PASS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.277 </td>
   <td style="text-align:center;"> -121.337 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19721231 </td>
   <td style="text-align:center;"> 98.63 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72790024141 </td>
   <td style="text-align:center;"> EPHRATA MUNICIPAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.516 </td>
   <td style="text-align:center;"> 20050101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 108.64 </td>
   <td style="text-align:center;"> 16.00 </td>
   <td style="text-align:center;"> 52 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782624141 </td>
   <td style="text-align:center;"> EPHRATA MUNICIPAL </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.515 </td>
   <td style="text-align:center;"> 19420101 </td>
   <td style="text-align:center;"> 19971231 </td>
   <td style="text-align:center;"> 108.69 </td>
   <td style="text-align:center;"> 8.00 </td>
   <td style="text-align:center;"> 26 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924141 </td>
   <td style="text-align:center;"> EPHRATA AP FCWOS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.308 </td>
   <td style="text-align:center;"> -119.515 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19550101 </td>
   <td style="text-align:center;"> 108.69 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782724110 </td>
   <td style="text-align:center;"> GRANT COUNTY INTL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.193 </td>
   <td style="text-align:center;"> -119.315 </td>
   <td style="text-align:center;"> 19430610 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 111.73 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72782799999 </td>
   <td style="text-align:center;"> MOSES LAKE/GRANT CO </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 47.200 </td>
   <td style="text-align:center;"> -119.317 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 112.06 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784524163 </td>
   <td style="text-align:center;"> TRI-CITIES AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.270 </td>
   <td style="text-align:center;"> -119.118 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250210 </td>
   <td style="text-align:center;"> 112.21 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72784599999 </td>
   <td style="text-align:center;"> TRI CITIES </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.267 </td>
   <td style="text-align:center;"> -119.117 </td>
   <td style="text-align:center;"> 20000101 </td>
   <td style="text-align:center;"> 20031231 </td>
   <td style="text-align:center;"> 112.40 </td>
   <td style="text-align:center;"> 4.00 </td>
   <td style="text-align:center;"> 13 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924163 </td>
   <td style="text-align:center;"> PASCO NAS </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 46.267 </td>
   <td style="text-align:center;"> -119.117 </td>
   <td style="text-align:center;"> 19450401 </td>
   <td style="text-align:center;"> 19460601 </td>
   <td style="text-align:center;"> 112.40 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72698824219 </td>
   <td style="text-align:center;"> MUNICIPAL AIRPORT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.619 </td>
   <td style="text-align:center;"> -121.166 </td>
   <td style="text-align:center;"> 19730101 </td>
   <td style="text-align:center;"> 20250209 </td>
   <td style="text-align:center;"> 120.70 </td>
   <td style="text-align:center;"> 31.00 </td>
   <td style="text-align:center;"> 100 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 99999924219 </td>
   <td style="text-align:center;"> THE DALLES MUNICIPAL ARPT </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.619 </td>
   <td style="text-align:center;"> -121.166 </td>
   <td style="text-align:center;"> 19480101 </td>
   <td style="text-align:center;"> 19650101 </td>
   <td style="text-align:center;"> 120.70 </td>
   <td style="text-align:center;"> 0.00 </td>
   <td style="text-align:center;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 72688399999 </td>
   <td style="text-align:center;"> HERMISTON MUNI </td>
   <td style="text-align:center;"> US </td>
   <td style="text-align:center;"> 45.828 </td>
   <td style="text-align:center;"> -119.259 </td>
   <td style="text-align:center;"> 19980514 </td>
   <td style="text-align:center;"> 20051231 </td>
   <td style="text-align:center;"> 128.55 </td>
   <td style="text-align:center;"> 7.64 </td>
   <td style="text-align:center;"> 25 </td>
  </tr>
</tbody>
</table></div>

3.  *Identify suitable weather stations for patching gaps*
4.  *Download weather data for promising stations, convert them to* `chillR` *format and compile them in a list*


``` r
patch_weather <-
  handle_gsod(action = "download_weather",
              location = as.character(station_list_Yakima$chillR_code[c(4, 6, 8)]),
              time_interval = c(1990, 2020)) %>%
  handle_gsod()
```

```
## Loading data for 31 years from station 'RANGE OP 13 / YAKIMA TRAINING CENTER'
## ===============================================================================================
## 
## Loading data for 31 years from station 'HANFORD AIRPORT'
## ===============================================================================================
## 
## Loading data for 31 years from station 'BOWERS FIELD AIRPORT'
## ===============================================================================================
```

5.  *Use the* `patch_daily_temperatures` *function to fill gaps*

    
    ``` r
    patched <- patch_daily_temperatures(weather = Yakima,
                                        patch_weather = patch_weather)
    ```

    
    ``` r
    # Patch statistics for YRANGE OP 13 /AKIMA TRAINING CENTER
    patched$statistics[[1]]
    ```

    <table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
     <thead>
      <tr>
       <th style="text-align:left;">  </th>
       <th style="text-align:center;"> mean_bias </th>
       <th style="text-align:center;"> stdev_bias </th>
       <th style="text-align:center;"> filled </th>
       <th style="text-align:center;"> gaps_remain </th>
      </tr>
     </thead>
    <tbody>
      <tr>
       <td style="text-align:left;"> Tmin </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
      <tr>
       <td style="text-align:left;"> Tmax </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
    </tbody>
    </table>

    
    ``` r
    # Patch statistics for HANFORD AIRPORT
    patched$statistics[[2]]
    ```

    <table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
     <thead>
      <tr>
       <th style="text-align:left;">  </th>
       <th style="text-align:center;"> mean_bias </th>
       <th style="text-align:center;"> stdev_bias </th>
       <th style="text-align:center;"> filled </th>
       <th style="text-align:center;"> gaps_remain </th>
      </tr>
     </thead>
    <tbody>
      <tr>
       <td style="text-align:left;"> Tmin </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
      <tr>
       <td style="text-align:left;"> Tmax </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
    </tbody>
    </table>

    
    ``` r
    # Patch statistics for BOWERS FIELD AIRPORT
    patched$statistics[[3]]
    ```

    <table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
     <thead>
      <tr>
       <th style="text-align:left;">  </th>
       <th style="text-align:center;"> mean_bias </th>
       <th style="text-align:center;"> stdev_bias </th>
       <th style="text-align:center;"> filled </th>
       <th style="text-align:center;"> gaps_remain </th>
      </tr>
     </thead>
    <tbody>
      <tr>
       <td style="text-align:left;"> Tmin </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
      <tr>
       <td style="text-align:left;"> Tmax </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
       <td style="text-align:center;"> NA </td>
      </tr>
    </tbody>
    </table>

6.  *Investigate the results - have all gaps been filled?*


``` r
write.csv(patched$weather,
          "Yakima/Yakima_weather.csv", row.names = FALSE)
```

<!--chapter:end:11-gaps.Rmd-->

# Generating temperature scenarios

## Learning goals

-   Understand what a weather generator is, (roughly) how it works and why it is useful for planning
-   Learn how to run the `temperature_generation` function included in `chillR`
-   Be able to produce chill profiles for a place of interest using histograms and cumulative distributions
-   Understand what Safe Winter Chill is and be able to calculate it

## Chill scenarios

The main goal so far has been to understand chill availability and other agroclimatic conditions at specific sites, which is essential for orchard managers choosing tree species and cultivars. While historical data has been helpful, growers need more tailored, site-specific information. They need a forecast of likely conditions - such as expected chill or heat levels - to make better planting decisions.

## Risk assessment in orchard planning

Because trees are long-lived, they encounter varied temperature patterns throughout their productive years. For optimal yields, trees must meet their climatic requirements every year. Therefore, selecting suitable trees requires understanding the plausible range of weather conditions at a site, helping managers choose trees that reliably meet chill needs or balance early flowering with frost risk. This range is determined by the local climate - essentially, the average of yearly weather patterns, representing all potential weather scenarios from which each year is a random outcome.

Annual weather can be interpreted as a random sample from the full distribution of possible weather conditions. For planning, however, it is more useful to understand this entire distribution rather than relying solely on the randomly observed years. So far, only these samples from historical chill data have been available. In this lesson, the goal is to determine the actual climate pattern to develop temperature profiles for specific locations that support orchard planning.

## Weather generators

The best way to characterize the climate of a specific location is through long-term weather records collected there. Such records allow calculation of average monthly temperatures, rainfall extremes, frost frequency, and other metrics. The detail level for describing local climate can vary, and producing realistic weather data requires a certain sophistication.

Weather generators differ significantly in how they model climate, and understanding their methods would help in choosing the best option. For `chillR`, the weather generator must be R-compatible and align with `chillR`’s structure. Currently, only one generator [RMAWGEN](https://cran.r-project.org/web/packages/RMAWGEN/index.html) meets these requirements, limiting choice. Previously, tools like [LARS-WG](https://sites.google.com/view/lars-wg/), which uses both temperature and rainfall data to model distinct dry and wet spell profiles, were used in analyses ([Luedeling et al., 2011a](https://link.springer.com/article/10.1007/s00484-010-0352-y), [2011b](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0020155)). The `chillR` tool doesn’t need precipitation data but performs well overall. However, evaluating these tools remains challenging, indicating potential for further improvement.

## Weather generation in `chillR`

`chillR` uses the [RMAWGEN](https://cran.r-project.org/web/packages/RMAWGEN/index.html) weather generator, currently the only R-based option found, and has shown to be reliable after initial setup challenges. However, `chillR` currently generates only temperature data, without comprehensive weather simulation capabilities—a limitation that is being addressed by further development, initiated by [Lars Caspersen](https://inresgb-lehre.iaas.uni-bonn.de/author/lars-caspersen/).

The function `temperature_generation` in `chillR` requires calibration using long-term temperature data in `chillR` format, enabling it to calculate parameters that define the local climate. These parameters are then applied to simulate synthetic temperature data over a specified number of years.

For practice, the Klein-Altendorf dataset (`KA_weather`) is used as an example. To use `temperature_generation`, a few key inputs are needed:

-   **years**: a vector specifying the years from observed data to characterize the climate.
-   **sim_years**: the years to simulate, used only for labeling purposes in the output dataset.

An additional option, `temperature_scenario`, will be discussed later; initially, its default zero values trigger a warning, which can be ignored for now. The next step is to run the weather generator to compare simulated data with observed records.




``` r
Temp <- KA_weather %>%
  temperature_generation(years = c(1998, 2009),
                         sim_years = c(2001,2100))


Temperatures <- KA_weather %>% filter(Year %in% 1998:2009) %>%
  cbind(Data_source = "observed") %>%
  rbind(
    Temp[[1]] %>% select(c(Year,
                           Month,
                           Day,
                           Tmin,
                           Tmax)) %>%
      cbind(Data_source = "simulated")
    ) %>%
  mutate(Date = as.Date(ISOdate(2000,
                                Month,
                                Day)))
```


``` r
ggplot(data = Temperatures,
       aes(Date, Tmin)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-227-1.png" width="672" />


``` r
ggplot(data=Temperatures,
       aes(Date,Tmax)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-228-1.png" width="672" />

The previous plot was created using `geom_smooth` in `ggplot`, rather than `geom_line`, which reduced noise in the dataset and made the figure easier to interpret.

Overall, the temperature trends were captured well, though some local weather nuances may have been missed. The simulated dataset now contains 100 years of data, even though only 8 years were used for calibration. This expanded dataset allows for a clearer understanding of the frequency of specific temperature-related events. Next, the distribution of winter chill for Klein-Altendorf will be examined based on this analysis.


``` r
chill_observed <- Temperatures %>%
  filter(Data_source == "observed") %>%
  stack_hourly_temps(latitude = 50.4) %>%
  chilling(Start_JDay = 305,
           End_JDay = 59)
  
chill_simulated <- Temperatures %>%
  filter(Data_source == "simulated") %>%
  stack_hourly_temps(latitude = 50.4) %>%
  chilling(Start_JDay = 305,
           End_JDay = 59)
  
chill_comparison <-
  cbind(chill_observed,
        Data_source = "observed") %>%
  rbind(cbind(chill_simulated,
              Data_source = "simulated"))
  
chill_comparison_full_seasons <- 
  chill_comparison %>%
  filter(Perc_complete == 100)
```

The data can now be easily visualized using `ggplot`:


``` r
ggplot(chill_comparison_full_seasons,
       aes(x = Chill_portions)) + 
  geom_histogram(binwidth = 1,
                 aes(fill = factor(Data_source))) +
  theme_bw(base_size = 20) +
  labs(fill = "Data source") +
  xlab("Chill accumulation (Chill Portions)") +
  ylab("Frequency")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-230-1.png" width="672" />

In the previous code, incomplete winter seasons were manually removed. The resulting histogram shows the distribution of chill that would have been reasonable to expect in Klein-Altendorf between 1998 and 2005. With more observations, these distributions would improve.

These data can also be plotted as a cumulative distribution function, which helps assess the risk of falling below a certain level of chill accumulation. This can also be directly calculated using the `quantile` function.


``` r
chill_simulations <-
  chill_comparison_full_seasons %>%
  filter(Data_source == "simulated")
  
ggplot(chill_simulations,
       aes(x = Chill_portions)) +
  stat_ecdf(geom = "step",
            lwd = 1.5,
            col = "blue") +
  ylab("Cumulative probability") +
  xlab("Chill accumulation (in Chill Portions)") +
  theme_bw(base_size = 20)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-231-1.png" width="672" />


``` r
# Here's the amount of chill that is exceeded in 90% of all years.
quantile(chill_simulations$Chill_portions,0.1)
```

```
##      10% 
## 77.21767
```


``` r
# and here's the 50% confidence interval (25th to 75th percentile)
quantile(chill_simulations$Chill_portions, c(0.25,0.75))
```

```
##      25%      75% 
## 79.68650 84.76564
```

The 10% quantile calculated above represents what is referred to as "Safe Winter Chill." This concept is illustrated in the following figure:

![](images/Figure_2_Boxplots_Davis_chilling_hours_a2.jpg)

The process for generating the data for this figure is similar to the one used previously, although different tools were employed at the time. The concept of Safe Winter Chill is based on the idea that a grower might tolerate a small risk of not meeting a tree’s chilling requirement. If a tree's chilling requirement exactly matches the Safe Winter Chill for a site, chill-related issues can be expected roughly one in every ten years. Whether this level of risk is acceptable depends on the grower’s tolerance, but it provides a reasonable threshold. A similar metric can be calculated for growers with different risk tolerances.

## `Exercises` on temperature generation

1.  *For the location you chose for your earlier analyses, use chillR’s weather generator to produce 100 years of synthetic temperature data.*


``` r
Yakima <- read.csv("Yakima/Yakima_weather.csv")

Temp <- Yakima %>% 
  temperature_generation(years = c(1998, 2009),
                         sim_years = c(2001, 2100))


Temperatures <- Yakima %>% 
  select(Year, Month, Day, Tmin, Tmax) %>%  
  filter(Year %in% 1998:2009) %>%
  cbind(Data_source = "observed") %>%
  rbind(
    Temp[[1]] %>% select(c(Year, Month, Day, Tmin, Tmax)) %>% 
      cbind(Data_source = "simulated")
  ) %>%
  mutate(Date = as.Date(ISOdate(2000, Month, Day)))
```


``` r
ggplot(data = Temperatures,
       aes(Date,
           Tmin)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-235-1.png" width="672" />


``` r
ggplot(data = Temperatures,
       aes(Date,
           Tmax)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-236-1.png" width="672" />

2.  *Calculate winter chill (in Chill Portions) for your synthetic weather, and illustrate your results as histograms and cumulative distributions.*


``` r
chill_observed <- Temperatures %>%
  filter(Data_source == "observed") %>%
  stack_hourly_temps(latitude = 46.6) %>%
  chilling(Start_JDay = 305,
           End_JDay = 59)
  
chill_simulated <- Temperatures %>%
  filter(Data_source == "simulated") %>%
  stack_hourly_temps(latitude = 46.6) %>%
  chilling(Start_JDay = 305,
           End_JDay = 59)
  
chill_comparison <-
  cbind(chill_observed,
        Data_source = "observed") %>%
  rbind(cbind(chill_simulated,
              Data_source = "simulated"))
  
chill_comparison_full_seasons <- 
  chill_comparison %>%
  filter(Perc_complete == 100)
```


``` r
ggplot(chill_comparison_full_seasons,
       aes(x = Chill_portions)) + 
  geom_histogram(binwidth = 1,
                 aes(fill = factor(Data_source))) +
  theme_bw(base_size = 20) +
  labs(fill = "Data source") +
  xlab("Chill accumulation (Chill Portions)") +
  ylab("Frequency")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-238-1.png" width="672" />


``` r
chill_simulations <-
  chill_comparison_full_seasons %>%
  filter(Data_source == "simulated")
  
ggplot(chill_simulations,
       aes(x = Chill_portions)) +
  stat_ecdf(geom = "step",
            lwd = 1.5,
            col = "blue") +
  ylab("Cumulative probability") +
  xlab("Chill accumulation (in Chill Portions)") +
  theme_bw(base_size = 20)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-239-1.png" width="672" />

3.  *Produce similar plots for the number of freezing hours (\<0°C) in April (or October, if your site is in the Southern Hemisphere) for your location of interest*


``` r
df <- data.frame(
  lower =  c(-1000,    0),
  upper =  c(    0, 1000),
  weight = c(    1,    0))

freezing_hours <- function(x) step_model(x,df)

chill_observed <- Temperatures %>%
  filter(Data_source == "observed") %>%
  stack_hourly_temps(latitude = 46.6) %>%
  tempResponse(Start_JDay = 91,
               End_JDay = 120,
               models = list(Frost = freezing_hours,
                             Chill_portions = Dynamic_Model,
                             GDH = GDH))

chill_simulated <- Temperatures %>%
  filter(Data_source == "simulated") %>%
  stack_hourly_temps(latitude = 46.6) %>%
  tempResponse(Start_JDay = 91,
               End_JDay = 120,
               models=list(Frost = freezing_hours,
                           Chill_portions = Dynamic_Model,
                           GDH = GDH))

chill_comparison <-
  cbind(chill_observed,
        Data_source = "observed") %>%
  rbind(cbind(chill_simulated,
              Data_source = "simulated"))

chill_comparison_full_seasons <-
  chill_comparison %>%
  filter(Perc_complete == 100)
```


``` r
ggplot(chill_comparison_full_seasons,
       aes(x = Frost)) + 
  geom_histogram(binwidth = 25,
                 aes(fill = factor(Data_source))) +
  theme_bw(base_size = 10) +
  labs(fill = "Data source") +
  xlab("Frost incidence during April (hours)") +
  ylab("Frequency")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-241-1.png" width="672" />


``` r
chill_simulations <-
  chill_comparison_full_seasons %>%
  filter(Data_source == "simulated")

ggplot(chill_simulations,
       aes(x = Frost)) +
  stat_ecdf(geom = "step",
            lwd = 1.5,
            col = "blue") +
  ylab("Cumulative probability") +
  xlab("Frost incidence during April (hours)") +
  theme_bw(base_size = 20)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-242-1.png" width="672" />

<!--chapter:end:12-generate-temp.Rmd-->

# Saving and loading data (and hiding this in markdown)

## Learning Goals

-   Learn how to write and read tables
-   Learn how to save and load lists of (not-too-complicated) objects
-   Learn how to hide such writing and saving from the readers of your markdown document

The learning logbook compilation time increases as more code and data processing are added, due to handling a large dataset—100 years of synthetic hourly weather data, totaling about 876,000 hours. Each hourly temperature calculation required extensive computations, including sunrise, sunset, day length, and chill metrics with the Dynamic Model function. Climate change scenario analysis will require even more data, with calculations potentially taking an hour or longer. To manage this, saving results for faster reloading becomes essential.

## Saving and loading data

R provides `save` and `load` functions to store and retrieve data, though simpler formats like CSV are often preferred for easy inspection outside R. For basic `data.frames`, `write.csv` can be used to save data efficiently. For example, to save the `Temperatures` dataset created in the last lesson, `write.csv` is a straightforward solution:




``` r
head(Temperatures)
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> Tmax </th>
   <th style="text-align:center;"> Data_source </th>
   <th style="text-align:center;"> Date </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> -2.778 </td>
   <td style="text-align:center;"> 11.722 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-01 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> -2.778 </td>
   <td style="text-align:center;"> 12.222 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-02 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> -6.722 </td>
   <td style="text-align:center;"> 2.222 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-03 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> -8.000 </td>
   <td style="text-align:center;"> -1.000 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-04 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> -11.111 </td>
   <td style="text-align:center;"> 6.111 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-05 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 0.611 </td>
   <td style="text-align:center;"> 7.778 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-06 </td>
  </tr>
</tbody>
</table>


``` r
write.csv(Temperatures, file = "Yakima/Temperatures.csv", row.names = FALSE)
```

To save the dataset without row numbering, `row.names=FALSE` is set in `write.csv`. To load the dataset back into R, use `read.tab` as shown below:


``` r
Temperatures <- read_tab("Yakima/Temperatures.csv")
```


``` r
head(Temperatures)
```

<table class="table table-striped" style="font-size: 14px; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> Tmax </th>
   <th style="text-align:center;"> Data_source </th>
   <th style="text-align:center;"> Date </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> -2.778 </td>
   <td style="text-align:center;"> 11.722 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-01 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> -2.778 </td>
   <td style="text-align:center;"> 12.222 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-02 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> -6.722 </td>
   <td style="text-align:center;"> 2.222 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-03 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> -8.000 </td>
   <td style="text-align:center;"> -1.000 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-04 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> -11.111 </td>
   <td style="text-align:center;"> 6.111 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-05 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 1998 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 0.611 </td>
   <td style="text-align:center;"> 7.778 </td>
   <td style="text-align:center;"> observed </td>
   <td style="text-align:center;"> 2000-01-06 </td>
  </tr>
</tbody>
</table>

In the previous example, instead of using R’s built-in `read.csv` function, the `chillR` package’s `read_tab` function was used, which behaves similarly by reading comma-separated files. However, `.csv` files can cause issues in non-English locales where commas are used as decimal symbols (e.g., in French, Spanish, or German environments). In these cases, values are often separated by semicolons instead. `read_tab` can detect whether commas or semicolons are used as delimiters, ensuring compatibility across different regional settings.

Saving and loading simple `data.frames` is straightforward, but more complex objects, like lists of multiple data frames, require a different approach. For this purpose, `chillR` includes functions specifically for saving and loading lists containing numbers, character strings, and `data frames`. Here’s how to create and save a simple list in the designated `data` folder:


``` r
test_list <- list(Number = 1,
                  String = "Thanks for using chillR!",
                  DataFrame = data.frame(a = c(1, 2, 3),
                                         b = c(3, 2, 1),
                                         c = c(5, 4, 3)))

save_temperature_scenarios(test_list,
                           path = "data",
                           prefix = "test_list")
```

In the data folder, three files have been created:

-   `test_list_1_Number.csv`

-   `test_list_2_String.csv`

-   `test_list_3_DataFrame.csv`

Each file stores a specific element of the list. To retrieve the list elements, `chillR` provides a function that reads these files and reassembles them into the original list format:


``` r
test_list <- load_temperature_scenarios(path = "data",
                                        prefix = "test_list")
```

The function's name includes "temperature_scenarios" because it was primarily designed to avoid repeating the time-intensive generation of temperature scenarios, a key step in many `chillR` workflows. Although this function works with other lists as well, it currently has a limitation: single strings and numbers within lists are converted into mini-data frames, an issue that needs addressing.

## Hiding all this from the readers of our markdown file

After completing several lessons, the calculations in the document accumulate, leading to significant processing time, especially as more complex tasks are introduced. To avoid re-running code each time, calculations are typically performed once, and the results are saved. During the document knitting process, the saved data is reloaded.

However, the code can still be visible, even though it may not be executed. This is possible because code chunks in a Markdown document can be configured to either run but remain hidden or be visible without being executed. Key options include:

-   `echo = FALSE`: Runs the code but hides it (and any output) in the final document, while "side effects" like figures are still shown.

-   `eval = FALSE`: Shows the code in the final document but doesn’t execute it.

-   `include = FALSE`: Hides code and results in the final file, but runs the code.

-   `message = FALSE`: Hides messages generated by the code.

-   `warning = FALSE`: Hides warnings generated by the code.

This strategy requires ensuring that all necessary data for later code chunks is preloaded.

<!--chapter:end:13-saving.Rmd-->

# Historic temperature scenarios



## Learning goals for this lesson

-   Understand how we can include temperature scenarios while generating synthetic weather
-   Be able to produce temperature scenarios with arbitrary change scenarios imposed
-   Understand the difference between absolute and relative temperature scenarios and the importance of baselines (for relative scenarios)
-   Learn how to produce temperature scenarios that represent past points in time from historic temperature records
-   Learn how to produce synthetic temperature scenarios for past points in time and efficiently compute agroclimatic metrics for them

## Climate change scenarios

A weather generator accessed through `chillR` can produce agroclimatic profiles for specific locations. Calibration with historical temperature data makes the generated profile representative of the climate during the calibration period. This weather generator can also simulate various climate scenarios using the `temperature_scenario` parameter in the `temperature_generation` function.

The `temperature_scenario` parameter requires a `data.frame` with columns `Tmin` and `Tmax`, each containing 12 values that specify monthly adjustments to the mean minimum and maximum temperatures. Without this parameter, the function defaults to a `data.frame` with zero adjustments, indicating no change.

A simple climate change scenario can be created by adding arbitrary values to each month’s `Tmin` and `Tmax:`


``` r
# Here's the call from the earlier lesson. We don't have to run this again.
Temp <- temperature_generation(KA_weather,
                               years = c(1998,2005),
                               sim_years = c(2001,2100))
 
# Now we make a temperature scenario that raises all temperatures by 2°C
```


``` r
change_scenario <- data.frame(Tmin = rep(2,12),
                              Tmax = rep(2,12))

change_scenario
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> Tmax </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 2 </td>
  </tr>
</tbody>
</table>


``` r
Temp_2 <- temperature_generation(KA_weather,
                                 years = c(1998,2005),
                                 sim_years = c(2001,2100),
                                 temperature_scenario = change_scenario)

Temperature_scenarios <- KA_weather %>%
  filter(Year %in% 1998:2005) %>%
  cbind(Data_source = "observed") %>%
  rbind(Temp[[1]] %>% 
          select(c(Year, Month, Day, Tmin, Tmax)) %>% 
          cbind(Data_source = "simulated")
        ) %>%
  rbind(Temp_2[[1]] %>%
          select(c(Year, Month, Day, Tmin, Tmax)) %>% 
          cbind(Data_source = "Warming_2C")
        ) %>%
  mutate(Date = as.Date(ISOdate(2000,
                                Month,
                                Day)))
```

Due to the identical structure of this dataset to the one used in the previous lesson, the same code can be applied with only the `data.frame` name needing adjustment:


``` r
ggplot(data = Temperature_scenarios, 
       aes(Date,Tmin)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/weather_generator_set_up_plot_scenarios-1.png" width="672" />

``` r
ggplot(data = Temperature_scenarios,
       aes(Date,Tmax)) +
  geom_smooth(aes(colour = factor(Year))) +
  facet_wrap(vars(Data_source)) +
  theme_bw(base_size = 20) +
  theme(legend.position = "none") +
  scale_x_date(date_labels = "%b")
```

<img src="bookdownproj_files/figure-html/weather_generator_set_up_plot_scenarios-2.png" width="672" />

The scenario is simplified, with future changes uniformly distributed across all months—an approach that doesn’t reflect historical patterns and is unlikely for the future. However, this method closely resembles an early attempt at modeling climate change scenarios, as illustrated in the figure from the initial publication on chilling.

![Chill scenarios for a mountain oasis in Oman according ([Luedeling et al., 2009b)](https://link.springer.com/article/10.1007/s10584-009-9581-7)(images/Luedeling_JPG_Figure_10_Future_chilling (1).jpg)

To create more realistic scenarios, specific years from historical records are used, considering both the expected typical temperature conditions of the time and actual recorded data. This approach clarifies historical climate trends by focusing on gradual climate shifts, avoiding distortions from random annual variations or extreme outliers that might obscure trend analysis.

## Making historic temperature scenarios

A long-term dataset is essential for this exercise, and the process of obtaining and preparing this data for use in `chillR` has already been covered.


``` r
# download weather station list for the vicinity of Bonn
station_list <- handle_gsod(action = "list_stations",
                            location=c(7.1,50.8))

# download weather data for Cologne/Bonn airport and convert it to chillR format
Bonn_weather <- handle_gsod(action = "download_weather",
                            location = station_list$chillR_code[1],
                            time_interval = c(1973,2019)) %>%
  handle_gsod()

# check record for missing data
fix_weather(Bonn_weather$`KOLN BONN`)$QC

# (incidentally almost all gaps are for years covered by the KA_weather dataset)
Bonn_patched <- patch_daily_temperatures(
  weather = Bonn_weather$`KOLN BONN`,
  patch_weather = list(KA_weather))

fix_weather(Bonn_patched)$QC

# There are still 4 days missing here, out of 47 years -
# let's simply interpolate these gaps now

Bonn <- fix_weather(Bonn_patched)

Bonn_temps <- Bonn$weather
```

To create weather scenarios representing specific years like 1980, 1990, 2000, and 2010, despite using data centered around the median year of 1996 (due to gradual temperature increases from 1973 to 2019), adjustments must be made to account for historical changes. The process involves analyzing the historical temperature record to quantify shifts between the **baseline** year (the reference year of the dataset) and each target **simulation year**.

The `chillR` package provides a function, `temperature_scenario_from_records`, designed for this purpose. This function allows for the creation of temperature scenarios based on past records, facilitating the generation of simulations that accurately reflect historical conditions for specified years:


``` r
scenario_1980 <- temperature_scenario_from_records(weather = Bonn_temps,
                                                   year = 1980)
```

This scenario involves several components:

-   `data`: A data frame containing the minimum (`Tmin`) and maximum (`Tmax`) temperatures that are representative of the year of interest.

-   `scenario_year`: The specific year for which the scenario is being created.

-   `reference_year`: This would be used if the scenario involved temperature changes relative to another year, but in this case, it is set to NA since we are working with absolute temperatures.

-   `scenario_type`: Indicates whether the scenario presents absolute temperatures for the year of interest (true in this case) or changes relative to another year.

-   `labels`: Additional information attached to the scenario, such as "running mean scenario," which provides further context or explanation about the nature of the scenario.


``` r
scenario_1980$'1980'$data
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> Tmax </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> -1.6792086 </td>
   <td style="text-align:center;"> 4.374077 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> -2.3167936 </td>
   <td style="text-align:center;"> 5.580554 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 0.8537656 </td>
   <td style="text-align:center;"> 9.763557 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2.8043289 </td>
   <td style="text-align:center;"> 13.474438 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 6.8980925 </td>
   <td style="text-align:center;"> 18.016243 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10.4950644 </td>
   <td style="text-align:center;"> 21.370489 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 12.3964194 </td>
   <td style="text-align:center;"> 23.175626 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 11.8548366 </td>
   <td style="text-align:center;"> 23.186135 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 9.2693867 </td>
   <td style="text-align:center;"> 19.827527 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.8487484 </td>
   <td style="text-align:center;"> 14.443617 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2.2375311 </td>
   <td style="text-align:center;"> 9.076796 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 0.1126710 </td>
   <td style="text-align:center;"> 6.024129 </td>
  </tr>
</tbody>
</table>

The warning message received when first running the weather generator highlighted a few important points:

-   *scenario doesn’t contain named elements - consider using the following element names: ‘data’, ‘reference_year’,‘scenario_type’,‘labels’*

-   *setting scenario_type to ‘relative’*

-   *Reference year missing - can’t check if relative temperature scenario is valid*

The warning message previously encountered highlighted the missing elements in the input data frame. Scenarios require more information, and when this is absent, the temperature generation function makes assumptions about how to proceed. Specifically, the **scenario_type** was automatically set to **‘relative’**, as the function had to determine whether the scenario represented absolute or relative temperatures. Additionally, the absence of a **reference_year** meant the function couldn't identify the baseline for the relative temperature scenario.

With the updated scenario, which now includes all necessary information - such as **data**, **scenario_year**, **reference_year**, **scenario_type**, and **labels** - these warnings should no longer occur. The temperature generation function can now be run correctly with this complete set of details:


``` r
temps_1980 <- temperature_generation(weather = Bonn_temps,
                                     years = c(1973,2019),
                                     sim_years = c(2001,2100),
                                     temperature_scenario = scenario_1980)
```

Despite providing all the necessary information in the updated scenario, a warning message was still encountered:

“Absolute temperature scenario specified - calibration weather record only used for simulating temperature variation, but not for the means”

The weather generator evaluated the calibration dataset by considering the variation of temperatures around the mean values. It then produced a new dataset with mean temperatures (for both **Tmin** and **Tmax**) for each month that correspond to the absolute temperature scenario provided. The variation in this generated dataset was similar to the observed temperature variation, which was the intended outcome.

To convert this absolute temperature scenario into a relative one, a baseline scenario needs to be specified for comparison. In this case, 1996 is chosen as the baseline year, since it represents the median year of the observed record. A scenario for that year can now be created as the reference for comparison:


``` r
scenario_1996 <- temperature_scenario_from_records(weather = Bonn_temps,
                                                   year = 1996)
```

The 1996 scenario is an absolute temperature scenario. To convert it to a relative change scenario, the `temperature_scenario_baseline_adjustment` function is used, which adjusts the temperatures based on the baseline scenario.


``` r
relative_scenario <- temperature_scenario_baseline_adjustment(
  baseline = scenario_1996,
  temperature_scenario = scenario_1980)
```

Now, a relative change scenario has been created, which contains the following elements:

-   `data`: A data frame with **Tmin** and **Tmax** columns, representing the relative changes in temperatures between 1996 and 1980 (all negative values, as 1980 was cooler than 1996).

-   `scenario_year`: 1980

-   `reference_year`: 1996

-   `scenario_type`: ‘relative’

-   `labels`: ‘running mean scenario’

The relative change scenario can now be applied similarly to previous scenarios:


``` r
temps_1980<-temperature_generation(weather = Bonn_temps,
                                   years = c(1973,2019),
                                   sim_years = c(2001,2100),
                                   temperature_scenario = relative_scenario)
```

This time, no warning message appeared because all the necessary information was provided to the `temperature_generation` function. Now, all the intended scenarios can be created easily, as most functions support vectors and lists, not just single values or data frames.


``` r
all_past_scenarios <- temperature_scenario_from_records(
  weather = Bonn_temps,
  year = c(1980,
           1990,
           2000,
           2010))

adjusted_scenarios <- temperature_scenario_baseline_adjustment(
  baseline = scenario_1996,
  temperature_scenario = all_past_scenarios)

all_past_scenario_temps <- temperature_generation(
  weather = Bonn_temps,
  years = c(1973,2019),
  sim_years = c(2001,2100),
  temperature_scenario = adjusted_scenarios)

save_temperature_scenarios(all_past_scenario_temps, "data", "Bonn_hist_scenarios")
```

To calculate chill accumulation, instead of manually applying each function to the four generated temperature scenarios, the `tempResponse_daily_list` function from `chillR` can be used, as it automates the process. Additionally, a simple frost model will be created, with the Dynamic Model and GDH Model selected for evaluation.


``` r
frost_model <- function(x)
  step_model(x,
             data.frame(
               lower=c(-1000,0),
               upper=c(0,1000),
               weight=c(1,0)))

models <- list(Chill_Portions = Dynamic_Model,
               GDH = GDH,
               Frost_H = frost_model)
```


``` r
chill_hist_scenario_list <- tempResponse_daily_list(all_past_scenario_temps,
                                                    latitude = 50.9,
                                                    Start_JDay = 305,
                                                    End_JDay = 59,
                                                    models = models)
```

To ensure the scenarios are available for later use in the lessons on **Making CMPI6 scenarios** and **Making CMIP5 scenarios with the ClimateWizard**, they should be saved with a clear file name that includes the place name and the start and end dates of the considered period. Before saving, any incomplete winters will be removed from the record to ensure the data is accurate and complete.


``` r
chill_hist_scenario_list <- lapply(chill_hist_scenario_list,
                                   function(x) x %>%
                                     filter(Perc_complete == 100))

save_temperature_scenarios(chill_hist_scenario_list, "data","Bonn_hist_chill_305_59")
```


``` r
scenarios <- names(chill_hist_scenario_list)[1:4]

all_scenarios <- chill_hist_scenario_list[[scenarios[1]]] %>%
  mutate(scenario = as.numeric(scenarios[1]))

for (sc in scenarios[2:4])
 all_scenarios <- all_scenarios %>%
  rbind(chill_hist_scenario_list[[sc]] %>%
          cbind(
            scenario=as.numeric(sc))
        ) %>%
  filter(Perc_complete == 100)

# Let's compute the actual 'observed' chill for comparison
actual_chill <- tempResponse_daily_list(Bonn_temps,
                                        latitude=50.9,
                                        Start_JDay = 305,
                                        End_JDay = 59,
                                        models)[[1]] %>%
  filter(Perc_complete == 100)

ggplot(data = all_scenarios,
       aes(scenario,
           Chill_Portions,
           fill = factor(scenario))) +
  geom_violin() +
  ylab("Chill accumulation (Chill Portions)") +
  xlab("Scenario year") +
  theme_bw(base_size = 15) +
  ylim(c(0,90)) +
  geom_point(data = actual_chill,
             aes(End_year,
                 Chill_Portions,
                 fill = "blue"),
             col = "blue",
             show.legend = FALSE) +
  scale_fill_discrete(name = "Scenario",
                      breaks = unique(all_scenarios$scenario)) 
```

<img src="bookdownproj_files/figure-html/condense_chill_list-1.png" width="672" />

The observed chill data should also be saved for later use in the lessons on **Making CMPI6 scenarios** and **Making CMIP5 scenarios with the ClimateWizard**. This will allow for easy access and comparison when working with those scenarios in the future.


``` r
write.csv(actual_chill,"data/Bonn_observed_chill_305_59.csv", row.names = FALSE)
```

The chill distribution scenarios for 1980, 1990, 2000, and 2010 show minimal change, suggesting that chill deficiencies in Bonn are unlikely in the near future.

So far, all annual scenarios were based on running means of **Tmin** and **Tmax**, which is a reasonable approach given the challenges of estimating temperatures in times of accelerating climate change. However, `chillR` also offers the option of using linear regression to determine representative temperatures for a specific historical scenario. A quick comparison will reveal how this method affects the scenarios.


``` r
temperature_means <- 
  data.frame(Year = min(Bonn_temps$Year):max(Bonn_temps$Year),
             Tmin = aggregate(Bonn_temps$Tmin,
                              FUN = "mean",
                              by = list(Bonn_temps$Year))[,2],
             Tmax=aggregate(Bonn_temps$Tmax,
                            FUN = "mean",
                            by = list(Bonn_temps$Year))[,2]) %>%
  mutate(runn_mean_Tmin = runn_mean(Tmin,15),
         runn_mean_Tmax = runn_mean(Tmax,15))


Tmin_regression <- lm(Tmin~Year,
                      temperature_means)

Tmax_regression <- lm(Tmax~Year,
                      temperature_means)

temperature_means <- temperature_means %>%
  mutate(regression_Tmin = Tmin_regression$coefficients[1]+
           Tmin_regression$coefficients[2]*temperature_means$Year,
           regression_Tmax = Tmax_regression$coefficients[1]+
           Tmax_regression$coefficients[2]*temperature_means$Year
         )

ggplot(temperature_means,
       aes(Year,
           Tmin)) + 
  geom_point() + 
  geom_line(data = temperature_means,
            aes(Year,
                runn_mean_Tmin),
            lwd = 2,
            col = "blue") + 
  geom_line(data = temperature_means,
            aes(Year,
                regression_Tmin),
            lwd = 2,
            col = "red") +
  theme_bw(base_size = 15) +
  ylab("Mean monthly minimum temperature (°C)")
```

<img src="bookdownproj_files/figure-html/runn_mean_vs_regression-1.png" width="672" />

``` r
ggplot(temperature_means,
       aes(Year,
           Tmax)) + 
  geom_point() + 
  geom_line(data = temperature_means,
            aes(Year,
                runn_mean_Tmax),
            lwd = 2,
            col = "blue") + 
  geom_line(data = temperature_means,
            aes(Year, 
                regression_Tmax),
            lwd = 2,
            col = "red") +
  theme_bw(base_size = 15) +
  ylab("Mean monthly maximum temperature (°C)")
```

<img src="bookdownproj_files/figure-html/runn_mean_vs_regression-2.png" width="672" />

There is a noticeable difference between the running mean function (blue) and the linear regression line (red). While the running mean provides a smoother approximation, the linear regression line offers a more direct trend. This difference can be significant, and it is expected to become more pronounced as climate change continues to affect temperature patterns.

## `Exercises` on generating historic temperature scenarios

Please document all results of the following assignments in your `learning logbook`.

1)  *For the location you chose for previous exercises, produce historic temperature scenarios representing several years of the historic record (your choice).*


```
##    YEARMODA                DATE                Date Year Month Day    Tmin   Tmax   Tmean
## 1  19730101 1973-01-01 12:00:00 1973-01-01 12:00:00 1973     1   1  -3.000  6.111   0.000
## 2  19730102 1973-01-02 12:00:00 1973-01-02 12:00:00 1973     1   2  -1.111  8.278   2.611
## 3  19730103 1973-01-03 12:00:00 1973-01-03 12:00:00 1973     1   3  -5.000  3.000  -1.278
## 4  19730104 1973-01-04 12:00:00 1973-01-04 12:00:00 1973     1   4 -12.222 -0.611  -6.389
## 5  19730105 1973-01-05 12:00:00 1973-01-05 12:00:00 1973     1   5 -10.000 -3.278  -6.667
## 6  19730106 1973-01-06 12:00:00 1973-01-06 12:00:00 1973     1   6 -17.222 -5.000  -9.944
## 7  19730107 1973-01-07 12:00:00 1973-01-07 12:00:00 1973     1   7 -17.000 -6.000 -12.333
## 8  19730108 1973-01-08 12:00:00 1973-01-08 12:00:00 1973     1   8 -17.000 -5.000 -11.167
## 9  19730109 1973-01-09 12:00:00 1973-01-09 12:00:00 1973     1   9 -13.889 -4.000  -7.389
## 10 19730110 1973-01-10 12:00:00 1973-01-10 12:00:00 1973     1  10  -9.000 -2.778  -5.056
## 11 19730111 1973-01-11 12:00:00 1973-01-11 12:00:00 1973     1  11  -6.111 -2.722  -4.556
## 12 19730112 1973-01-12 12:00:00 1973-01-12 12:00:00 1973     1  12  -8.278 -1.611  -4.000
## 13 19730113 1973-01-13 12:00:00 1973-01-13 12:00:00 1973     1  13  -1.111  2.222   0.667
## 14 19730114 1973-01-14 12:00:00 1973-01-14 12:00:00 1973     1  14  -2.222  1.111  -0.222
## 15 19730115 1973-01-15 12:00:00 1973-01-15 12:00:00 1973     1  15  -3.278  3.778  -0.444
## 16 19730116 1973-01-16 12:00:00 1973-01-16 12:00:00 1973     1  16   1.111  5.000   2.889
## 17 19730117 1973-01-17 12:00:00 1973-01-17 12:00:00 1973     1  17  -2.778  6.611   1.333
## 18 19730118 1973-01-18 12:00:00 1973-01-18 12:00:00 1973     1  18  -1.722  6.111   0.778
## 19 19730119 1973-01-19 12:00:00 1973-01-19 12:00:00 1973     1  19  -3.889  4.389   1.056
## 20 19730120 1973-01-20 12:00:00 1973-01-20 12:00:00 1973     1  20  -6.611  4.389  -2.278
## 21 19730121 1973-01-21 12:00:00 1973-01-21 12:00:00 1973     1  21  -7.222  4.389  -3.111
## 22 19730122 1973-01-22 12:00:00 1973-01-22 12:00:00 1973     1  22  -7.722  3.278  -4.167
## 23 19730123 1973-01-23 12:00:00 1973-01-23 12:00:00 1973     1  23  -5.000  2.222  -1.889
## 24 19730124 1973-01-24 12:00:00 1973-01-24 12:00:00 1973     1  24  -5.500  6.111  -1.111
## 25 19730125 1973-01-25 12:00:00 1973-01-25 12:00:00 1973     1  25  -0.611  7.778   3.333
## 26 19730126 1973-01-26 12:00:00 1973-01-26 12:00:00 1973     1  26  -7.722  3.778  -2.444
## 27 19730127 1973-01-27 12:00:00 1973-01-27 12:00:00 1973     1  27  -5.000  2.778  -2.222
## 28 19730128 1973-01-28 12:00:00 1973-01-28 12:00:00 1973     1  28  -3.889  2.222  -0.611
## 29 19730129 1973-01-29 12:00:00 1973-01-29 12:00:00 1973     1  29  -4.389  2.778  -1.556
## 30 19730130 1973-01-30 12:00:00 1973-01-30 12:00:00 1973     1  30  -5.611  1.722  -1.778
## 31 19730131 1973-01-31 12:00:00 1973-01-31 12:00:00 1973     1  31  -6.222  2.222  -1.500
## 32 19730201 1973-02-01 12:00:00 1973-02-01 12:00:00 1973     2   1  -5.611  3.278  -1.944
## 33 19730202 1973-02-02 12:00:00 1973-02-02 12:00:00 1973     2   2  -2.722  6.111   0.778
## 34 19730203 1973-02-03 12:00:00 1973-02-03 12:00:00 1973     2   3  -0.500  8.278   2.444
## 35 19730204 1973-02-04 12:00:00 1973-02-04 12:00:00 1973     2   4  -1.111  7.778   3.111
## 36 19730205 1973-02-05 12:00:00 1973-02-05 12:00:00 1973     2   5  -5.000  7.222   0.000
## 37 19730206 1973-02-06 12:00:00 1973-02-06 12:00:00 1973     2   6   0.500  6.722   1.778
## 38 19730207 1973-02-07 12:00:00 1973-02-07 12:00:00 1973     2   7   0.000  5.500   1.722
## 39 19730208 1973-02-08 12:00:00 1973-02-08 12:00:00 1973     2   8  -5.611  6.111  -0.611
## 40 19730209 1973-02-09 12:00:00 1973-02-09 12:00:00 1973     2   9  -3.278  5.000   0.444
## 41 19730210 1973-02-10 12:00:00 1973-02-10 12:00:00 1973     2  10  -0.611  2.778   0.944
## 42 19730211 1973-02-11 12:00:00 1973-02-11 12:00:00 1973     2  11  -2.722  1.722   0.056
## 43 19730212 1973-02-12 12:00:00 1973-02-12 12:00:00 1973     2  12  -1.111  1.111  -0.056
## 44 19730213 1973-02-13 12:00:00 1973-02-13 12:00:00 1973     2  13   0.000  3.278   0.833
## 45 19730214 1973-02-14 12:00:00 1973-02-14 12:00:00 1973     2  14   0.500  4.389   1.611
## 46 19730215 1973-02-15 12:00:00 1973-02-15 12:00:00 1973     2  15   1.111  3.278   1.889
## 47 19730216 1973-02-16 12:00:00 1973-02-16 12:00:00 1973     2  16  -0.500  3.278   1.278
## 48 19730217 1973-02-17 12:00:00 1973-02-17 12:00:00 1973     2  17   1.111  6.111   2.167
## 49 19730218 1973-02-18 12:00:00 1973-02-18 12:00:00 1973     2  18  -2.778 11.611   3.444
## 50 19730219 1973-02-19 12:00:00 1973-02-19 12:00:00 1973     2  19  -2.778 10.611   2.278
## 51 19730220 1973-02-20 12:00:00 1973-02-20 12:00:00 1973     2  20  -3.278 12.722   2.944
## 52 19730221 1973-02-21 12:00:00 1973-02-21 12:00:00 1973     2  21  -3.278 13.278   3.556
## 53 19730222 1973-02-22 12:00:00 1973-02-22 12:00:00 1973     2  22  -3.278 12.722   3.278
## 54 19730223 1973-02-23 12:00:00 1973-02-23 12:00:00 1973     2  23  -2.222 13.778   4.389
## 55 19730224 1973-02-24 12:00:00 1973-02-24 12:00:00 1973     2  24  -2.778 13.778   4.667
## 56 19730225 1973-02-25 12:00:00 1973-02-25 12:00:00 1973     2  25   1.111 14.389   7.167
## 57 19730226 1973-02-26 12:00:00 1973-02-26 12:00:00 1973     2  26   2.722 13.278   7.389
## 58 19730227 1973-02-27 12:00:00 1973-02-27 12:00:00 1973     2  27   0.000 14.389   6.333
## 59 19730228 1973-02-28 12:00:00 1973-02-28 12:00:00 1973     2  28   3.278 15.000   7.500
## 60 19730301 1973-03-01 12:00:00 1973-03-01 12:00:00 1973     3   1   6.111 13.278   9.722
## 61 19730302 1973-03-02 12:00:00 1973-03-02 12:00:00 1973     3   2  -1.611 13.278   6.111
## 62 19730303 1973-03-03 12:00:00 1973-03-03 12:00:00 1973     3   3  -0.611 12.778   4.611
## 63 19730304 1973-03-04 12:00:00 1973-03-04 12:00:00 1973     3   4  -2.778 14.389   6.056
## 64 19730305 1973-03-05 12:00:00 1973-03-05 12:00:00 1973     3   5  -2.722 13.778   5.222
## 65 19730306 1973-03-06 12:00:00 1973-03-06 12:00:00 1973     3   6  -1.111 15.000   6.500
## 66 19730307 1973-03-07 12:00:00 1973-03-07 12:00:00 1973     3   7   4.389 16.111   9.611
## 67 19730308 1973-03-08 12:00:00 1973-03-08 12:00:00 1973     3   8   3.278 16.111   9.278
## 68 19730309 1973-03-09 12:00:00 1973-03-09 12:00:00 1973     3   9   2.722 15.611  10.000
## 69 19730310 1973-03-10 12:00:00 1973-03-10 12:00:00 1973     3  10   7.222 14.389  10.556
## 70 19730311 1973-03-11 12:00:00 1973-03-11 12:00:00 1973     3  11  -3.889 15.500   4.500
## 71 19730312 1973-03-12 12:00:00 1973-03-12 12:00:00 1973     3  12  -2.722 14.389   4.889
## 72 19730313 1973-03-13 12:00:00 1973-03-13 12:00:00 1973     3  13  -1.111 13.889   5.167
## 73 19730314 1973-03-14 12:00:00 1973-03-14 12:00:00 1973     3  14  -5.000 14.389   3.556
## 74 19730315 1973-03-15 12:00:00 1973-03-15 12:00:00 1973     3  15  -0.500 14.389   6.833
## 75 19730316 1973-03-16 12:00:00 1973-03-16 12:00:00 1973     3  16   2.222 17.778   8.667
## 76 19730317 1973-03-17 12:00:00 1973-03-17 12:00:00 1973     3  17  -3.778 12.222   4.944
## 77 19730318 1973-03-18 12:00:00 1973-03-18 12:00:00 1973     3  18   1.611 13.778   5.611
## 78 19730319 1973-03-19 12:00:00 1973-03-19 12:00:00 1973     3  19   5.611 12.222   8.111
## 79 19730320 1973-03-20 12:00:00 1973-03-20 12:00:00 1973     3  20   3.778 15.000   8.500
## 80 19730321 1973-03-21 12:00:00 1973-03-21 12:00:00 1973     3  21  -1.611 15.000   7.056
## 81 19730322 1973-03-22 12:00:00 1973-03-22 12:00:00 1973     3  22   2.722 15.000   9.611
## 82 19730323 1973-03-23 12:00:00 1973-03-23 12:00:00 1973     3  23  -2.722 18.278   7.778
## 83 19730324 1973-03-24 12:00:00 1973-03-24 12:00:00 1973     3  24  -2.778 18.278   7.333
##       Prec Tmin_source Tmax_source
## 1    0.000        <NA>        <NA>
## 2    0.000        <NA>        <NA>
## 3    0.000        <NA>        <NA>
## 4    0.000        <NA>        <NA>
## 5    1.016        <NA>        <NA>
## 6    0.000        <NA>        <NA>
## 7    0.000        <NA>        <NA>
## 8    0.000        <NA>        <NA>
## 9   44.958        <NA>        <NA>
## 10  50.038        <NA>        <NA>
## 11   4.064        <NA>        <NA>
## 12   7.112        <NA>        <NA>
## 13   6.096        <NA>        <NA>
## 14   0.000        <NA>        <NA>
## 15 136.906        <NA>        <NA>
## 16   1.016        <NA>        <NA>
## 17   1.016        <NA>        <NA>
## 18   0.000        <NA>        <NA>
## 19   7.874        <NA>        <NA>
## 20   0.000        <NA>        <NA>
## 21  35.052        <NA>        <NA>
## 22   0.000        <NA>        <NA>
## 23   0.000        <NA>        <NA>
## 24      NA        <NA>        <NA>
## 25  41.910        <NA>        <NA>
## 26  42.926        <NA>        <NA>
## 27   0.000        <NA>        <NA>
## 28  37.084        <NA>        <NA>
## 29   0.000        <NA>        <NA>
## 30   0.000        <NA>        <NA>
## 31   0.000        <NA>        <NA>
## 32   0.000        <NA>        <NA>
## 33  39.116        <NA>        <NA>
## 34   0.000        <NA>        <NA>
## 35  39.878        <NA>        <NA>
## 36  46.990        <NA>        <NA>
## 37   0.000        <NA>        <NA>
## 38   0.000        <NA>        <NA>
## 39  41.910        <NA>        <NA>
## 40  77.978        <NA>        <NA>
## 41  34.036        <NA>        <NA>
## 42   1.016        <NA>        <NA>
## 43  35.052        <NA>        <NA>
## 44   1.016        <NA>        <NA>
## 45   0.000        <NA>        <NA>
## 46   0.000        <NA>        <NA>
## 47   0.000        <NA>        <NA>
## 48   0.000        <NA>        <NA>
## 49  43.942        <NA>        <NA>
## 50   0.000        <NA>        <NA>
## 51 102.108        <NA>        <NA>
## 52  44.958        <NA>        <NA>
## 53   0.000        <NA>        <NA>
## 54  59.944        <NA>        <NA>
## 55   0.000        <NA>        <NA>
## 56   0.000        <NA>        <NA>
## 57   0.000        <NA>        <NA>
## 58 119.888        <NA>        <NA>
## 59   0.000        <NA>        <NA>
## 60   0.000        <NA>        <NA>
## 61   0.000        <NA>        <NA>
## 62   0.000        <NA>        <NA>
## 63   0.000        <NA>        <NA>
## 64   0.000        <NA>        <NA>
## 65   0.000        <NA>        <NA>
## 66  54.102        <NA>        <NA>
## 67 130.048        <NA>        <NA>
## 68   0.000        <NA>        <NA>
## 69   0.000        <NA>        <NA>
## 70  89.916        <NA>        <NA>
## 71 144.018        <NA>        <NA>
## 72 109.982        <NA>        <NA>
## 73   0.000        <NA>        <NA>
## 74   0.000        <NA>        <NA>
## 75 109.982        <NA>        <NA>
## 76   0.000        <NA>        <NA>
## 77   0.000        <NA>        <NA>
## 78  49.022        <NA>        <NA>
## 79   0.000        <NA>        <NA>
## 80   0.000        <NA>        <NA>
## 81   0.000        <NA>        <NA>
## 82   0.000        <NA>        <NA>
## 83  54.102        <NA>        <NA>
##  [ reached 'max' / getOption("max.print") -- omitted 18544 rows ]
```


``` r
#get a list of close-by weather stations
station_list <- handle_gsod(action = "list_stations",
                            location = c(long = -120.5, lat = 46.6),
                            time_interval = c(1973, 2023))


#download data
Yakima_weather <- handle_gsod(action = "download_weather",
                            location = station_list$chillR_code[1],
                            time_interval = c(1973, 2023)) %>%
  handle_gsod()
```

```
## Loading data for 51 years from station 'YAKIMA AIR TERMINAL/MCALSR FIELD AP'
## ===============================================================================================
```

``` r
# check record for missing data
fix_weather(Yakima_weather$`YAKIMA AIR TERMINAL/MCALSR FIELD AP`)$QC
```

```
##       Season End_year Season_days Data_days Missing_Tmin Missing_Tmax Incomplete_days
## 1  1972/1973     1973         365       365            0            0               0
## 2  1973/1974     1974         365       365            0            0               0
## 3  1974/1975     1975         365       365            0            0               0
## 4  1975/1976     1976         366       366            0            0               0
## 5  1976/1977     1977         365       365            0            0               0
## 6  1977/1978     1978         365       365            0            0               0
## 7  1978/1979     1979         365       365            0            0               0
## 8  1979/1980     1980         366       366            0            0               0
## 9  1980/1981     1981         365       365            0            0               0
## 10 1981/1982     1982         365       365            0            0               0
## 11 1982/1983     1983         365       365            0            0               0
## 12 1983/1984     1984         366       366            0            0               0
## 13 1984/1985     1985         365       365            0            0               0
## 14 1985/1986     1986         365       365            0            0               0
## 15 1986/1987     1987         365       365            0            0               0
## 16 1987/1988     1988         366       366            0            0               0
## 17 1988/1989     1989         365       365            0            0               0
## 18 1989/1990     1990         365       365            0            0               0
## 19 1990/1991     1991         365       365            0            0               0
## 20 1991/1992     1992         366       366            0            0               0
## 21 1992/1993     1993         365       365            0            0               0
## 22 1993/1994     1994         365       365            0            0               0
## 23 1994/1995     1995         365       365            0            0               0
## 24 1995/1996     1996         366       366            0            0               0
## 25 1996/1997     1997         365       365            0            0               0
## 26 1997/1998     1998         365       365            0            0               0
## 27 1998/1999     1999         365       365            0            0               0
## 28 1999/2000     2000         366       366            0            0               0
## 29 2000/2001     2001         365       365            0            0               0
## 30 2001/2002     2002         365       365            0            0               0
## 31 2002/2003     2003         365       365            0            0               0
## 32 2003/2004     2004         366       366            0            0               0
## 33 2004/2005     2005         365       365            0            0               0
## 34 2005/2006     2006         365       365            0            0               0
## 35 2006/2007     2007         365       365            0            0               0
## 36 2007/2008     2008         366       366            0            0               0
## 37 2008/2009     2009         365       365            0            0               0
## 38 2009/2010     2010         365       365            0            0               0
## 39 2010/2011     2011         365       365            0            0               0
## 40 2011/2012     2012         366       366            0            0               0
## 41 2012/2013     2013         365       365            0            0               0
## 42 2013/2014     2014         365       365            0            0               0
## 43 2014/2015     2015         365       365            0            0               0
## 44 2015/2016     2016         366       366            0            0               0
## 45 2016/2017     2017         365       365            0            0               0
## 46 2017/2018     2018         365       365            0            0               0
## 47 2018/2019     2019         365       365            0            0               0
## 48 2019/2020     2020         366       366            0            0               0
## 49 2020/2021     2021         365       365            0            0               0
## 50 2021/2022     2022         365       365            0            0               0
## 51 2022/2023     2023         365       365            0            0               0
##    Perc_complete
## 1            100
## 2            100
## 3            100
## 4            100
## 5            100
## 6            100
## 7            100
## 8            100
## 9            100
## 10           100
## 11           100
## 12           100
## 13           100
## 14           100
## 15           100
## 16           100
## 17           100
## 18           100
## 19           100
## 20           100
## 21           100
## 22           100
## 23           100
## 24           100
## 25           100
## 26           100
## 27           100
## 28           100
## 29           100
## 30           100
## 31           100
## 32           100
## 33           100
## 34           100
## 35           100
## 36           100
## 37           100
## 38           100
## 39           100
## 40           100
## 41           100
## 42           100
## 43           100
## 44           100
## 45           100
## 46           100
## 47           100
## 48           100
## 49           100
## 50           100
## 51           100
```

``` r
# filling gaps
patch_weather <-
  handle_gsod(action = "download_weather",
              location = as.character(station_list$chillR_code[c(4, 6)]),
              time_interval = c(1973, 2023)) %>%
  handle_gsod()
```

```
## Loading data for 51 years from station 'RANGE OP 13 / YAKIMA TRAINING CENTER'
## ===============================================================================================
## 
## Loading data for 51 years from station 'BOWERS FIELD AIRPORT'
## ===============================================================================================
```

``` r
Yakima_patched <- patch_daily_temperatures(
  weather = Yakima_weather$`YAKIMA AIR TERMINAL/MCALSR FIELD AP`,
  patch_weather = patch_weather)


fix_weather(Yakima_patched)$QC
```

```
##       Season End_year Season_days Data_days Missing_Tmin Missing_Tmax Incomplete_days
## 1  1972/1973     1973         365       365            0            0               0
## 2  1973/1974     1974         365       365            0            0               0
## 3  1974/1975     1975         365       365            0            0               0
## 4  1975/1976     1976         366       366            0            0               0
## 5  1976/1977     1977         365       365            0            0               0
## 6  1977/1978     1978         365       365            0            0               0
## 7  1978/1979     1979         365       365            0            0               0
## 8  1979/1980     1980         366       366            0            0               0
## 9  1980/1981     1981         365       365            0            0               0
## 10 1981/1982     1982         365       365            0            0               0
## 11 1982/1983     1983         365       365            0            0               0
## 12 1983/1984     1984         366       366            0            0               0
## 13 1984/1985     1985         365       365            0            0               0
## 14 1985/1986     1986         365       365            0            0               0
## 15 1986/1987     1987         365       365            0            0               0
## 16 1987/1988     1988         366       366            0            0               0
## 17 1988/1989     1989         365       365            0            0               0
## 18 1989/1990     1990         365       365            0            0               0
## 19 1990/1991     1991         365       365            0            0               0
## 20 1991/1992     1992         366       366            0            0               0
## 21 1992/1993     1993         365       365            0            0               0
## 22 1993/1994     1994         365       365            0            0               0
## 23 1994/1995     1995         365       365            0            0               0
## 24 1995/1996     1996         366       366            0            0               0
## 25 1996/1997     1997         365       365            0            0               0
## 26 1997/1998     1998         365       365            0            0               0
## 27 1998/1999     1999         365       365            0            0               0
## 28 1999/2000     2000         366       366            0            0               0
## 29 2000/2001     2001         365       365            0            0               0
## 30 2001/2002     2002         365       365            0            0               0
## 31 2002/2003     2003         365       365            0            0               0
## 32 2003/2004     2004         366       366            0            0               0
## 33 2004/2005     2005         365       365            0            0               0
## 34 2005/2006     2006         365       365            0            0               0
## 35 2006/2007     2007         365       365            0            0               0
## 36 2007/2008     2008         366       366            0            0               0
## 37 2008/2009     2009         365       365            0            0               0
## 38 2009/2010     2010         365       365            0            0               0
## 39 2010/2011     2011         365       365            0            0               0
## 40 2011/2012     2012         366       366            0            0               0
## 41 2012/2013     2013         365       365            0            0               0
## 42 2013/2014     2014         365       365            0            0               0
## 43 2014/2015     2015         365       365            0            0               0
## 44 2015/2016     2016         366       366            0            0               0
## 45 2016/2017     2017         365       365            0            0               0
## 46 2017/2018     2018         365       365            0            0               0
## 47 2018/2019     2019         365       365            0            0               0
## 48 2019/2020     2020         366       366            0            0               0
## 49 2020/2021     2021         365       365            0            0               0
## 50 2021/2022     2022         365       365            0            0               0
## 51 2022/2023     2023         365       365            0            0               0
##    Perc_complete
## 1            100
## 2            100
## 3            100
## 4            100
## 5            100
## 6            100
## 7            100
## 8            100
## 9            100
## 10           100
## 11           100
## 12           100
## 13           100
## 14           100
## 15           100
## 16           100
## 17           100
## 18           100
## 19           100
## 20           100
## 21           100
## 22           100
## 23           100
## 24           100
## 25           100
## 26           100
## 27           100
## 28           100
## 29           100
## 30           100
## 31           100
## 32           100
## 33           100
## 34           100
## 35           100
## 36           100
## 37           100
## 38           100
## 39           100
## 40           100
## 41           100
## 42           100
## 43           100
## 44           100
## 45           100
## 46           100
## 47           100
## 48           100
## 49           100
## 50           100
## 51           100
```

``` r
Yakima_temps <- Yakima_patched$weather
```


``` r
temperature_means <- 
  data.frame(Year = min(Yakima_temps$Year):max(Yakima_temps$Year),
             Tmin = aggregate(Yakima_temps$Tmin,
                              FUN = "mean",
                              by = list(Yakima_temps$Year))[,2],
             Tmax=aggregate(Yakima_temps$Tmax,
                            FUN = "mean",
                            by = list(Yakima_temps$Year))[,2]) %>%
  mutate(runn_mean_Tmin = runn_mean(Tmin,15),
         runn_mean_Tmax = runn_mean(Tmax,15))


Tmin_regression <- lm(Tmin~Year,
                      temperature_means)

Tmax_regression <- lm(Tmax~Year,
                      temperature_means)

temperature_means <- temperature_means %>%
  mutate(regression_Tmin = Tmin_regression$coefficients[1]+
           Tmin_regression$coefficients[2]*temperature_means$Year,
         regression_Tmax = Tmax_regression$coefficients[1]+
           Tmax_regression$coefficients[2]*temperature_means$Year
  )
```


``` r
# plot mean monthly minimum temperature of 1973 to 2023
ggplot(temperature_means,
       aes(Year,
           Tmin)) + 
  geom_point() + 
  geom_line(data = temperature_means,
            aes(Year,
                runn_mean_Tmin),
            lwd = 2,
            col = "blue") + 
  geom_line(data = temperature_means,
            aes(Year,
                regression_Tmin),
            lwd = 2,
            col = "red") +
  theme_bw(base_size = 15) +
  ylab("Mean monthly minimum temperature (°C)")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-258-1.png" width="672" />


``` r
# plot mean monthly maximum temperature of 1973 to 2023
ggplot(temperature_means,
       aes(Year,
           Tmax)) + 
  geom_point() + 
  geom_line(data = temperature_means,
            aes(Year,
                runn_mean_Tmax),
            lwd = 2,
            col = "blue") + 
  geom_line(data = temperature_means,
            aes(Year, 
                regression_Tmax),
            lwd = 2,
            col = "red") +
  theme_bw(base_size = 15) +
  ylab("Mean monthly maximum temperature (°C)")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-259-1.png" width="672" />

2)  *Produce chill distributions for these scenarios and plot them.*


``` r
scenario_1980 <- temperature_scenario_from_records(weather = Yakima_temps,
                                                   year = 1980)



temps_1980 <- temperature_generation(weather = Yakima_temps,
                                     years = c(1973, 2023),
                                     sim_years = c(2001, 2100),
                                     temperature_scenario = scenario_1980)
```

```
## Warning: Absolute temperature scenario specified - calibration weather record only used for
## simulating temperature variation, but not for the means
```

``` r
scenario_1998 <- temperature_scenario_from_records(weather = Yakima_temps,
                                                   year = 1998)

relative_scenario <- temperature_scenario_baseline_adjustment(
  baseline = scenario_1998,
  temperature_scenario = scenario_1980)

temps_1980 <- temperature_generation(weather = Yakima_temps,
                                   years = c(1973, 2023),
                                   sim_years = c(2001,2100),
                                   temperature_scenario = relative_scenario)

all_past_scenarios <- temperature_scenario_from_records(
  weather = Yakima_temps,
  year = c(1980,
           1990,
           2000,
           2010, 
           2020))

adjusted_scenarios <- temperature_scenario_baseline_adjustment(
  baseline = scenario_1998,
  temperature_scenario = all_past_scenarios)

all_past_scenario_temps <- temperature_generation(
  weather = Yakima_temps,
  years = c(1973, 2023),
  sim_years = c(2001, 2100),
  temperature_scenario = adjusted_scenarios)

save_temperature_scenarios(all_past_scenario_temps, "Yakima", "Yakima_hist_scenarios")

frost_model <- function(x)
  step_model(x,
             data.frame(
               lower = c(-1000,0),
               upper  = c(0,1000),
               weight = c(1,0)))

models <- list(Chill_Portions = Dynamic_Model,
               GDH = GDH,
               Frost_H = frost_model)

chill_hist_scenario_list <- tempResponse_daily_list(all_past_scenario_temps,
                                                    latitude = 46.6,
                                                    Start_JDay = 305,
                                                    End_JDay = 59,
                                                    models = models)

chill_hist_scenario_list <- lapply(chill_hist_scenario_list,
                                   function(x) x %>%
                                     filter(Perc_complete == 100))

save_temperature_scenarios(chill_hist_scenario_list, "Yakima","Yakima_hist_chill_305_59")

scenarios <- names(chill_hist_scenario_list)[1:5]

all_scenarios <- chill_hist_scenario_list[[scenarios[1]]] %>%
  mutate(scenario = as.numeric(scenarios[1]))

for (sc in scenarios[2:5])
  all_scenarios <- all_scenarios %>%
  rbind(chill_hist_scenario_list[[sc]] %>%
          cbind(
            scenario=as.numeric(sc))
  ) %>%
  filter(Perc_complete == 100)

# Let's compute the actual 'observed' chill for comparison
actual_chill <- tempResponse_daily_list(Yakima_temps,
                                        latitude=46.6,
                                        Start_JDay = 305,
                                        End_JDay = 59,
                                        models)[[1]] %>%
  filter(Perc_complete == 100)
```


``` r
ggplot(data = all_scenarios,
       aes(scenario,
           Chill_Portions,
           fill = factor(scenario))) +
  geom_violin() +
  ylab("Chill accumulation (Chill Portions)") +
  xlab("Scenario year") +
  theme_bw(base_size = 15) +
  ylim(c(0,90)) +
  geom_point(data = actual_chill,
             aes(End_year,
                 Chill_Portions,
                 fill = "blue"),
             col = "blue",
             show.legend = FALSE) +
  scale_fill_discrete(name = "Scenario",
                      breaks = unique(all_scenarios$scenario)) 
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-261-1.png" width="672" />


``` r
write.csv(actual_chill,"Yakima/Yakima_observed_chill_305_59.csv", row.names = FALSE)
```

<!--chapter:end:14-historic.Rmd-->

# Future temperature scenarios

## Learning goals for this lesson

-   Acquire background knowledge on some important concepts in climate change analysis
-   Understand how future climate projections are generated
-   Learn about the "generations" of climate models and greenhouse gas concentration scenarios
-   Appreciate that it's important to use up-to-date scenarios when you're working in this space

## Impacts of future climate change

Human-induced climate change has already left significant impacts on the climate, ecosystems, and agriculture, as confirmed by numerous studies. The situation is expected to worsen due to historically high greenhouse gas levels and ongoing emissions of about 40 Gt CO2-equivalents annually, with little sign of decline. Widespread ecosystem degradation further erodes the planet's resilience. While the future remains uncertain, including the success of mitigation efforts and ecosystems' capacity to adapt, climate change adaptation research seeks to address these uncertainties by focusing on exposure, sensitivity, and adaptive capacity.

![**Conceptual framework for evaluating vulnerability and adaptation to climate change (Luedeling, 2020)**](images/adaptation_challenge.png)

The framework for assessing climate change vulnerability and adaptation (Luedeling, 2020) includes **exposure** (expected future conditions), **sensitivity** (how the system responds), and **adaptive capacity** (the system's ability to adapt). Combining exposure and sensitivity helps estimate potential impacts, while adaptation aims to reduce sensitivity (e.g., selecting resilient cultivars) or increase adaptive capacity (e.g., implementing flexible management strategies).

Current work focuses mainly on **exposure**, as it develops future scenarios for orchards. While chill models incorporate aspects of tree sensitivity, this is only partial, so the analyses primarily align with exposure.

## Future climate scenarios

Future climate scenarios and methods for creating historical chill scenarios, including relevant technical details, have been covered. The next step involves accessing climate model predictions for the desired location.

Running climate models is a complex process, requiring precise setup of global climate models (GCMs), regional models (RCMs), and downscaling, with no consensus on a single correct approach. `chillR` functions are compatible with both high-quality and less precise scenarios. While advanced climate data or collaboration with experts is ideal, \`chillR\` includes tools to facilitate access to reliable climate databases.

### Some background on climate models and warming pathways

Until November 2023, the `ClimateWizard` database, maintained by Center for Tropical Agriculture (CIAT), was the best source of climate data available in `chillR`. Its main advantage over other sources is the ability to provide point-specific data for climate scenarios from multiple models, avoiding the need to process large-scale gridded datasets. This reduces data transfer bottlenecks, especially when dealing with Tmin and Tmax data for multiple months, models, scenarios, and downscaling methods. `ClimateWizard` simplifies this by delivering data for specified coordinates, making it a practical tool despite its limitations.Originally developed as a web tool by Dr. Evan Girvetz, `ClimateWizard` can also be accessed via an API, streamlining data retrieval without navigating through a web interface. However, the database does not include the latest climate scenarios, such as those from CMIP6, which represents the current state of climate science and incorporates updated Shared Socioeconomic Pathways (SSPs). These SSPs, released in 2021, are now the recommended scenarios for generating state-of-the-art projections. `ClimateWizard` remains based on the older CMIP5 models and the outdated Representative Concentration Pathways (RCPs), offering only two RCP scenarios that fail to encompass the full range of plausible future climates. While these RCP scenarios were useful initially, they are increasingly unsuitable for publishing credible results. Instructions for using `ClimateWizard` with CMIP5 data are still provided, but transitioning to CMIP6 data and SSP scenarios is strongly recommended for up-to-date analyses.

## `Exercises` on future temperature scenarios

Please document all results of the following assignments in your `learning logbook`.

1)  *Briefly describe the differences between the RCPs and the SSPs (you may have to follow some of the links provided above).*

The Representative Concentration Pathways (RCPs) and the Shared Socioeconomic Pathways (SSPs) are both scenario frameworks used for modeling future climate developments, but they differ in their methodology and focus.

-   **RCPs (Representative Concentration Pathways)**:

    -   Developed for the IPCC's 5th Assessment Report (AR5, published in 2014).

    -   Describe different possible levels of radiative forcing (W/m²) by 2100, meaning the direct effect of greenhouse gas emissions on the climate.

    -   Four main pathways: RCP2.6 (strong emissions reduction), RCP4.5 and RCP6.0 (moderate emissions), RCP8.5 (very high emissions, often referred to as "business as usual").

    -   A purely climate-science-based approach without considering socioeconomic developments.

-   **SSPs (Shared Socioeconomic Pathways)**:

    -   Developed for the IPCC's 6th Assessment Report (AR6, published in 2021).

    -   Combine socioeconomic developments with emission pathways to create different future scenarios.

    -   Five main scenarios (SSP1 to SSP5), representing various societal, economic, and political trajectories, such as sustainable development (SSP1) or continued reliance on fossil fuels (SSP5).

    -   Can be combined with different radiative forcing levels (e.g., SSP1-2.6 for sustainable development with low emissions or SSP5-8.5 for high emissions and fossil fuel dependence).

**Summary**:\
RCPs focus solely on emissions and their impact on radiative forcing, while SSPs incorporate socioeconomic factors, making them more comprehensive and flexible for climate projections. SSPs are considered more modern and detailed in representing possible climate futures.

<!--chapter:end:15-future.Rmd-->

# Making CMIP6 scenarios



Running this code requires `chillR` version \>= 0.76, which is available on CRAN. Earlier versions should not be used for CMIP6 projections.

## Learning goals for this lesson

-   Learn how to download future temperature projections for a CMIP6 ensemble from the Copernicus database
-   Be able to produce synthetic temperature scenarios for an ensemble of future climate scenarios
-   Transfer knowledge you gained earlier to compute temperature-based agroclimatic metrics for all the historic temperature records, as well as for past and future temperature scenarios
-   Learn how to plot all your results in a concise manner

## Accessing gridded climate data from the Copernicus climate data store

Most future climate data comes in the form of grids, meaning that to obtain information for a specific location, large files containing data for other locations must often be downloaded. For CMIP5 scenarios, the `ClimateWizard` API allowed access to specific point locations. However, a similar tool is not available for CMIP6 scenarios, which are currently the most advanced. As a result, downloading gridded data may be necessary, though it is more cumbersome than using `ClimateWizard`.

The [Copernicus Climate Data Store (CDS)](https://cds.climate.copernicus.eu/), maintained by the European Centre for Medium-Range Weather Forecasts, offers a reliable source of future climate data. To access this data, an API key and user ID are required. Users must create a free account on the CDS website to obtain these credentials. After registration, navigate to the user profile to retrieve the User ID and Access Token. After agreeing to the Terms of Use, the code will work to download the data.

### Downloading future climate data

To download data using the `download_cmip6_ecmwfr` function, the download area must be specified. The data will be saved locally, so it is important to carefully choose the extent. A small extent can be selected if only data for a single station is needed, while a larger area should be chosen for multiple stations, especially if they are close together.

For example, for Bonn (located at approximately 7.1°E, 50.8°N), a small extent can be selected around this location. The extent is specified as a vector in the format:

`c(maximum latitude,minimum longitude,minimum latitude,maximum longitude)`

This allows for downloading the required data and storing it locally to avoid future downloads.


``` r
location = c(7.1, 50.8)
area <- c(52, 6, 50, 8)
```

The `download_cmip6_ecmwfr` function includes a default set of models, which can be used for downloading data. In this case, data for SSP1 (ssp126) will be selected for the download. By using this function, it is possible to specify the models and scenarios needed, while focusing on the specific SSP scenario of interest for the analysis.


``` r
download_cmip6_ecmwfr(
  scenarios = 'ssp126', 
  area =  area,
  user = 'write user id here',
  key = 'write key here',
  model = 'default',
  frequency = 'monthly',
  variable = c('Tmin', 'Tmax'),
  year_start = 2015,
  year_end = 2100)
```



After running the `download_cmip6_ecmwfr` function, several files are generated in a subfolder of the working directory, typically named `cmip6_downloaded`, unless the folder name is specified using the `path_download` parameter. If the function encounters models for which no data is available based on the provided specifications, a message about "Dropped models" appears. These models are blacklisted to prevent future download attempts, and a note is added to the download folder.

Once the initial download is successful, additional SSP scenarios can be downloaded by providing a vector of scenarios to the `scenarios` parameter. For example, SSP126, SSP245, SSP370, and SSP585 can be selected. Since the function automatically detects previously downloaded data, it will skip any files that are already present, allowing for efficient downloading without redundancy.


``` r
download_cmip6_ecmwfr(
  scenarios = c("ssp126", "ssp245", "ssp370", "ssp585"), 
  area = area,
  user = 'write user id here'
  key = 'write key here',
  model = 'default',
  frequency = 'monthly',
  variable = c('Tmin', 'Tmax'),
  year_start = 2015,
  year_end = 2100)
```



### Generating change scenarios

The data downloaded so far, stored in the `cmip6_downloaded/52_6_50_8` folder, represents future climate projections starting from 2015. However, these data are based on coarse-resolution climate models, where each pixel averages large areas, potentially including diverse landscapes like rivers, mountains, and coastal regions. As a result, these projections may not accurately represent the local temperature conditions of a specific place.

For site-specific analyses, such coarse data might not be sufficient. Although landscape features significantly influence rainfall patterns, their effect on temperature dynamics is less pronounced. Therefore, while the future temperature data might not be directly usable, the temperature change projected by these models can still be useful. For example, if a model projects a 2°C increase in January temperatures for a future scenario, this change can be added to current temperature observations.

However, it's crucial to determine what "today" refers to when discussing climate change. The baseline temperature used for comparison affects the projected warming. A 2°C increase applied to a cooler climate from 1850 will be different from applying it to today's warmer conditions. In the `chillR` workflow for CMIP6 data, the default baseline period is 1986-2014, as this period is available in the Copernicus database, represents a good median year (2000), and is close to the 30 years commonly used by climate scientists for robust climatology.

To generate accurate change scenarios, it's essential to subtract the conditions during the baseline period from the future projections, ensuring that both the baseline and future data come from the same climate model. Historical data for the same models can be retrieved using the `download_baseline_cmip6_ecmwfr` function.


``` r
download_baseline_cmip6_ecmwfr(
  area = area,
  user = 'write user id here'
  key = 'write key here',
  model = 'match_downloaded',
  frequency = 'monthly',
  variable = c('Tmin', 'Tmax'),
  year_start = 1986, 
  year_end = 2014, 
  month = 1:12)
```



By specifying `models = match_downloaded`, the function will automatically identify the downloaded models and retrieve the corresponding baseline data.

### Extracting data from the grids

The downloaded data is still in a gridded format, so the data for the specific location needs to be extracted. A small `data.frame` is created containing the station name and coordinates for Bonn. While additional stations could be added, only Bonn is considered in this case. The `extract_cmip6_data` function is then used to extract the data for the specified location.


``` r
station <- data.frame(
  station_name = c("Bonn"),
  longitude = c(7.1),
  latitude = c(50.8))

extracted <- extract_cmip6_data(stations = station)
```



Let's look at some of the data for one of the climate models.


``` r
head(extracted$`ssp126_AWI-CM-1-1-MR`)
```



<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;"> Date </th>
   <th style="text-align:center;"> Year </th>
   <th style="text-align:center;"> Month </th>
   <th style="text-align:center;"> Day </th>
   <th style="text-align:center;"> lat </th>
   <th style="text-align:center;"> lon </th>
   <th style="text-align:center;"> location </th>
   <th style="text-align:center;"> model </th>
   <th style="text-align:center;"> ssp </th>
   <th style="text-align:center;"> Tmin </th>
   <th style="text-align:center;"> Tmax </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 2015-01-16 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> -13.6960 </td>
   <td style="text-align:center;"> 10.8620 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015-02-15 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> -3.2364 </td>
   <td style="text-align:center;"> 12.8374 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015-03-16 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> -2.8993 </td>
   <td style="text-align:center;"> 13.5311 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015-04-16 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> 0.0531 </td>
   <td style="text-align:center;"> 21.7272 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015-05-16 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> 3.9305 </td>
   <td style="text-align:center;"> 22.6927 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2015-06-16 </td>
   <td style="text-align:center;"> 2015 </td>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> 50.9608 </td>
   <td style="text-align:center;"> 7.5 </td>
   <td style="text-align:center;"> Bonn </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
   <td style="text-align:center;"> ssp126 </td>
   <td style="text-align:center;"> 7.7302 </td>
   <td style="text-align:center;"> 24.7364 </td>
  </tr>
</tbody>
</table>

Since the baseline data is stored in the same folder, a compact call can now be used to generate change scenarios for all the climate projections in that folder.


``` r
change_scenarios <- gen_rel_change_scenario(extracted)
head(change_scenarios)
```



<table class="table table-striped" style="font-size: 10px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:left;"> location </th>
   <th style="text-align:right;"> Month </th>
   <th style="text-align:right;"> Tmax </th>
   <th style="text-align:right;"> Tmin </th>
   <th style="text-align:left;"> scenario </th>
   <th style="text-align:right;"> start_year </th>
   <th style="text-align:right;"> end_year </th>
   <th style="text-align:right;"> scenario_year </th>
   <th style="text-align:right;"> reference_year </th>
   <th style="text-align:left;"> scenario_type </th>
   <th style="text-align:left;"> labels </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 1.826612 </td>
   <td style="text-align:right;"> 1.803455 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 2.765976 </td>
   <td style="text-align:right;"> 2.179606 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 1.485612 </td>
   <td style="text-align:right;"> 1.170670 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:right;"> 1.501575 </td>
   <td style="text-align:right;"> 1.264827 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 1.733385 </td>
   <td style="text-align:right;"> 1.485717 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Bonn </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 1.808780 </td>
   <td style="text-align:right;"> 1.506125 </td>
   <td style="text-align:left;"> ssp126 </td>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 2065 </td>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:left;"> relative </td>
   <td style="text-align:left;"> ACCESS-CM2 </td>
  </tr>
</tbody>
</table>

The data is stored in a single long data frame, which can easily be saved as a `csv` file. While this format isn't directly compatible with the weather generator, `chillR` provides a conversion function called `convert_scen_information`. This function extracts the relevant information and creates scenarios that are compatible with the `temperature_generation` function.


``` r
write.csv(change_scenarios, "data/all_change_scenarios.csv", row.names = FALSE)

scen_list <- convert_scen_information(change_scenarios)
```

The `convert_scen_information` function can also be used to convert the list back into the data.frame format, making it easier to work with for further analysis or processing.


``` r
scen_frame <- convert_scen_information(scen_list)
```

Let's look at one of the elements in the scenario lists.


``` r
scen_list$Bonn$ssp126$`ACCESS-CM2`$'2050'
```

```
## $data
##        Tmin     Tmax
## 1  1.803455 1.826612
## 2  2.179606 2.765976
## 3  1.170670 1.485612
## 4  1.264827 1.501575
## 5  1.485717 1.733385
## 6  1.506125 1.808780
## 7  2.047910 2.668619
## 8  1.654944 2.754484
## 9  2.388600 3.323390
## 10 2.540916 2.722248
## 11 2.322483 2.434944
## 12 2.737679 2.713174
## 
## $scenario
## [1] "ssp126"
## 
## $start_year
## [1] 2035
## 
## $end_year
## [1] 2065
## 
## $scenario_year
## [1] 2050
## 
## $reference_year
## [1] 2000
## 
## $scenario_type
## [1] "relative"
## 
## $labels
## [1] "ACCESS-CM2"
```

The scenario includes changes for the mean daily minimum and maximum temperatures for each month, along with several key pieces of information. The `scenario` specifies the SSP scenario, `scenario_type` indicates that this is a relative scenario, and `labels` contain the name of the GCM. The four attributes related to years—`start_year`, `end_year`, and `scenario_year`—define the time slice for the scenario. In this case, the scenario covers a 31-year period (2035-2065), with the median year (2050) being the `scenario_year`, which represents the year most typical for the scenario. The `reference_year` is also crucial, as it specifies the year to which the temperature change is relative—in this case, the changes are relative to conditions in 2000.

### Baseline adjustment

To produce future scenarios, while ensuring that the weather generator simulates temperatures for Bonn specifically, the observed data from Bonn can be used as input. This approach ensures that the temperatures generated reflect local conditions, rather than the average conditions from a GCM pixel. The weather generator can accommodate this, so the next step is to test it with one of the scenarios.




``` r
Bonn_temps<-read_tab("data/Bonn_temps.csv")

temperature_generation(Bonn_temps, 
                       years = c(1973, 2019),
                       sim_years = c(2001, 2100),
                       scen_list$Bonn$ssp126$`ACCESS-CM2`)
```

The attempt to use the weather generator with the scenario failed due to a mismatch in the reference years. The reference year for the weather station data is 1996, while the future projections have a reference year of 2000. One solution would be to use fewer observation years, such as from 1981 onward, to align the median year with 2000. However, if it's important to include older data, `chillR` provides a tool to adjust the reference year based on temperature trends within the observed dataset.

To adjust the baseline of the observed weather, the first step is to calculate the warming (or cooling) that occurred in Bonn between 1996 and 2000. This can be done by determining typical temperature conditions for both years using the `temperature_scenario_from_records` function.


``` r
temps_1996 <- temperature_scenario_from_records(Bonn_temps,
                                                1996)

temps_2000 <- temperature_scenario_from_records(Bonn_temps,
                                                2000)

temps_1996
```

```
## $`1996`
## $`1996`$data
##           Tmin      Tmax
## 1   0.05096808  5.997514
## 2   0.30177644  7.789863
## 3   2.64832507 11.855124
## 4   4.11737331 14.884386
## 5   7.96058170 20.280445
## 6  10.70945702 22.325216
## 7  12.69138958 24.926619
## 8  12.59137274 25.079171
## 9   9.55441331 19.960842
## 10  6.40661969 14.768213
## 11  2.82059109  9.308959
## 12  0.59133654  6.103919
## 
## $`1996`$scenario_year
## [1] 1996
## 
## $`1996`$reference_year
## [1] NA
## 
## $`1996`$scenario_type
## [1] "absolute"
## 
## $`1996`$labels
## [1] "running mean scenario"
```

``` r
temps_2000
```

```
## $`2000`
## $`2000`$data
##           Tmin      Tmax
## 1   0.09999567  5.888243
## 2   0.49262403  7.189344
## 3   2.28327954 11.206499
## 4   4.71243331 15.764268
## 5   8.47223725 20.053640
## 6  11.06525924 22.935700
## 7  13.05258062 25.085306
## 8  12.50049711 24.345505
## 9  10.00307775 20.264008
## 10  6.84396341 15.241450
## 11  3.12942664  9.319114
## 12  0.75037488  6.036563
## 
## $`2000`$scenario_year
## [1] 2000
## 
## $`2000`$reference_year
## [1] NA
## 
## $`2000`$scenario_type
## [1] "absolute"
## 
## $`2000`$labels
## [1] "running mean scenario"
```

The temperature scenarios for 1996 and 2000 are absolute scenarios, describing typical temperature conditions for each year. Using these, a relative change scenario can now be computed to represent the temperature changes that occurred over this period. This is done with the `temperature_scenario_baseline_adjustment` function, which adjusts the baseline based on the observed temperature trends between the two years.


``` r
base <- temperature_scenario_baseline_adjustment(temps_1996,
                                                 temps_2000)

base
```

```
## $`2000`
## $`2000`$data
##           Tmin        Tmax
## 1   0.04902759 -0.10927019
## 2   0.19084759 -0.60051936
## 3  -0.36504552 -0.64862502
## 4   0.59506000  0.87988164
## 5   0.51165555 -0.22680567
## 6   0.35580222  0.61048386
## 7   0.36119103  0.15868680
## 8  -0.09087563 -0.73366588
## 9   0.44866444  0.30316609
## 10  0.43734372  0.47323734
## 11  0.30883555  0.01015498
## 12  0.15903835 -0.06735621
## 
## $`2000`$scenario_year
## [1] 2000
## 
## $`2000`$reference_year
## [1] 1996
## 
## $`2000`$scenario_type
## [1] "relative"
## 
## $`2000`$labels
## [1] "running mean scenario"
```

The baseline correction can now be applied to the climate scenarios. Since this process currently only works with an unstructured list of scenarios, the scenarios must first be converted using the `give_structure = FALSE` option before applying the correction.


``` r
scen_list <- convert_scen_information(change_scenarios, 
                                      give_structure = FALSE)

adjusted_list <- 
  temperature_scenario_baseline_adjustment(
    base,
    scen_list,
    temperature_check_args =
      list( scenario_check_thresholds = c(-5, 15)))
```

The temperature generation process can now begin. Given the large number of scenarios, it may take hours to complete. While this might seem like a long time, it’s important to remember that the computer is handling numerous operations that would otherwise be done manually.


``` r
temps <- temperature_generation(Bonn_temps, 
                                years = c(1973, 2019), 
                                sim_years = c(2001, 2100), 
                                adjusted_list,    
                                temperature_check_args =
                                  list( scenario_check_thresholds = c(-5, 15)))

save_temperature_scenarios(temps,
                           "data/future_climate",
                           "Bonn_futuretemps")
```

It's important to save the data now to avoid waiting for the process to run again in the future.

Next, temperature responses can be calculated efficiently using the `tempResponse_daily_list` function. For this calculation, three models are selected: the Dynamic Model for chill accumulation, the GDH model for heat accumulation, and a simple model to compute frost hours.


``` r
frost_model <- function(x)
  step_model(x,
             data.frame(
               lower = c(-1000, 0),
               upper = c(0, 1000),
               weight = c(1, 0)))

models <- list(Chill_Portions = Dynamic_Model,
               GDH = GDH,
               Frost_H = frost_model)
```


``` r
chill_future_scenario_list <- tempResponse_daily_list(temps,
                                                    latitude = 50.8,
                                                    Start_JDay = 305,
                                                    End_JDay = 59,
                                                    models = models)

chill_future_scenario_list <- lapply(chill_future_scenario_list,
                                     function(x) x %>%
                                       filter(Perc_complete == 100))

save_temperature_scenarios(chill_future_scenario_list,
                           "data/future_climate",
                           "Bonn_futurechill_305_59")
```



To facilitate plotting later, climate scenarios are first generated using the `make_climate_scenario` function in chillR. The plotting function will process a list of these scenarios. The starting point is a historic scenario, which includes both distributions for historical years and the observed chill. These records, ideally saved in the "Historic temperature scenarios" lesson, are now loaded for further use.


``` r
chill_hist_scenario_list<-load_temperature_scenarios("data",
                                                     "Bonn_hist_chill_305_59")

observed_chill <- read_tab("data/Bonn_observed_chill_305_59.csv")


chills <- make_climate_scenario(
  chill_hist_scenario_list,
  caption = "Historical",
  historic_data = observed_chill,
  time_series = TRUE)

plot_climate_scenarios(
  climate_scenario_list = chills,
  metric = "Chill_Portions",
  metric_label = "Chill (Chill Portions)")
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-289-1.png" width="672" />

```
## [[1]]
## [1] "time series labels"
```

The function had two outcomes: it generated a plot and returned a brief list with the message "time series labels." While this message may not be of immediate interest, it will contain more relevant content later. To store the information without displaying the plot, the plotting command can be assigned to a new object (e.g., `info <- plot_climate_scenarios(...)`), allowing the function to produce the plot as a side effect.

The same process is repeated for all future climate scenarios. For each scenario, it is added to the chills object using the `make_climate_scenario` function’s `add_to` argument. Before proceeding, the data must first be sorted by the specific combinations of SSP and time.


``` r
SSPs <- c("ssp126", "ssp245", "ssp370", "ssp585")
Times <- c(2050, 2085)

list_ssp <- 
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(2) %>%
  unlist()

list_gcm <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(3) %>%
  unlist()

list_time <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(4) %>%
  unlist()


for(SSP in SSPs)
  for(Time in Times)
    {
    
    # find all scenarios for the ssp and time
    chill <- chill_future_scenario_list[list_ssp == SSP & list_time == Time]
    names(chill) <- list_gcm[list_ssp == SSP & list_time == Time]
    if(SSP == "ssp126") SSPcaption <- "SSP1"
    if(SSP == "ssp245") SSPcaption <- "SSP2"
    if(SSP == "ssp370") SSPcaption <- "SSP3"
    if(SSP == "ssp585") SSPcaption <- "SSP5"    
    if(Time == "2050") Time_caption <- "2050"
    if(Time == "2085") Time_caption <- "2085"
    chills <- chill %>% 
      make_climate_scenario(
        caption = c(SSPcaption,
                    Time_caption),
        add_to = chills)
}
```

At this point, all the necessary data and steps are in place to plot the results of the climate change analysis:


``` r
info_chill <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "Chill_Portions",
    metric_label = "Chill (Chill Portions)",
    texcex = 1.5)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-291-1.png" width="672" />


``` r
info_heat <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "GDH",
    metric_label = "Heat (Growing Degree Hours)",
    texcex = 1.5)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-292-1.png" width="672" />


``` r
info_frost <-
 plot_climate_scenarios(
   climate_scenario_list=chills,
   metric="Frost_H",
   metric_label="Frost hours",
   texcex=1.5)
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-293-1.png" width="672" />

Now that everything is set up, the trends in chill and heat accumulation, as well as in frost hours for Klein-Altendorf, can be visualized. The function not only produces the plot but also returns supplementary information, which was stored in the `info` objects. By inspecting these objects, it is possible to see the names of the climate models for each subplot, along with the time series labels for the historic plot. Since the same models were used for each scenario, this information is repeated multiple times. To avoid redundancy, it’s best to review this data once, focusing on just one of the plots.


``` r
info_chill[[2]]
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:center;"> code </th>
   <th style="text-align:center;"> Label </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 1 </td>
   <td style="text-align:center;"> CMCC-ESM2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> ACCESS-CM2 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 3 </td>
   <td style="text-align:center;"> AWI-CM-1-1-MR </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> MIROC6 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5 </td>
   <td style="text-align:center;"> FIO-ESM-2-0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 6 </td>
   <td style="text-align:center;"> CNRM-CM6-1-HR </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 7 </td>
   <td style="text-align:center;"> INM-CM5-0 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 8 </td>
   <td style="text-align:center;"> NESM3 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> EC-Earth3-Veg-LR </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> GFDL-ESM4 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 11 </td>
   <td style="text-align:center;"> MPI-ESM1-2-LR </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> CNRM-ESM2-1 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 13 </td>
   <td style="text-align:center;"> IPSL-CM6A-LR </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 14 </td>
   <td style="text-align:center;"> FGOALS-g3 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 15 </td>
   <td style="text-align:center;"> INM-CM4-8 </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 16 </td>
   <td style="text-align:center;"> MRI-ESM2-0 </td>
  </tr>
</tbody>
</table>

The labels are not included directly in the plot to avoid overcrowding the visualization. Instead, each model is represented by a number, with a key provided in a separate table to explain these number codes.

If the design of the figure is not preferred, a customized version can be created later. Additionally, a more modern version of the plot, available in `chillR`, will be explored in later steps.

## `Exercises` on generating CMIP6 temperature scenarios

Please document all results of the following assignments in your `learning logbook`.

1)  *Analyze the historic and future impact of climate change on two agroclimatic metrics of your choice, for the location you've chosen for your earlier analyses.*




``` r
# set location
location = c(-120.5, 46.6)
area <- c(48, -122 , 45, -119)


# download scenarios 
download_cmip6_ecmwfr(
  scenarios = c("ssp126", "ssp245", "ssp370", "ssp585"), 
  area = c(49, -122 , 44, -118),
  user = 'd78103f2-834f-468c-94f0-8b7064c75df7',
  key = 'ac66d05a-e82b-42d1-9a8d-a94c1afb9fb9',
  model = 'default',
  frequency = 'monthly',
  variable = c('Tmin', 'Tmax'),
  year_start = 2015,
  year_end = 2100)


# download baseline
download_baseline_cmip6_ecmwfr(
  area = c(49, -122 , 44, -118),
  user = 'd78103f2-834f-468c-94f0-8b7064c75df7',
  key = 'ac66d05a-e82b-42d1-9a8d-a94c1afb9fb9',
  model = 'match_downloaded',
  frequency = 'monthly',
  variable = c('Tmin', 'Tmax'),
  year_start = 1986, 
  year_end = 2014, 
  month = 1:12)


#
station <- data.frame(
  station_name = c("Yakima"),
  longitude = c(-120.5),
  latitude = c(46.6))

extracted <- extract_cmip6_data(stations = station,
                                download_path = "cmip6_downloaded/49_-122_44_-118")


change_scenarios <- gen_rel_change_scenario(extracted)

scen_list <- convert_scen_information(change_scenarios)

temps_1996 <- temperature_scenario_from_records(Yakima_temps,
                                                1996)

temps_2000 <- temperature_scenario_from_records(Yakima_temps,
                                                2000)

base <- temperature_scenario_baseline_adjustment(temps_1996,
                                                 temps_2000)

scen_list <- convert_scen_information(change_scenarios, 
                                      give_structure = FALSE)

adjusted_list <- temperature_scenario_baseline_adjustment(base,
                                                          scen_list,
                                                          temperature_check_args =
                                                            list(scenario_check_thresholds = c(-5, 15)))

for(scen in 1:length(adjusted_list))
{
  if(!file.exists(paste0("Yakima/future_climate/Yakima_future_",
                         scen,"_",
                         names(adjusted_list)[scen],".csv")) )
  {temp_temp <- temperature_generation(Yakima_temps,
                                       years = c(1973, 2019),
                                       sim_years = c(2001, 2100),
                                       adjusted_list[scen],  
                                       temperature_check_args = 
                                         list( scenario_check_thresholds = c(-5, 15)))
  write.csv(temp_temp[[1]],paste0("Yakima/future_climate/Yakima_future_",scen,"_",names(adjusted_list)[scen],".csv"),
            row.names=FALSE)
  print(paste("Processed object",scen,"of", length(adjusted_list)))
  
  
  }
  
}


frost_model <- function(x)
  step_model(x,
             data.frame(
               lower=c(-1000,0),
               upper=c(0,1000),
               weight=c(1,0)))

models <- list(Chill_Portions = Dynamic_Model,
               GDH = GDH,
               Frost_H = frost_model)

temps <- load_temperature_scenarios("Yakima/future_climate","Yakima_future_")

chill_future_scenario_list <- tempResponse_daily_list(temps,
                                                      latitude = 46.6,
                                                      Start_JDay = 305,
                                                      End_JDay = 59,
                                                      models = models)

chill_future_scenario_list <- lapply(chill_future_scenario_list,
                                     function(x) x %>%
                                       filter(Perc_complete == 100))

save_temperature_scenarios(chill_future_scenario_list,
                           "Yakima/future_climate",
                           "Yakima_futurechill_305_59")
chill_hist_scenario_list <- load_temperature_scenarios("Yakima",
                                                       "Yakima_hist_chill_305_59")

observed_chill <- read_tab("Yakima/Yakima_observed_chill_305_59.csv")


chills <- make_climate_scenario(
  chill_hist_scenario_list,
  caption = "Historic",
  historic_data = observed_chill,
  time_series = TRUE)

plot_climate_scenarios(
  climate_scenario_list = chills,
  metric = "Chill_Portions",
  metric_label = "Chill (Chill Portions)")

SSPs <- c("ssp126", "ssp245", "ssp370", "ssp585")
Times <- c(2050, 2085)

list_ssp <- 
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(2) %>%
  unlist()

list_gcm <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(3) %>%
  unlist()

list_time <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(4) %>%
  unlist()


for(SSP in SSPs)
  for(Time in Times)
  {
    
    chill <- chill_future_scenario_list[list_ssp == SSP & list_time == Time]
    names(chill) <- list_gcm[list_ssp == SSP & list_time == Time]
    if(SSP == "ssp126") SSPcaption <- "SSP1"
    if(SSP == "ssp245") SSPcaption <- "SSP2"
    if(SSP == "ssp370") SSPcaption <- "SSP3"  
    if(SSP == "ssp585") SSPcaption <- "SSP5"    
    if(Time == "2050") Time_caption <- "2050"
    if(Time == "2085") Time_caption <- "2085"
    chills <- chill %>% 
      make_climate_scenario(
        caption = c(SSPcaption,
                    Time_caption),
        add_to = chills)
  }

# Plot chill hours
info_chill <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "Chill_Portions",
    metric_label = "Chill (Chill Portions)",
    texcex = 1.5)

# Plot Heat (Growing degree hours)
info_heat <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "GDH",
    metric_label = "Heat (Growing Degree Hours)",
    texcex = 1.5)
```

<!--chapter:end:16-cmip6.Rmd-->

# Making CMIP5 scenarios with the `ClimateWizard`




***Note that this chapter only deals with CMIP5 climate scenarios. For methods to produce CMIP6 scenarios refer to the chapter on [Making CMIP6 scenarios]*** 

## Learning goals for this lesson {-#goals_ClimateWizard}

- Learn how to download future temperature projections from the ClimateWizard database
- Be able to produce synthetic temperature scenarios for an ensemble of future climate scenarios
- Transfer knowledge you gained earlier to compute temperature-based agroclimatic metrics for all the historic temperature records, as well as for past and future temperature scenarios
- Learn how to plot all your results in a concise manner

## Using the `ClimateWizard`

Here we'll use the `ClimateWizard` tool to download some future data, produced by the CMIP5 models for the RCPs 4.5 and 8.5 (these are the only scenarios that are available there). I should note here that the `ClimateWizard` service has been down from time to time, so the following code doesn't always work.

We'll first look at a small example to familiarize ourselves with the way this function works:


``` r
getClimateWizardData(coordinates = c(longitude = 10.61,
                                     latitude = 34.93),
                     scenario = "rcp45",
                     start_year = 2020,
                     end_year = 2050,
                     metric = c("CD18", "R02"),
                     GCMs = c("bcc-csm1-1", "BNU-ESM"))
```

This code only downloaded data for two GCMs and one RCP scenario. We're accessing two climate metrics:
  
  - "CD18" - cooling degree days (>18°C)
- "R02" - the annual number of wet days > 0.2 mm/day

We'll get mean values of all years from 2020 to 2050 for a position with longitude=10.61 and latitude=34.93 (somewhere in Tunisia).

These metrics aren't of interest to us, and we'd rather use data from Bonn than Tunisia. Also we'd like to have data for all the climate models in the dataset and for both RCPs (there are only two in the database unfortunately). Finally, since we want to use these data for producing temperature scenarios for our weather generator, we'd like to get information on expected future $T_{min}$ and $T_{max}$ values. Since the latter is a pretty standard objective in the context of `chillR`, the default option for the `metric` parameter is actually the string `monthly_min_max_temps`, which instructs the function to download all the information we need for the weather generator.

There is no automated function for downloading multiple RCPs or multiple points in time, but we can easily implement this using `for` loops. We still have to decide what baseline period we want to use for our analysis. 

The weather record from Bonn goes from 1973 to 2019. Unfortunately, the `ClimateWizard` database requires the baseline period to be a 20-year interval between 1950 and 2005. Since climate has been changing over the 71-year span we have data for, we may want to choose an interval towards the end of this period. Let's therefore select the 31-year interval between 1975 and 2005 (I'm using 31 years, because then the median year is an integer - this isn't necessary, but somehow more aesthetically pleasing than some .5 business). The median year is now 1990.

We'll save the temperature scenarios after download to make sure we don't have to download them again (this takes quite a while). 


``` r
RCPs <- c("rcp45",
          "rcp85")
Times <- c(2050,
           2085)

for(RCP in RCPs)
  for(Time in Times)
  {start_year <- Time - 15
  end_year <- Time + 15
  clim_scen <-
    getClimateWizardData(
      c(longitude = 7.143,
        latitude = 50.866),
      RCP,
      start_year,
      end_year,
      temperature_generation_scenarios = TRUE,
      baseline =c(1975, 2005),
      metric = "monthly_min_max_temps",
      GCMs = "all")
  save_temperature_scenarios(clim_scen,
                             "data/ClimateWizard",
                             paste0("Bonn_futures_",Time,"_",RCP))}
```

So we selected a period from 1975 to 2005 as the baseline for the future climate data. We could now also restrict the observed weather data used for calibrating the weather generator to the same interval. That would make some sense, but let's say we want to use all of our observed data, which ranges from 1973 to 2019. The median of this period is 1996, which is different from 1990. So we need a baseline adjustment:


``` r
scenario_1990 <- Bonn_temps %>%
  temperature_scenario_from_records(1990)
scenario_1996 <- Bonn_temps %>%
  temperature_scenario_from_records(1996)
adjustment_scenario <-
  temperature_scenario_baseline_adjustment(scenario_1996,
                                           scenario_1990)

print(adjustment_scenario)
```

```
## $`1990`
## $`1990`$data
##           Tmin       Tmax
## 1  -0.99587560 -0.6454233
## 2  -1.86685715 -1.5703307
## 3  -1.20041969 -1.2117587
## 4  -0.68921998 -0.3348927
## 5  -0.68852579 -1.2886948
## 6  -0.37833257 -1.0643560
## 7  -0.02411646 -0.4542211
## 8  -0.43258994 -0.7959042
## 9  -0.46712220 -0.6622015
## 10 -0.10242399  0.4056240
## 11 -0.52490664 -0.1442660
## 12 -0.10446557  0.3855606
## 
## $`1990`$scenario_year
## [1] 1990
## 
## $`1990`$reference_year
## [1] 1996
## 
## $`1990`$scenario_type
## [1] "relative"
## 
## $`1990`$labels
## [1] "running mean scenario"
```

We see that the reference year is now 1996. This is correct, because this scenario will be used for temperature generation, where we'll use the whole observed record for calibration. This adjustment scenario will have to be applied to all downloaded weather scenarios.

We first need to select the RCPs and scenario years for our analysis:
  

``` r
RCPs <- c("rcp45",
          "rcp85")
Times <- c(2050,
           2085)
```

Now we load the saved scenarios again. Saving and loading wouldn't be absolutely necessary of course, but it really comes in handy when our computer crashes, we accidentally close RStudio etc. The `load_ClimateWizard_scenarios` function was specifically written to load such scenarios.

We'll also add the baseline adjustment and the temperature generation step here, and then save the generated weather:
  

``` r
for(RCP in RCPs)
  for(Time in Times)
  {
    clim_scen <- load_ClimateWizard_scenarios(
      "data/climateWizard",
      paste0("Bonn_futures_",
             Time,
             "_",
             RCP))
    
    clim_scen_adjusted <-
      temperature_scenario_baseline_adjustment(
        baseline_temperature_scenario = adjustment_scenario,
        temperature_scenario = clim_scen)
    
    Temps <- temperature_generation(
      weather = Bonn_temps, 
      years = c(1973,
                2019),
      sim_years = c(2001,
                    2101),
      temperature_scenario = clim_scen_adjusted)
    
    save_temperature_scenarios(
      Temps,
      "data/Weather_ClimateWizard",
      paste0("Bonn_",
             Time,
             "_",
             RCP))
  }
```

This took quite a while, but now we have all the future temperature data we need for our scenario analysis, and all of this is saved to disk. So we don't have to run this code again.

Let's add some historic scenarios though. This is similar to what we've done before. I'll make scenarios corresponding to 1980, 1990, 2000 and 2010.


``` r
all_past_scenarios <- temperature_scenario_from_records(
  weather = Bonn_temps,
  year = c(1980,
           1990,
           2000,
           2010))

adjusted_scenarios <- temperature_scenario_baseline_adjustment(
  baseline = scenario_1996,
  temperature_scenario = all_past_scenarios)

all_past_scenario_temps <- temperature_generation(
  weather = Bonn_temps,
  years = c(1973,
            2019),
  sim_years = c(2001,
                2101),
  temperature_scenario = adjusted_scenarios)

save_temperature_scenarios(
  all_past_scenario_temps,
  "data/Weather_ClimateWizard",
  "Bonn_historic")
```


Now all we have to do is follow the steps we used to make our historic scenarios. The `tempResponse_daily_list` function makes this reasonably easy. Let's first make a list of models we want to apply - I'm choosing the Dynamic Model for chill, the Growing Degree Hours model for heat, and a frost model here: 
  

``` r
frost_model <- function(x)
  step_model(x,
             data.frame(
               lower=c(-1000,0),
               upper=c(0,1000),
               weight=c(1,0)))

models <- list(Chill_Portions = Dynamic_Model,
               GDH = GDH,
               Frost_H = frost_model)
```

Now let's first apply these models to the historic data, both the scenarios and the observed temperatures:


``` r
Temps <- load_temperature_scenarios("data/Weather_ClimateWizard",
                                    "Bonn_historic")

chill_past_scenarios <-
  Temps %>%
  tempResponse_daily_list(
    latitude = 50.866,
    Start_JDay = 305,
    End_JDay = 59,
    models = models,
    misstolerance = 10)
chill_observed <- 
  Bonn_temps %>%
  tempResponse_daily_list(
    latitude = 50.866,
    Start_JDay = 305,
    End_JDay = 59,
    models = models,
    misstolerance = 10)

save_temperature_scenarios(chill_past_scenarios,
                           "data/chill_ClimateWizard",
                           "Bonn_historic")
save_temperature_scenarios(chill_observed,
                           "data/chill_ClimateWizard",
                           "Bonn_observed")
```

We'll later want to plot all our data. In `chillR`, this is most conveniently done by producing climate scenarios with the `make_climate_scenario` function. The plotting function we'll be using later then simply processes a list of such climate scenarios. Let's start with a historic scenario that contains both the distributions for historic years and the historically observed chill.



``` r
chill_past_scenarios <- load_temperature_scenarios(
  "data/chill_ClimateWizard",
  "Bonn_historic")
chill_observed <- load_temperature_scenarios(
  "data/chill_ClimateWizard",
  "Bonn_observed")

chills <- make_climate_scenario(
  chill_past_scenarios,
  caption = "Historic",
  historic_data = chill_observed,
  time_series = TRUE)

plot_climate_scenarios(
  climate_scenario_list = chills,
  metric = "Chill_Portions",
  metric_label = "Chill (Chill Portions)")
```

<img src="bookdownproj_files/figure-html/load_and_plot_chill_scens-1.png" width="672" />

```
## [[1]]
## [1] "time series labels"
```

As you can see, this function had two effects. It produced a plot and it returned a short list containing the message "time series labels". This message isn't too interesting now, but it will later contain more content. If we want to just store this information rather than immediately displaying it in our output, we can assign the plotting command to a new object (as in `info <- plot_climate_scenarios(...`). The function will then just produce its **side effect**, which is the plot itself.

Now we run through the same process for all the future climate scenarios. For each one, we add the climate scenario to the `chills` object (`make_climate_scenario` has an argument `add_to`, where we can specify that):


``` r
for(RCP in RCPs)
  for(Time in Times)
    {
    Temps <- load_temperature_scenarios(
      "data/Weather_ClimateWizard",
      paste0("Bonn_",
             Time,
             "_",
             RCP))
    chill <- Temps %>% 
      tempResponse_daily_list(
        latitude = 50.866,
        Start_JDay = 305,
        End_JDay = 59,
        models = models,
        misstolerance = 10)
    save_temperature_scenarios(
      chill,
      "data/chill_ClimateWizard",
      paste0("Bonn_",
             Time,
             "_",
             RCP))
}
```

We now load this again, make climate scenario the same way we did for the historic data, and add them to our `chills` list so that we can easily plot them:


``` r
for(RCP in RCPs)
  for(Time in Times)
    {
    chill <- load_temperature_scenarios(
      "data/chill_ClimateWizard",
      paste0("Bonn_",
             Time,
             "_",
             RCP))
    if(RCP == "rcp45") RCPcaption <- "RCP4.5"
    if(RCP == "rcp85") RCPcaption <- "RCP8.5"
    if(Time == "2050") Time_caption <- "2050"
    if(Time == "2085") Time_caption <- "2085"
    chills <- chill %>% 
      make_climate_scenario(
        caption = c(RCPcaption,
                    Time_caption),
        add_to = chills)
}
```

Now we have everything we need to plot the results of our climate change analysis:


``` r
info_chill <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "Chill_Portions",
    metric_label = "Chill (Chill Portions)",
    texcex = 1.5)
```

<img src="bookdownproj_files/figure-html/plot_full_climate_scenario_analysis-1.png" width="672" />

``` r
info_heat <-
  plot_climate_scenarios(
    climate_scenario_list = chills,
    metric = "GDH",
    metric_label = "Heat (Growing Degree Hours)",
    texcex = 1.5)
```

<img src="bookdownproj_files/figure-html/plot_full_climate_scenario_analysis-2.png" width="672" />

``` r
info_frost <- 
  plot_climate_scenarios(  
    climate_scenario_list=chills,
    metric="Frost_H",
    metric_label="Frost hours",
    texcex=1.5)
```

<img src="bookdownproj_files/figure-html/plot_full_climate_scenario_analysis-3.png" width="672" />

Now we can see the trends in chill and heat accumulation, as well as in frost hours for Klein-Altendorf. As we saw earlier, the function didn't only return the plot, but also some supplementary information, which we stored in the the `info...` objects in the latest code chunk. If you inspect these objects, you'll see that they contain the names of the climate models for each of the subplots (in addition to the **time series labels** for the historic plot). Since we used the same models each time, all information is listed multiple times. Let's only look at this once, and only for one of the plots:
  

``` r
info_chill[[2]]
```

<table class="table table-striped" style="font-size: 10px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:right;"> code </th>
   <th style="text-align:left;"> Label </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:left;"> bcc-csm1-1 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:left;"> BNU-ESM </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:left;"> CanESM2 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 4 </td>
   <td style="text-align:left;"> CESM1-BGC </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:left;"> MIROC-ESM </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:left;"> CNRM-CM5 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 7 </td>
   <td style="text-align:left;"> ACCESS1-0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:left;"> CSIRO-Mk3-6-0 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 9 </td>
   <td style="text-align:left;"> GFDL-CM3 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:left;"> GFDL-ESM2G </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 11 </td>
   <td style="text-align:left;"> GFDL-ESM2M </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:left;"> inmcm4 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:left;"> IPSL-CM5A-LR </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:left;"> IPSL-CM5A-MR </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:left;"> CCSM4 </td>
  </tr>
</tbody>
</table>

These labels aren't provided directly in the plot, because they would take up quite a bit of space. Instead, each model is specified by a number, with the key to these number codes given in this table.

If you don't like the design of this figure, don't worry. We'll be making our own version soon (and there's also a more modern version in `chillR` now that we'll get to know later).


## `Exercises` on generating CMIP5 temperature scenarios {-#exercises_ClimateWizard}

Please document all results of the following assignments in your `learning logbook`.

1) Analyze the historic and future impact of climate change on three agroclimatic metrics of your choice, for the location you've chosen for your earlier analyses.

<!--chapter:end:17-cmip5.Rmd-->

# Plotting future scenarios

## Learning goals for this lesson

-   Learn how we can use the `ggplot2` package to make an appealing illustrations of the chill projection results

## Making attractive plots

The default function in `chillR` can generate plots for climate impact projections, but its design may not always meet user preferences. The current version of the `plot_climate_scenarios` function offers limited options for customizing the plot's appearance. This limitation is primarily due to the function being written before extensive use of `ggplot2`.

In this chapter, a similar figure will be recreated using `ggplot`, offering greater flexibility and customization. [Eduardo Fernandez](https://scholar.google.de/citations?hl=de&user=ibSma_AAAAAJ) has already developed a function for this, which is included in `chillR`. However, the process will be built up gradually here to demonstrate how complex plots can be constructed using `ggplot`. Eduardo’s code has been slightly modified for clarity, but the core ideas remain his.

First, all necessary packages will be installed and loaded. New packages introduced here are `ggpmisc` and `patchwork`.

Building on prior work, the outputs produced in the chapters ***Historic Temperature Scenarios*** and ***Making CMIP6 Scenarios*** will also need to be loaded.


``` r
library(kableExtra)
library(chillR)
library(tidyverse)
library(ggpmisc)
library(patchwork)

chill_hist_scenario_list <- load_temperature_scenarios("data",
                                                       "Bonn_hist_chill_305_59")
actual_chill <- read_tab("data/Bonn_observed_chill_305_59.csv")

chill_future_scenario_list <- load_temperature_scenarios("data/future_climate","Bonn_futurechill_305_59")

chills <- make_climate_scenario(
  chill_hist_scenario_list,
  caption = "Historic",
  historic_data = actual_chill,
  time_series = TRUE)

SSPs <- c("ssp126", "ssp245", "ssp370", "ssp585")
Times <- c(2050, 2085)

list_ssp <- 
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(2) %>%
  unlist()

list_gcm <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(3) %>%
  unlist()

list_time <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(4) %>%
  unlist()


for(SSP in SSPs)
  for(Time in Times)
    {
    
    # find all scenarios for the ssp and time
    chill <- chill_future_scenario_list[list_ssp == SSP & list_time == Time]
    names(chill) <- list_gcm[list_ssp == SSP & list_time == Time]
    if(SSP == "ssp126") SSPcaption <- "SSP1"
    if(SSP == "ssp245") SSPcaption <- "SSP2"
    if(SSP == "ssp370") SSPcaption <- "SSP3"
    if(SSP == "ssp585") SSPcaption <- "SSP5"    
    if(Time == "2050") Time_caption <- "2050"
    if(Time == "2085") Time_caption <- "2085"
    chills <- chill %>% 
      make_climate_scenario(
        caption = c(SSPcaption,
                    Time_caption),
        add_to = chills)
}
```

To work effectively with `ggplot`, data needs to be arranged in a single `data.frame` rather than the list format currently used for storing projection data. Each row of the `data.frame` should include details such as the GCM, SSP, and Year. The most straightforward way to achieve this is by iterating through the elements of the chill projection list, extracting the necessary information, and combining it into a new, long-format `data.frame`.


``` r
# We'll first process the past scenarios (element 1 of the chills list).
# Within the data element, we have a list of multiple data.frames for
# the various past scenarios.
# Using a 'for' loop, we cycle through all these data.frames.

for(nam in names(chills[[1]]$data))
  {
   # Extract the data frame.
   ch <- chills[[1]]$data[[nam]]
   # Add columns for the new information we have to add and fill them.
   ch[,"GCM"] <- "none"
   ch[,"SSP"] <- "none"
   ch[,"Year"] <- as.numeric(nam)
   
   # Now check if this is the first time we've gone through this loop.
   # If this is the first time, the ch data.frame becomes the output
   # object (past_simulated).
   # If it is not the first time ('else'), we add the current data.frame
   # to the 'past_simulated' object
  if(nam == names(chills[[1]]$data)[1])
    past_simulated <- ch else
      past_simulated <- rbind(past_simulated,
                              ch)
  }

# We add another column called 'Scenario' and label all rows as 'Historical' 
past_simulated["Scenario"] <- "Historical"

kable(head(past_simulated))  %>%
  kable_styling("striped", position = "left",font_size = 14)
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:left;"> Season </th>
   <th style="text-align:right;"> End_year </th>
   <th style="text-align:right;"> Season_days </th>
   <th style="text-align:right;"> Data_days </th>
   <th style="text-align:right;"> Perc_complete </th>
   <th style="text-align:right;"> Chill_Portions </th>
   <th style="text-align:right;"> GDH </th>
   <th style="text-align:right;"> Frost_H </th>
   <th style="text-align:left;"> GCM </th>
   <th style="text-align:left;"> SSP </th>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:left;"> Scenario </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2001/2002 </td>
   <td style="text-align:right;"> 2002 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 81.77681 </td>
   <td style="text-align:right;"> 3099.912 </td>
   <td style="text-align:right;"> 728 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2002/2003 </td>
   <td style="text-align:right;"> 2003 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 78.92166 </td>
   <td style="text-align:right;"> 2626.071 </td>
   <td style="text-align:right;"> 749 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2003/2004 </td>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 77.04512 </td>
   <td style="text-align:right;"> 1126.760 </td>
   <td style="text-align:right;"> 1035 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2004/2005 </td>
   <td style="text-align:right;"> 2005 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 81.69922 </td>
   <td style="text-align:right;"> 1754.188 </td>
   <td style="text-align:right;"> 734 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2005/2006 </td>
   <td style="text-align:right;"> 2006 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 85.73869 </td>
   <td style="text-align:right;"> 2712.910 </td>
   <td style="text-align:right;"> 549 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2006/2007 </td>
   <td style="text-align:right;"> 2007 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 80.83104 </td>
   <td style="text-align:right;"> 2254.430 </td>
   <td style="text-align:right;"> 727 </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:left;"> none </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:left;"> Historical </td>
  </tr>
</tbody>
</table>


``` r
# We'll want to add the historic observation too, so let's simplify the
# pointer to this information for easier use later

past_observed <- chills[[1]][["historic_data"]]
```


``` r
head(past_observed)
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:left;"> Season </th>
   <th style="text-align:right;"> End_year </th>
   <th style="text-align:right;"> Season_days </th>
   <th style="text-align:right;"> Data_days </th>
   <th style="text-align:right;"> Interpolated_days </th>
   <th style="text-align:right;"> Perc_complete </th>
   <th style="text-align:right;"> Chill_Portions </th>
   <th style="text-align:right;"> GDH </th>
   <th style="text-align:right;"> Frost_H </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 1973/1974 </td>
   <td style="text-align:right;"> 1974 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 85.34065 </td>
   <td style="text-align:right;"> 2166.376 </td>
   <td style="text-align:right;"> 498 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1975/1976 </td>
   <td style="text-align:right;"> 1976 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 81.50011 </td>
   <td style="text-align:right;"> 1831.580 </td>
   <td style="text-align:right;"> 711 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1976/1977 </td>
   <td style="text-align:right;"> 1977 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 83.37374 </td>
   <td style="text-align:right;"> 1892.026 </td>
   <td style="text-align:right;"> 741 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1977/1978 </td>
   <td style="text-align:right;"> 1978 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 78.15125 </td>
   <td style="text-align:right;"> 2653.059 </td>
   <td style="text-align:right;"> 830 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1978/1979 </td>
   <td style="text-align:right;"> 1979 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 67.29434 </td>
   <td style="text-align:right;"> 1428.630 </td>
   <td style="text-align:right;"> 1376 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 1979/1980 </td>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 82.00353 </td>
   <td style="text-align:right;"> 2356.143 </td>
   <td style="text-align:right;"> 702 </td>
  </tr>
</tbody>
</table>

The same process is now applied to the future data, transforming it into a long-format `data.frame` for further analysis and visualization.


``` r
# Extract future data
for(i in 2:length(chills))
  for(nam in names(chills[[i]]$data))
    {ch <- chills[[i]]$data[[nam]]
     ch[,"GCM"] <- nam
     ch[,"SSP"] <- chills[[i]]$caption[1]
     ch[,"Year"] <- chills[[i]]$caption[2]
     if(i == 2 & nam == names(chills[[i]]$data)[1])
       future_data <- ch else
         future_data <- rbind(future_data,ch)
  }
```


``` r
head(future_data)
```

<table class="table table-striped" style="font-size: 14px; color: black; ">
 <thead>
  <tr>
   <th style="text-align:left;"> Season </th>
   <th style="text-align:right;"> End_year </th>
   <th style="text-align:right;"> Season_days </th>
   <th style="text-align:right;"> Data_days </th>
   <th style="text-align:right;"> Perc_complete </th>
   <th style="text-align:right;"> Chill_Portions </th>
   <th style="text-align:right;"> GDH </th>
   <th style="text-align:right;"> Frost_H </th>
   <th style="text-align:left;"> GCM </th>
   <th style="text-align:left;"> SSP </th>
   <th style="text-align:left;"> Year </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2001/2002 </td>
   <td style="text-align:right;"> 2002 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 82.40300 </td>
   <td style="text-align:right;"> 6711.915 </td>
   <td style="text-align:right;"> 350 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2002/2003 </td>
   <td style="text-align:right;"> 2003 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 82.26671 </td>
   <td style="text-align:right;"> 5935.780 </td>
   <td style="text-align:right;"> 443 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2003/2004 </td>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 85.07761 </td>
   <td style="text-align:right;"> 3366.613 </td>
   <td style="text-align:right;"> 599 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2004/2005 </td>
   <td style="text-align:right;"> 2005 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 121 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 89.65584 </td>
   <td style="text-align:right;"> 4391.204 </td>
   <td style="text-align:right;"> 293 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2005/2006 </td>
   <td style="text-align:right;"> 2006 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 89.75666 </td>
   <td style="text-align:right;"> 5904.127 </td>
   <td style="text-align:right;"> 133 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2006/2007 </td>
   <td style="text-align:right;"> 2007 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 84.41638 </td>
   <td style="text-align:right;"> 4938.089 </td>
   <td style="text-align:right;"> 413 </td>
   <td style="text-align:left;"> CMCC-ESM2 </td>
   <td style="text-align:left;"> SSP1 </td>
   <td style="text-align:left;"> 2050 </td>
  </tr>
</tbody>
</table>

The data is now formatted for use with `ggplot` and includes three metrics: *Chill_Portions*, *GDH*, and *Frost_H*. While a function could be written to handle this process, the current approach focuses on making the code flexible enough to plot all three metrics without significant modifications. This is achieved by defining variables for the metric (`metric`) and its axis label (`axis_label`) to allow easy adjustments.

The complex plot to be created cannot be produced as a single `ggplot` plot. However, this is manageable since multiple plots can be combined into a compound figure using the `plot_layout` function from the `patchwork` package.

A challenge when combining plots with shared axes, such as a common y-axis, is that the axes may vary due to differing data ranges across plots. To address this, the `range` function is used to determine axis extents that are consistent and reasonable for all plots.


``` r
metric <- "GDH"
axis_label <- "Heat (in GDH)"

# get extreme values for the axis scale

rng <- range(past_observed[[metric]],
             past_simulated[[metric]],
             future_data[[metric]])  
rng
```

```
## [1]   747.5324 21090.1451
```

The first plot can now be created, focusing on the past scenarios. This serves as the starting point for visualizing the data:


``` r
past_plot <- ggplot() +
  geom_boxplot(data = past_simulated,
               aes_string("as.numeric(Year)",
                          metric,group="Year"),
               fill = "skyblue")
```


``` r
past_plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-312-1.png" width="672" />

The general layout of this `ggplot` command should now be familiar. However, a specific detail requires attention: in many `ggplot` commands, variable names can be written directly (e.g., `group = Year`) without quotation marks, which is uncommon in R. Normally, strings must be quoted; otherwise, R interprets them as variable names and raises an error if the variable is undefined.

The developers of `ggplot2`, led by [Hadley Wickham](https://scholar.google.de/citations?hl=en&user=YA43PbsAAAAJ), have removed this requirement, simplifying code in many cases. However, this convenience can cause issues when actual variable names are needed in **ggplot2** calls. To address this, the `aes_string` function can be used instead of `aes`, as demonstrated in the example.

Additionally, the y-axis must accommodate not only the data from this plot but also the data from all future scenarios. This is achieved using the `range` (`rng`) determined earlier. The axis labels will also be customized, with the y-axis label set using the previously defined `axis_label`.


``` r
past_plot <- past_plot +
  scale_y_continuous(
    limits = c(0, 
               round(rng[2] + rng[2]/10))) +
  labs(x = "Year", 
       y = axis_label)

past_plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-313-1.png" width="672" />

The plot for the past scenarios is now complete, but adjustments are needed to ensure consistent formatting with the future data. While the past scenarios involve only one plot, the future scenarios will include multiple plots, created using the `facet_wrap` function. This function automatically adds design elements to the plots.

To maintain a uniform layout across the entire figure, the single plot for the past scenarios will also be converted into a facet layout. Additionally, the black-and-white theme will be applied for consistency.


``` r
past_plot <- past_plot +
  facet_grid(~ Scenario) +
  theme_bw(base_size = 15) 
  
past_plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-314-1.png" width="672" />

The final adjustments involve modifying the facet title and x-axis text. The facet title's background will be removed, and its text will be set to bold for clarity. The x-axis text will be angled to ensure proper display of all year labels, even if the text size is adjusted.


``` r
past_plot <- past_plot +  
  theme(strip.background = element_blank(),
        strip.text = element_text(face = "bold"),
        axis.text.x = element_text(angle=45,
                                   hjust=1)) 

past_plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-315-1.png" width="672" />

The plot of past scenarios is now complete. Next, actual observations will be added to the plot. To distinguish them from the outliers in the box plots, the observations will be colored blue. This step is straightforward and will enhance the clarity of the visualization.


``` r
# add historic data
past_plot <- past_plot +
  geom_point(data = past_observed,
             aes_string("End_year",
                        metric),
             col = "blue")

past_plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-316-1.png" width="672" />

With the past scenarios complete, attention shifts to the future scenarios. These will be organized into two plots: one for the two scenarios in 2050 and another for 2085. These plots will later be displayed as two groups of two plots each.

To maintain an organized structure and allow for potential expansion with additional scenarios, the two plots will be stored in a list. While not strictly necessary for this case, this approach provides flexibility for future modifications.

Before constructing the plots within the list, one will be assembled first as an example, starting with the year 2050.


``` r
y <- 2050

future_2050 <- ggplot(data= future_data[which(future_data$Year==y),]) +
  geom_boxplot(aes_string("GCM", 
                          metric, 
                          fill = "GCM"))

future_2050
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-317-1.png" width="672" />

At this point, all SSPs are mixed together, and the y-axis is not easily readable. While the information is conveyed through the color scheme, the plot appears cluttered. To improve its appearance, padding will be added to the sides of the plots using the `expand` parameter, ensuring the plot doesn't look too crowded and enhancing its overall readability.


``` r
future_2050 <- future_2050 +
  facet_wrap(vars(SSP), nrow = 1) +
   scale_x_discrete(labels = NULL,
                    expand = expansion(add = 1)) 
```

In this case, the axis limits also need to be adjusted to ensure consistency between the future and past plots. Additionally, the scenario year will be added to the plots for clarity. This is accomplished using the `geom_text_npc` function from the `ggpmisc` package. This will help in placing the year label appropriately on the plot.


``` r
future_2050 <- future_2050 +
  scale_y_continuous(limits = c(0, 
                                round(round(1.1*rng[2])))) +
    geom_text_npc(aes(npcx = "center", 
                      npcy = "top",
                      label = Year),
                  size = 5)

future_2050
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-319-1.png" width="672" />

For the final adjustments, the black-and-white theme will be applied once again. To reduce clutter, all axis text and titles will be removed, as they don’t add significant value. The y-axis ticks will also be removed. The legend will be placed at the bottom, and the facet title will be formatted in the same way as in the past plot to maintain visual consistency.


``` r
future_2050 <- future_2050 +
  theme_bw(base_size = 15) +
  theme(axis.ticks.y = element_blank(),
        axis.text = element_blank(),
        axis.title = element_blank(),
        legend.position = "bottom",
        legend.margin = margin(0,
                               0,
                               0,
                               0,
                               "cm"),
        legend.background = element_rect(),
        strip.background = element_blank(),
        strip.text = element_text(face = "bold"),
        legend.box.spacing = unit(0, "cm"),
        plot.subtitle = element_text(hjust = 0.5,
                                     vjust = -1,
                                     size = 15 * 1.05,
                                     face = "bold")) 

future_2050
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-320-1.png" width="672" />

The legend is currently too large, but it can be adjusted later.

Next, the procedure will be implemented in a loop to create a list of two plots: one for 2050 and one for 2085. This approach will allow for consistent plotting while maintaining flexibility for future adjustments.


``` r
future_plot_list <- list()

time_points <- c(2050, 2085)

for(y in time_points)
{
  future_plot_list[[which(y == time_points)]] <-
    ggplot(data = future_data[which(future_data$Year==y),]) +
    geom_boxplot(aes_string("GCM",
                            metric,
                            fill="GCM")) +
    facet_wrap(vars(SSP), nrow = 1) +
    scale_x_discrete(labels = NULL,
                     expand = expansion(add = 1)) +
    scale_y_continuous(limits = c(0, 
                                  round(round(1.1*rng[2])))) +
    geom_text_npc(aes(npcx = "center",
                      npcy = "top", 
                      label = Year),
                  size = 5) +
    theme_bw(base_size = 15) +
    theme(axis.ticks.y = element_blank(),
          axis.text = element_blank(),
          axis.title = element_blank(),
          legend.position = "bottom",
          legend.margin = margin(0, 
                                 0, 
                                 0, 
                                 0, 
                                 "cm"),
          legend.background = element_rect(),
          strip.background = element_blank(),
          strip.text = element_text(face = "bold"),
          legend.box.spacing = unit(0, "cm"),
          plot.subtitle = element_text(
            hjust = 0.5,
            vjust = -1,
            size = 15 * 1.05,
            face = "bold")) 
}

future_plot_list
```

```
## [[1]]
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-321-1.png" width="672" />

```
## 
## [[2]]
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-321-2.png" width="672" />

Combining the plots is straightforward. The plots can be joined using the `+` sign, which allows for easy layering and combination into a single cohesive figure.


``` r
both_plots <- past_plot + future_plot_list

both_plots
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-322-1.png" width="672" />

The basic structure of the plots is in place, but a few adjustments are needed, particularly for the legend. The `plot_layout` function from the `patchwork` package is used for this purpose. It allows for the creation of patchwork figures by collecting all legends and removing duplicates, ensuring that only one version of the legend is displayed. Additionally, the width of the individual plots can be adjusted. To achieve this, a vector `c(1, 1.8, 1.8)` is used, specifying that each set of future plots should be 1.8 times the width of the past scenario plot. This provides a more balanced layout.


``` r
plot <- both_plots +
           plot_layout(guides = "collect",
                       widths = c(1,rep(2,length(future_plot_list))))
```

With the previous adjustments, the plot is no longer clearly visible, so the legend will be moved to the bottom for better visibility. Due to how the `patchwork` package works, the corresponding theme call must be added after an `&` symbol to ensure the legend is positioned correctly at the bottom. This adjustment ensures the plot remains clear and the layout is consistent.


``` r
plot <- plot & theme(legend.position = "bottom",
                     legend.text = element_text(size=8),
                     legend.title = element_text(size=10),
                     axis.title.x = element_blank())
```

## The results

The adjustments have resulted in clear and consistent `ggplot` figures displaying a heat analysis for Bonn. The figures are well-organized, with properly placed legends and axis labels, making them ready for presentation.


``` r
plot
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-325-1.png" width="672" />

The process is now complete. The same procedure can be applied to the other metrics. By simply changing the `metric` and `axis_label` variables and running the code again, the same steps can be followed for the other metrics. The full code will not be shown here, but the approach should work seamlessly for these adjustments.

<img src="bookdownproj_files/figure-html/unnamed-chunk-326-1.png" width="672" />

<img src="bookdownproj_files/figure-html/unnamed-chunk-327-1.png" width="672" />

To create a generally applicable function for the entire processing workflow, some additional effort is required. This involves ensuring that the function produces appropriate warnings or errors when given incorrect inputs, and making it flexible enough to handle different types of data. However, if the function is only intended for use with data structured in the same way as the current dataset, it can be simplified. In this case, all the steps performed so far can be wrapped into a function call, streamlining the process.


``` r
plot_scenarios_gg <- function(past_observed,
                              past_simulated,
                              future_data,
                              metric,
                              axis_label,
                              time_points)
{
  rng <- range(past_observed[[metric]],
               past_simulated[[metric]],
               future_data[[metric]])  
  past_plot <- ggplot() +
    geom_boxplot(data = past_simulated,
                 aes_string("as.numeric(Year)",
                            metric,
                            group="Year"),
                 fill="skyblue") +
    scale_y_continuous(limits = c(0, 
                                  round(round(1.1*rng[2])))) +
    labs(x = "Year", y = axis_label) +
    facet_grid(~ Scenario) +
    theme_bw(base_size = 15) +  
    theme(strip.background = element_blank(),
          strip.text = element_text(face = "bold"),
          axis.text.x = element_text(angle=45, 
                                     hjust=1)) +
    geom_point(data = past_observed,
               aes_string("End_year",
                          metric),
               col="blue")
  
  future_plot_list <- list()
  
  for(y in time_points)
  {
    future_plot_list[[which(y == time_points)]] <-
      ggplot(data = future_data[which(future_data$Year==y),]) +
      geom_boxplot(aes_string("GCM", 
                              metric, 
                              fill="GCM")) +
      facet_wrap(vars(SSP), nrow = 1) +
      scale_x_discrete(labels = NULL,
                       expand = expansion(add = 1)) +
      scale_y_continuous(limits = c(0, 
                                    round(round(1.1*rng[2])))) +
      geom_text_npc(aes(npcx = "center",
                        npcy = "top",
                        label = Year),
                    size = 5) +
      theme_bw(base_size = 15) +
      theme(axis.ticks.y = element_blank(),
            axis.text = element_blank(),
            axis.title = element_blank(),
            legend.position = "bottom",
            legend.margin = margin(0,
                                   0, 
                                   0, 
                                   0, 
                                   "cm"),
            legend.background = element_rect(),
            strip.background = element_blank(),
            strip.text = element_text(face = "bold"),
            legend.box.spacing = unit(0, "cm"),
            plot.subtitle = element_text(hjust = 0.5,
                                         vjust = -1,
                                         size = 15 * 1.05,
                                         face = "bold")) 
  }
  
  plot <- (past_plot +
             future_plot_list +
             plot_layout(guides = "collect",
                         widths = c(1,rep(2,length(future_plot_list))))
           ) & theme(legend.position = "bottom",
                     legend.text = element_text(size = 8),
                     legend.title = element_text(size = 10),
                     axis.title.x=element_blank())
  plot
  
}
```

By wrapping all the steps into a function, the same outputs can now be generated more quickly. This approach simplifies the process and allows for efficient reuse of the code without repeating all the individual commands.


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "GDH",
                  axis_label = "Heat (in Growing Degree Hours)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-329-1.png" width="672" />


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "Chill_Portions",
                  axis_label = "Chill (in Chill Portions)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-330-1.png" width="672" />


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "Frost_H",
                  axis_label = "Frost duration (in hours)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-331-1.png" width="672" />

## `Exercises` on plotting future projections

1.  Produce similar plots for the weather station you selected for earlier exercises.


``` r
chill_hist_scenario_list <- load_temperature_scenarios("Yakima",
                                                       "Yakima_hist_chill_305_59")
actual_chill <- read_tab("Yakima/Yakima_observed_chill_305_59.csv")

chill_future_scenario_list <- load_temperature_scenarios("Yakima/future_climate","Yakima_futurechill_305_59")

chills <- make_climate_scenario(
  chill_hist_scenario_list,
  caption = "Historic",
  historic_data = actual_chill,
  time_series = TRUE)

SSPs <- c("ssp126", "ssp245", "ssp370", "ssp585")
Times <- c(2050, 2085)

list_ssp <- 
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(2) %>%
  unlist()

list_gcm <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(3) %>%
  unlist()

list_time <-
  strsplit(names(chill_future_scenario_list), '\\.') %>%
  map(4) %>%
  unlist()


for(SSP in SSPs)
  for(Time in Times)
    {
    
    # find all scenarios for the ssp and time
    chill <- chill_future_scenario_list[list_ssp == SSP & list_time == Time]
    names(chill) <- list_gcm[list_ssp == SSP & list_time == Time]
    if(SSP == "ssp126") SSPcaption <- "SSP1"
    if(SSP == "ssp245") SSPcaption <- "SSP2"
    if(SSP == "ssp370") SSPcaption <- "SSP3"
    if(SSP == "ssp585") SSPcaption <- "SSP5"    
    if(Time == "2050") Time_caption <- "2050"
    if(Time == "2085") Time_caption <- "2085"
    chills <- chill %>% 
      make_climate_scenario(
        caption = c(SSPcaption,
                    Time_caption),
        add_to = chills)
}
```


``` r
for(nam in names(chills[[1]]$data))
  {
   # Extract the data frame.
   ch <- chills[[1]]$data[[nam]]
   # Add columns for the new information we have to add and fill them.
   ch[,"GCM"] <- "none"
   ch[,"SSP"] <- "none"
   ch[,"Year"] <- as.numeric(nam)
   
   # Now check if this is the first time we've gone through this loop.
   # If this is the first time, the ch data.frame becomes the output
   # object (past_simulated).
   # If it is not the first time ('else'), we add the current data.frame
   # to the 'past_simulated' object
  if(nam == names(chills[[1]]$data)[1])
    past_simulated <- ch else
      past_simulated <- rbind(past_simulated,
                              ch)
  }

# We add another column called 'Scenario' and label all rows as 'Historical' 
past_simulated["Scenario"] <- "Historical"
```


``` r
for(i in 2:length(chills))
  for(nam in names(chills[[i]]$data))
    {ch <- chills[[i]]$data[[nam]]
     ch[,"GCM"] <- nam
     ch[,"SSP"] <- chills[[i]]$caption[1]
     ch[,"Year"] <- chills[[i]]$caption[2]
     if(i == 2 & nam == names(chills[[i]]$data)[1])
       future_data <- ch else
         future_data <- rbind(future_data,ch)
  }
```


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "Frost_H",
                  axis_label = "Frost duration (in hours)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-335-1.png" width="672" />


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "Chill_Portions",
                  axis_label = "Chill (in Chill Portions)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-336-1.png" width="672" />


``` r
plot_scenarios_gg(past_observed = past_observed,
                  past_simulated = past_simulated,
                  future_data = future_data,
                  metric = "GDH",
                  axis_label = "Heat (in Growing Degree Hours)",
                  time_points = c(2050, 2085))
```

<img src="bookdownproj_files/figure-html/unnamed-chunk-337-1.png" width="672" />

<!--chapter:end:18-plotting.Rmd-->

