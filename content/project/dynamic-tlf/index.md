---
date: "2022-12-29T00:00:00Z"
external_link: ""
image:
  caption: A linked TLF
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View App
  url: https://matt-portfolio.shinyapps.io/dynamic-tlf/
- icon: r-project
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/dynamic-tlf
- icon: youtube
  icon_pack: fab
  name: View Video
  url: https://www.youtube.com/watch?v=kt_5AB3OmJw
slides: example
summary: Exploring dynamic and interactive TLFs using Tplyr and reactable via Quarto
tags:
- Data Visualization
- Statistical
- Table
- Quarto
- Shiny
- CDISC
title: Dynamic TLFs
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---
## Overview
This is another entry into the ⚡[R Studio 2022 Table Contest.](https://mattkumar.quarto.pub/time-travel/)
This app enables the exploration of subgroups on-the-fly through linked, interactive tables, listings and figures (TLFs) for clinical trial data. It leverages Tplyr, reactable and reactablefmtr for computing and is presented as a dashboard using Quarto. </br>

My aims for this project were two-fold:

1. Investigate whether we can dynamically create tables which can be used to guide an exploratory analysis.

The analysis starts with an anchor table, where individual cells can be clicked to retrieve the study participants ID's who comprise it. These are subsequently fed into additional tables, listings and figures through reactives.

In [previous work](https://matt-kumar.netlify.app/project/tplyr/), I've hard coded the anchor table by pre-specifying the variables to be displayed. With this work, you can now dynamically specify the anchor table to include any variables you like, which in turn can be used explore subgroups on-the-fly.

This work is largely enabled by utilizing the metadata building features of the [Tplyr](https://cran.r-project.org/web/packages/Tplyr/index.html) 📦.

2. Currently, no dashboard extension or package exists for Quarto. I used this opportunity to also see if I could (roughly) mimic what flexdashboard offers by using Quarto and custom css. My inspiration was the bootswatch lux theme. 👀

## Approach
The linked TLFs are also interactive and share the spirit of "drilling down" 🔃 

### Adverse Events Table 🕵
1. Uses reactable's groupBy to succinctly present a large table
2. Cells (in the second column) are hyper-linked to open a MedlinePlus search of that term. I found this resource was helpful in learning about medical conditions when analyzing clinical trials data.
3. A table-wide search functionality to pin-point certain SOCs/PTs of interest
4. A button to expand all SOCs at once to show the nested PTs

### Adverse Event Figure 📊
1. The highcharter column chart is a drill down plot. The first layer displays the top 4 System Organ Classes for a given subset
2. Clicking each of bars lets you drill down into a stacked column chart for the Preferred Terms x Severity
3. Customized tool tips to display information more clearly (i.e. severity of adverse event)

### Patient Listing 1 📝
1. Uses reactable's filter + search to navigate a potentially exhaustive table
2. Leverages reactable's columnGroups + formatting to organize the data layout
3. Capable of exporting a list subject identifiers as a CSV file to enable further analyses of interesting subgroups

### Patient Listing 2 📋
1. Uses reactablefmtr's inline visual to show vital signs measured at three times relative to baseline (i.e. percent change)
2. Leverages reactable's columnGroups + formatting to organize the data layout
3. Paired with shiny inputs to enable switching of Blood Pressure Parameters and Visits


## Future
This app can be extended in a number of different ways:

1. Including additional, linked TLFs; the sky's the limit! 🤩
2. Uploading data - the way I've began to structure the server will enable this in the future ⏫
3. More robust organization, control and validation for when the anchor table is updated 🛠

Till next time, 🍻!
