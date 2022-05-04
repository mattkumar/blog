---
date: "2021-07-02T00:00:00Z"
external_link: ""
image:
  caption: An example of the editor
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View Demo
  url: https://matt-kumar.shinyapps.io/demo
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/shinyTrumbowyg
slides: example
summary: A 'WYSIWYG' text editor widget for Shiny and Rmarkdown
tags:
- Shiny
- Rmarkdown
title: shinyTrumbowyg
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

[Trumboywg.js](https://alex-d.github.io/Trumbowyg/) is a lightweight, what-you-see-is-what-you-get, text editor written in jQuery. 

I really wanted to use this library in my shiny apps (some work related, some personal), but I couldn't locate any prior efforts in an R port. Therefore, I used this opportunity to learn to do it myself using the `{htmlwidgets}` package.


I was able to successfully port over the base version of Trumbowyg and it can be called quite easily using the familiar shiny widget: 

`trumbowygInput(id = "id",
                label = "text",
                value = "Hello world!")`
                   
At the same time, many plugins are available for Trumbowyg, such as emoji's, text coloring, highlighting, and more. I was able to also learn enough to use them natively and to have them be a part of the package.

This was a great learning experience to see how javascript integrates with R and Shiny *under the hood*. It's helped me develop a deeper appreciation for the work that goes into creating shiny extensions that I think we all (certainly I!) sometimes take for granted!

A quick shoutout to [John Coene](https://john-coene.com/) and [Maya Gans](https://maya.rbind.io/) for their various works in describing how to bridge the gap between javascript and R!

You may view a demo of this [here](https://matt-kumar.shinyapps.io/demo)