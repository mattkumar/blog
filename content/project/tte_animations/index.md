---
date: "2021-07-21T00:00:00Z"
external_link: ""
image:
  caption: An animated KM curve
  focal_point: Smart
links:
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/tte_animations/
- icon: linkedin
  icon_pack: fab
  name: Linked In
  url: https://www.linkedin.com/posts/matthew-kumar-24910629_storytellingwithdata-rstats-datascience-activity-6823690592946667520-nSl5?utm_source=linkedin_share&utm_medium=member_desktop_web
slides: example
summary: An experiment in storytelling using animation for statistical analysis
tags:
- Data Visualization
- Statistical
- Pharma
- Animation
title: Animated KM
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

This was a neat experiment using the `{gganimate}` package for storytelling purposes. In the Kaplan-Meier plot, animation serves as the vehicle to unravel chronological events in a fictitious Oncology clinical trial. 

Some features include:
+ Animation of the individual survival curves over time - here you can see how fast the probability of survival drops quite clearly.

+ Tracking of number of events and number at risk in real time.

+ The use of stopping points to emphasize when the median survival time is achieved

+ The use of stopping points to emphasize contextual information such as planned analyses dates and results of interim stats. Note: may or may not make actual sense given the data.

![km](km.gif) 

I also had a bit of fun to see where else this could potentially play a role. In the below graph, we compare theoretical versus observed values from a simulation study to see where across the axes the biggest differences lie.

![sim](curve.gif)

This was experiment sparked further discussion into how we can help our Stat colleagues during their round-table discussions. It was eventually spun off into a shiny app.

Good times.
