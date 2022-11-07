---
date: "2022-11-07T00:00:00Z"
external_link: ""
image:
  caption: Time Machine (static, non-animated)
  focal_point: Smart
links:
- icon: r-project
  icon_pack: fab
  name: View Interactive Table
  url: https://mattkumar.quarto.pub/time-travel/
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/time-travel-contest
slides: example
summary: A Back To The Future time machine using reactable, countup and a lot of css
tags:
- reactable
- quarto
- table
title: Time Machine
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
editor_options: 
  markdown: 
    wrap: 72
---

## Overview
This is another entry into the ⚡[R Studio 2022 Table Contest.](https://mattkumar.quarto.pub/time-travel/)
It uses reactable, countup and css to recreate the time machine gizmo seen in the movie [Back To The Future](https://www.imdb.com/title/tt0088763/) </br>

My aims for this project were two-fold:

1. To think about creative uses of tables! ✅

2. Continue to experiment with reactable, css and Quarto. ✅

## Approach
My goal was to reenvision the following image as a table using R. 
![](https://images.squarespace-cdn.com/content/v1/545f5b33e4b0719cb5aee3a5/1606653495764-HE8UCUWTBZR2M4IWXOLA/Screen+Shot+2020-11-29+at+12.36.14.png)

I can divide my approach into 2 sections: general and styling

### General

When I first saw the above image, I thought it would make a great use-case for getting creative with tables. It was immediately apparent that the bulk of this work was going to boil down to styling. The general approach is quite simple:

1. Create a data frame with the required data

```{r}
data <- tibble::tribble(
  ~MONTH, ~DAY, ~YEAR, ~AMPM, ~HOUR, ~COLON, ~MIN,
   "OCT",   26,  1985,    NA,    10,     NA,   21,
   "OCT",   26,  1985,    NA,    10,     NA,   22,
   "OCT",   26,  1985,    NA,    10,     NA,   20
  )
```

The <strong>AMPM</strong> and <strong>COLON</strong> columns are left as placeholders which get rendered in `reactable`.

2. Execute <strong>3</strong> successive calls to a custom `reactable` function, one for each row of the table. E.g.

```{r}
data %>%
  filter(row_number() == 1) %>%
  my_reactable()
  
# etc
```
`my_reactable()` is a wrapper that is written by me and takes care of the formatting of a single table row including the cell, column and footer rendering along with css. A great use-case for a function! 🎯

### Styling
Much of my effort in this table was around styling. This involved quite a bit of work and playing around, and in the end I'm glad I saw it through to completion. 😥 ➡ 🤓

#### CSS
Yes, much of this table relies on custom css classes. It shouldn't be taken for granted the amount of work needed however, including research on the following to match aesthetics:

- custom fonts, font sizes, color schemes
- using new html elements (i.e. `<mark></mark>`)
- animations with css
- leveraging the `@extend` directive to make my css file shorter and more compact 💥💥💥

#### Countup
One neat package I was finally thrilled to have a use for was the [countup](https://github.com/JohnCoene/countup) by [John Coene](https://john-coene.com/). In short, his package lets you transform the appearance of a number as if a counter were running as an html element. This integrated quite nicely with `reactable` and serves to give the illusion that the time machine is calibrating! 😵

#### 3D
I also spent a bit of time learning some additional methods of css, namely `perspective`, `skew`, `scale` and `transform`. I decided to integrate this into this work as well as a separate table. 📦 This image was my inspiration:
![](https://www.rookscastle.com/tutorials/bttf-int-016-1.jpg)

### Forward
You can view these tables and all their interactive glory [here](https://mattkumar.quarto.pub/time-travel/)


🍻✌  Till next time!


