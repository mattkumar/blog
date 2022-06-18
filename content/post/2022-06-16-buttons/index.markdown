---
title: tweaking shiny actionButton
author: Matthew Kumar
date: '2022-06-16'
slug: shinybuttons
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

The default behavior in `shiny::actionButton()` is to open a web link in the *current* window. This approach has two potential implications for user-experience:

1.  The current progress within the shiny app will be lost; clicking 🔙 on your browser will reload the app 😭
2.  This can (independent of \#1) inadvertently divert users away from your app 🏃️💨

<center>
⬇️⬇️⬇️ See for yourself ⬇️⬇️⬇️
<br>
<br>
<button class="btn btn-default action-button btn-warning" id="btn0" onclick="alert(&quot;Just kidding! Youre not going anywhere!&quot;)" type="button">Click Me!</button>
</center>

<br> <br>

So what can we do?

✖️ Do nothing. Leave it as is and let all the hard work you put into the app be overshadowed by the site your are linking to.

✔️ Make the link open in a new tab or window.

✔️ Force the link to open in a new window.

The distinction between the two latter choices boils down to a users default browser settings. If you use Chrome like me, opening a link (designed to open in a tab or new window) defaults to opening it in a new tab. For you, it *might* open in a new window. Who knows? 🎱

If you really need the link to open in a separate window, luckily with a little elbow grease we can make that a sure thing.🎯 We just need to explicitly specify the window `height` and `width` in pixels. You can also pass `fullscreen=1` to make the new window, well, full screen.

> ⚠️⚠️⚠️ Opening links in a new window may result in getting dinged by an ad-blocker. This is because the so-called new window is more of a pop-up rather than it being a truly new window (i.e. `CTRL + N`).

Thank you [iqis](https://github.com/iqis) for pointing out that! 👽️

Whatever option you chose for your app, we have options. Below, I have three buttons and their corresponding code you might use in a shiny app. It’s pretty straight forward so I’ll end with saying keep user-experience front and center in your design! ✌🍻

``` r
# Default - current
shiny::actionButton('btn1',
                    'Current Window',
                    onclick ="location.href='http://google.com';")

# New tab or window  
shiny::actionButton('btn2',
                    'New Window or Tab', 
                    onclick ="window.open('http://google.com', '_blank')")

# New window
shiny::actionButton('btn3',
                    'New Window', 
                    onclick ="window.open('http://google.com', '_blank','width=800,height=800')")
```

<button class="btn btn-default action-button btn-danger" id="btn1" onclick="location.href=&#39;http://google.com&#39;;" type="button">Current Window</button>&nbsp;<button class="btn btn-default action-button btn-warning" id="btn2" onclick="window.open(&#39;http://google.com&#39;, &#39;_blank&#39;)" type="button">New Window or Tab</button>&nbsp;<button class="btn btn-default action-button btn-success" id="btn3" onclick="window.open(&#39;http://google.com&#39;, &#39;_blank&#39;,&#39;width=800,height=800&#39;)" type="button">New Window</button>
