---
title: old code and beginnings
author: ''
date: '2022-07-04'
slug: r-code
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2022-07-04T21:47:04-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


... and by old, I mean really old. Like year 2008 old. Like the first R code I ever wrote. 


I recently went digging in an old dropbox account for photos and to my surprise I had saved a copy of my undergraduate thesis, complete with code.

My undergraduate degree was in Psychology and I had a keen interest in psychometrics. My thesis involved an application of [item response theory](https://en.wikipedia.org/wiki/Item_response_theory) to ordinal data.

>*if you are interested, I used [Samejima's Graded Response Model](https://link.springer.com/chapter/10.1007/978-1-4757-2691-6_5) to analyze responses made to the [Barratt Impulsiveness Scale](https://en.wikipedia.org/wiki/Barratt_Impulsiveness_Scale) from a sample of first year university students*

At the time, my only experience with statistical software was with [SPSS](https://en.wikipedia.org/wiki/SPSS). I remember teaching myself how to use it only a year prior in order to double check my intro stats homework assignments 🤓🔬📏. I think that was a good move in retrospect because I was also able to spin that experience into a **paid** Stats Advisory position at the Psychology Resource Center. 

I digress.

The type of model I needed to fit for my thesis was only available through proprietary software. My [thesis advisor](https://health.yorku.ca/health-profiles/index.php?mid=498680) recommended I look into R as he had caught wind of a package that could help. The upside was that it would be 🆓 and open source 🤑. The downside was that I was going to have to learn "syntax" 🤢. I was aware that SPSS had syntax facilities for advanced users, but it was always intimidating 😣. 

But now I **had** to learn "syntax". *I'm laughing while typing this believe you me.* 🤣 Anyway, I don't quite recall the learning process, but I reckon it was difficult and in the end I was probably just relieved to get the job done. ✅🎓.I ended up having to write "syntax" for other supporting analyses in my thesis, namely Confirmatory Factor Analysis for assumption checking in [LISREL](https://ssicentral.com/index.php/products/lisrel/). *shudders*

For historical (and sentimental reasons) I've included the R code in my thesis below. It marked the first steps on the path I'm on today. 

From what I can tell I was using R 2.8.1 and I'm happy to see the original 📦, [**ltm**](https://cran.r-project.org/web/packages/ltm/) is still active on CRAN today.

Till next time, 🍻✌


```r
install.packages("ltm", dependencies = TRUE)
#downloads and installs the 'LTM' packageto the user’s hard drive.

library(ltm)
#loads the 'LTM' package from the user’s hard drive

attention = read.table(file.choose(),header=T)
#prompts for location of data set

grm0 = grm(attention, constrained = TRUE, Hessian = TRUE)
#fits the constrained GRM to the specified data set. The HESSIAN = TRUE argument computes standard error values.

summary(grm0)
#returns the parameter estimates

grm1 = grm(attention, constrained = FALSE, Hessian = TRUE)
#fits the unconstrained GRM and computes standard error values

summary(grm1)
#returns the parameter estimates

anova(grm0,grm1)
#performs a likelihood ratio test on the two models.

plot(grm1, type = "IIC", lwd = 2, cex = 1.2, legend = TRUE, cx = "topleft",xlab = "Latent
Trait", cex.main = 1.5, cex.lab = 1.3, cex.axis = 1.1)
#plots the IIFs

plot(grm1, type = "IIC", items = 0, lwd = 2, xlab = "Attention",
     cex.main = 1.5, cex.lab = 1.3, cex.axis = 1.1)
#plots the TIF

plot(grm1, lwd = 2, cex = 1.2, legend = TRUE, cx = "left",
     xlab = "Attention", cex.main = 1.5, cex.lab = 1.3, cex.ax
     is = 1.1)
#plots the CRCs

plot(grm1, type = "OCCu", lwd = 2, cex = 1.2, legend = TRUE, cx = "topleft",
     xlab = "Attention", cex.main = 1.5, cex.lab = 1.3, cex.axis = 1.1)
#plots the OCCs
```
