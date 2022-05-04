---
date: "2019-09-12T00:00:00Z"
external_link: ""
image:
  caption: I should be on the log-scale
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View Demo
  url: https://visard.shinyapps.io/forestr
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/forestplot
slides: example
summary: An interactive tool to create publication-quality forest plots
tags:
- Shiny
- Data Visualization
- Statistical
title: forestR
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

In a previous role, creating forest plots were a routine task in almost any project that involved studying statistical associations between various exposures and outcomes using population-level data. These usually came in the form of logistic regression (odds ratios) or Cox models (hazard ratios) and needed to be visualized, often using a forest plot.

While that role (and organization) was very SAS-centric, no macro or PROC, to my knowledge, existed at the time that made this process painless. Often analysts would turn to Excel (cringe) and spend needless hours trying to ~~format~~ shoehorn their results into a template. 

To help overcome this, I created a forest plot in R and shared it with colleagues. As more and more wished to use it and adapt it, I realized this was a good candidate for a Shiny app. So, regardless of familiarity with R, all project members could craft a high-quality, publication ready forest plot for the journal article submission.

To help bridge the gap between SAS and R, I structured the input data set required by the shiny app around what PROC logistic or Lifetest would spit out via ODS (or something very near). This was also because at the time, most statistical analyses were *not* done in R. 

So, the app works like this.

1. I provide you a template with some light conventions to follow. These mimic most SAS PROCS ODS outputs.
2. Fill in the template and upload it to the app.
3. I provide you a good deal of aesthetic control (color, log-scaling, custom breaks, text, etc) to customize your plot.
4. Download your plot as a high-res PDF.
5. ???
6. Profit.

There's sample data in the app. You can edit it to your liking or just click **Proceed**. Give it a shot.