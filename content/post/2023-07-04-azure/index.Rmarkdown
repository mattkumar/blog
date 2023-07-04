---
title: DevOps Bootcamp
author: Matthew Kumar
date: '2023-07-14'
slug: azure
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
<h4>Preface</h4>

I'll preface with this post is related to a project I lead at work. I can't share too many details about it here unfortunately (including code), but what I can safely share is my experience and process 💡.

<h4>tl;dr</h4>

I lead the development of a medium-size shiny application that is used by users within my organization. This app has evolved to the state where I need to move it from the current platform to a platform that is capable of scaling 📈 and has storage 📁. The issue? Well, data connectivity. The old way of accessing data via ssh is not tenable anymore, and so we must rely on the new platforms Azure-based systems. How can I re-factor my existing app to integrate with this? 🎯

<h4>First Steps</h4>

Until very recently, I had almost no experience with Azure or it's systems, or, it's lingo 💬. Our first steps were to attempt to read data in a local R session from a file container on Azure. I'll ⏭️ the details of this setup, mostly because I don't quite understand all that the Azure DevOps had to configure, but also my scope is restricted to R and shiny in this post.

I looked into the `AzureStor` package because by it's description alone, it's what I was going to need to do: Access files from Azure Storage. Straight forward right? Not exactly.

It turns out I needed to use the `AzureAuth` package first, whose sole focus is on establishing authentication with services on Azure. OK, so gameplan. Use `AzureAuth` to connect, get a token, then pass it to functions in `AzureStor` to do operations like download/upload/list. Once I could do this, I was confident my app would work in it's entirety.

This task in reality took quite a bit of time to map 🕵. Remember, I don't speak Azure. I also don't expect the DevOps engineers 👷 to be familiar with this R package and support it. Enter growing pains 😭 🏋️‍♀️ 👨‍🔧.

In the end we did get it mapped out, some parameters / settings more obvious than others, and I could finally read local Azure file containers on my local session ✅.

Here is the function I used:

`AzureAuth::get_azure_token(resource,   tenant,   app,   password = NULL,   username = NULL,   certificate = NULL,   auth_type = NULL,   aad_host = "https://login.microsoftonline.com/",   version = 1,   authorize_args = list(),   token_args = list(),   use_cache = NULL,   on_behalf_of = NULL,   auth_code = NULL,   device_creds = NULL )`

<h4>Shiny</h4>

Oh man, you would think just because you can produce something in a local R session, you can throw it into a shiny app and have it work right? right? Wrong. That was a learning here.

<img src = "https://i.imgflip.com/5c7lwq.png">

I'll mention too that on this new platform, we've chosen to use Posit Connect to host our shiny apps going forward. This product is definitely new to the DevOps team and while I have experience deploying apps to it, I don't have experience in configuring it.

Some weeks later, the connect server was setup, and I could deploy hello world apps to it from my local instance. I could actually deploy my full app, but it essentially didn't do anything since the data connectivity wasn't ironed out. I'll say this vignette was [super-helpful](https://cran.r-project.org/web/packages/AzureAuth/vignettes/shiny.html) in theory, but a lottttttttttttttttttttttttt of the pains were configurations specific to <strong>our internal systems</strong>

<h5>Hello App, with Azure</h5>

Our first task was to setup any kind of hello world shiny app that could read the files through the Azure file container. We eventually got this to work by using the <strong>app-password</strong> (defined in the link above). This was a reassuring sign of being on the right track ☀️. But what we really needed was to use the <strong>user</strong> 👥 credentials (since they will be tied to data access within the app). This was a lot more challenging, but an absolute necessity given what my app does.

<h5>Hello Matt, with Azure</h5>

I tried for the life of me to get the app to pull my credentials with no luck. Relying on the app-password was just a non-starter for this project. Enter `AzureGraph` 🌄

We had Microsoft Graph setup in our Azure system. In the end, after many hours of googling (GPT-4 was not helpful here) and experimenting, this is what I did:

-   request a token 🌕️ using Microsoft Graph service. This toke 🌕️n <strong>did</strong> contain my user credential🕵s
-   clone that token for use in another Microsoft Service, namely Azure Storage
-   pass that token when listing/reading/writing files in Azure using `AzureStor` within the shiny app ↪️
-   ❓️❓️❓️
-   Profit 🤑.

It worked.

Below is the culmination of many hours and weeks of learning about Azure, and it's integration into R and Shiny, with the added complexity of our companies systems/policies. 😝😝😝

![](azure.png)

See those credentials? Those are automatically obtained through configuring the 1) SSO 2) Azure Graph. User's don't really have to "login" any further 🔓. Even better, because the storage is setup and the ACL maintained, users only see what they are supposed to see. No more manual setups ☑️ ...at least from my end and from the perspective of Shiny.

Okay that's it. I just want to also say I've learned so much from working with the Azure folks 💪🏻; really I have 🙏. They were super patient with me, and really took the time to explain micro-concepts (much of which abbreviated here or skipped for brevity).

Till next time, 🍻🥂🥃
