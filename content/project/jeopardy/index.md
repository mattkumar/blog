---
date: "2022-09-28T00:00:00Z"
external_link: ""
image:
  caption: Jeopardy board (static)
  focal_point: Smart
links:
- icon: r-project
  icon_pack: fab
  name: View Interactive Table
  url: https://mattkumar.quarto.pub/jeopardy-game-contest
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/jeopardy-game-contest
slides: example
summary: Recreating a Jeopardy! game board using reactable and css in Quarto
tags:
- reactable
- quarto
- table
title: Jeopardy!
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
editor_options: 
  markdown: 
    wrap: 72
---

## Overview
This is my entry into the ⚡[R Studio 2022 Table Contest.](https://www.rstudio.com/blog/rstudio-table-contest-2022/)
It uses reactable and scss in Quarto to style a Jeopardy! game board. </br>

My aims for this project were three-fold:

1. To think about creative uses of tables! ✅

2. Learn how to use some of `reactable`'s custom rendering capabilities ✅

3. Continue to investigate and experiment (s)css and Quarto. ✅

## Approach
I start by pulling archived Jeopardy! game data using the `whatr` 📦. What's nice is that each row of data is indexed by the row and column it appears on in the actual board 😝. This makes it simple to ensure the <em>right content</em> is in the <em>right place.</em> ✅

In the next step, I borrow some preexisting css for creating [flip cards](https://www.w3schools.com/howto/howto_css_flip_card.asp) 🔍. I ♻️, 🔨  and 🗑 elements in order to match the aesthetic of Jeopardy! This was relatively straightforward, though researching colors and fonts took a bit of time.

The last step is to arrange the data once it's been read into R into a format serviceable for display. I knew I planned to use `reactable` as the display table package and leverage escaping html. 

### Method 1
My first approach was to bake the html/css stuff directly into each cell, before passing it to reactable for escaping. It looked something like this:  



```{code}
raw_data %>%
  .... %>%
  mutate(content = if_else(row == 1,
                             # html for header
                             glue::glue('<div class="flip-card">
                                          <div class="flip-card-inner">
                                            <div class="flip-card-head">
                                              <p>{category}</p>
                                            </div>
                                            <div class="flip-card-head">
                                              {category}
                                            </div>
                                          </div>
                                        </div>')
 .... %>%
 reactable(.,
           defaultColDef = colDef(html = TRUE))
```
                            
While this certainly worked (it has in the past for me), I knew reactable had more to offer in terms of custom rendering but have never delved into it.😨

### Method 2
It turns reactables `defaultColDef` argument works great for custom rendering in this case since every cell in my Jeopardy! board needs the same html/css treatment. It looks something like this:

```{code}
table_data %>%
  reactable(.,
    sortable = FALSE,
    defaultColDef = colDef(
      html = TRUE,
      align = "center",
      header = function(value) {
        tags$div(
          class = "flip-card flip-card-head",
          value
        )
      })
    )
```

I like this approach much better than the first because I'm keeping table and data wrangling parts of my workflow separate and hopefully more clear for readers. 🤓

## Forward
It's been an awesome ride so far experimenting with Quarto and continuing to learn how to create and modify existing CSS. I'm happy that the [R Studio 2022 Table Contest.](https://www.rstudio.com/blog/rstudio-table-contest-2022/) is taking place right around this time because it was a constructive outlet to build something that uses the new things I've recently learned.

🍻✌ Enjoy!


