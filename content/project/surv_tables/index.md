---
date: "2020-09-20T00:00:00Z"
external_link: ""
image:
  caption: An example drill down table
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View Demo
  url: https://visard.shinyapps.io/react_surv_tables/
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/react_surv_tables
- icon: r-project
  icon_pack: fab
  name: R-Studio Contest
  url: https://community.rstudio.com/t/interactive-survival-tables-table-contest-submission/81216
slides: example
summary: Interactive survival analysis tables using DT and reactable display table packages
tags:
- Shiny
- Data Visualization
- Contest
- Table
- JS
- Statistical
- Pharma
title: Survival Tables
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

The following project was an entry into the first R Studio table contest held in 2020.

It depicts a standard survival analysis using the Kaplan-Meier method. Accompanying the graph is an interactive Number at Risk (DT) table which can be clicked.

![NAR Table](t1.png)

Upon clicking a cell of the Number at Risk table, a second (Reactable) table is produced for those subjects. 

In this table, contextual information is given for these subjects and an inline, interactive swimmer plot (Highcharter) is also produced.

![Swimmer Table](t2.png)

Sadly this table did not place in the contest, though parts of it have made it's way into some of our team projects.

I learned a lot about JS and Reactable in this project, which has since become my display table package of choice within R :)
 