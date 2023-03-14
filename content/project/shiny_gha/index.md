---
date: "2023-03-13T00:00:00Z"
external_link: ""
image:
  caption: A sample shiny app
  focal_point: Smart
links:
- icon: link
  icon_pack: fas
  name: View App
  url: https://matt-portfolio.shinyapps.io/shiny-gha/
- icon: r-project
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/shiny-gha
slides: example
summary: Github Actions for auto-deployment of shiny apps on shinyapps.io
tags:
- CICD
- Github Actions
- Shiny
title: GHA and Shiny
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

This was a fun 🤓 experiment to build the intuition of using Github Actions (GHA) to automate "things". In this case, I use GHA to auto-deploy a shiny app to my personal shinyapps.io account.

In a nutshell, it works like this:

-   Everytime a push is made to the master branch of this repo, a github action script is triggered 🏃🏃🏻🏃🏼 💨
-   The set of GHAs is specified using a `yaml` file, here `~/.github/workflows/deploy.yaml`
-   In the yaml file, you provide explicit instructions to build your app from the ground up. This includes everything from first installing R, R packages to deployment to shinyapps.io via the `{rsconnect}` package.🔀🔁
-   One the GHAs are finished, the app is made available at the destination. ✅

In order to test whether GHA was working, the sample app I created is a super-simple dashboard 📈📉📊 that takes a single reactive: the date and time of deployment ⏰. There are other, more informative ways to monitor their progress and I will be covering this and more in depth in my Quarto use-case write up 💬. Stay tuned!

For now, I want to make this available as it reflects a recent learning and a pattern I can see myself reusing in the future. Many thanks to the following people + resources 💪💪💪

-   [Kyle Cuilla](https://github.com/kcuilla/USgasprices)
-   [Siqi Zhang](https://github.com/iqis)
-   [Making Data Science Work for Clinical Reporting Coursera](https://ca.coursera.org/learn/making-data-science-work-for-clinical-reporting)

Till next time, 🍻!
