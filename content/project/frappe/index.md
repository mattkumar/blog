---
date: "2021-06-13T00:00:00Z"
external_link: ""
image:
  caption: An example gradient area chart
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View Demo
  url: https://rpubs.com/matt-kumar/781074
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/frappe
slides: example
summary: My first attempt at porting a JS plotting library to R! Frappe Charts for all!
tags:
- Shiny
- Rmarkdown
- Data Visualization
title: frappe Charts
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

[Frappe charts](https://frappe.io/charts) is a modern, open source SVG charting library written in javascript.

I had been reading John Coene's [Javascript for R](https://javascript-for-r.com/), an excellent exposition into building widgets for R, and was inspired to put my new-found knowledge to the test. I selected the Frappe charts library as my use case and wanted to see how far down the rabbit hole I could go.

I was successful in porting over some of the charts and put them (very crudely) into a few R functions for use in Shiny, Rmarkdown and the viewer in R Studio IDE. I probably won't flesh this package out further as it was for educational purposes.

Below you can find a sample of what it can currently create: 

<div>
<iframe
    src="https://rstudio-pubs-static.s3.amazonaws.com/781074_8197ded96dc34034b92dff8f87d28e8d.html"
    frameborder="0"
    style="overflow:hidden;height:1000;width:100%"
    height="1000"
    width="100%">
</iframe>
</div>

Nothing earth-shattering, but very satisfying in being able to do some of this myself rather than waiting for someone else to.