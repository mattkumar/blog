---
date: "2020-11-04T00:00:00Z"
external_link: ""
image:
  caption: An example drill down table
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View Demo
  url: https://visard.shinyapps.io/react_calendar/
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/react_calendar
- icon: r-project
  icon_pack: fab
  name: R-Studio Contest
  url: https://community.rstudio.com/t/a-reactable-based-calendar-table-contest-submission/86582
slides: example
summary: An reactable-based calendar and a whole lot of javascript and CSS
tags:
- Shiny
- Data Visualization
- Contest
- Table
- JS
- CSS
title: React Calendar
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

The following project was a second entry into the first R Studio table contest held in 2020.

I don't even know where to start with this one. I was looking at creative uses of a table and I landed on the idea of using a table as a calendar. 

At the same time, I was really into figuring out how to incorporate custom CSS into shiny. I had found this awesome 8-bit inspired CSS library and immediately wanted to use it. You can view it [here.](https://nostalgic-css.github.io/NES.css/)

Building on my previous experience of the `reactable` package (and custom JS), I kind of went HAM on this one:

- In addition to the custom bezel, added animated gifs from the super mario games

- Added (borrwed) JS code to give the particle effect of snow falling (it was December afterall!)

- Using JS, set custom modals on certain dates to mimic the feel of a calendar invite in Outlook. These are also stylized to match the overall aesthetic.

![NAR Table](screencap.gif)


