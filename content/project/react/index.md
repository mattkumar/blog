---
date: "2023-12-10T00:00:00Z"
external_link: ""
image:
  caption: A reproducible waterfall plot
  focal_point: Smart
links:
- icon: react
  icon_pack: fab
  name: View React App
  url: https://mattkumar.github.io/react-app/
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/react-app/
slides: example
summary: A simple react app that takes user-provided topics and creates a story using OpenAI's GPT 3.5
tags:
- react
title:  story creator
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
editor_options: 
  markdown: 
    wrap: 72
---

<h2>The App</h2>
This is a simple react app I wrote that has the following intention:  

- A user provides 4 topic areas they want a funny, short story written about
- A prompt is created in the background based on that input
- The prompt is sent to Open AI via an API to request a story
- The returned story is displayed to the user
- The app is styled to give an 'authors' feel via CSS

><em>It turns out my API usage hit it's limit, so I've slightly altered the code to just display a static message. The ChatGPT part was secondary to actually learning and applying react, which was the real purpose of this. See below! </em>

<h2>The Journey</h2>
I'll start by saying I 😍 shiny. It's my 🔝. But this year has shown me a few things, namely, it's 😢 to need a Connect server to share apps. I've also wanted to learn something a bit more broad strokes, and so I chose React.  
<br><br>
This app, while simple, was a bit of a pain to get up and running. Here are the things I needed to learn:
<br><br>
- <strong>🔨 fundamental react concepts and syntax 👨‍💻:</strong> I mostly followed Youtube 🎥 and surprisingly... the official 📝. I tried <strong>not</strong> to use GPT in generating any code as that would defeat the purpose 🎯
<br>
<br>
- <strong>◀️adapting ideas▶️:</strong> What I mean by this is pretty much everything UI and server-based in shiny. Integrating existing CSS, applying style to UI elements, translating my ideas couched Shiny's reactive framework to React. The UI stuff wasn't difficult since I use a lot of custom CSS and JS in my shiny apps 💅
<br>
<br>
- <strong>👷 development environment setup:</strong> I (begrudgingly) used VSCode to do the development. This involved setting up Node, using `npm` and getting familiar with testing and debugging in Chrome developer tools. `npm create-react-app` allowed me to hit the ground running 🏃💨
<br>
<br>
- <strong>CI/CD:</strong> kind of, I first setup a github repository in VSCode, which was a learning by itself 👨‍🏫. I then had to figure out how to actually `build` 🛠 a react app and deploy it somewhere! Here I setup a process to compile and push to gh-pages for hosting.
<br><br>
I realize a lot of these things I take for granted using R Studio and I see the value in knowing how to do it through other means ✅. I'll  most likely continue working on my react skills next year, so keep an eye out!

Till next time 🍻✌
