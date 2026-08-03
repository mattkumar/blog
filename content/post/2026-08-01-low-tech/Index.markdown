---
title: "Going Low Tech"
author: "Matthew Kumar"
date: "2026-08-02"
slug: googleleaderboard
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
editor_options:
  markdown:
    wrap: 72
---
# Going Low Tech 🚦

Last weekend we hosted a birthday party for my wife at our house 🎉. Along with friends and family, we set up three activity stations throughout the evening:

* 💃 Dance Dance Revolution (I have my own original machine)
* 🎤 Karaoke (in the main living room)
* 🏀 Basketball (on our backyard half court)

Naturally, we needed a way to crown an overall champion 🏆🥇.

My first instinct was the same as usual: build something in R using Shiny. Instead, I deliberately went in the opposite direction.

No R ✖️. No Shiny ✖️. No databases ✖️. No APIs ✖️.

Just Google Forms ✅, Google Sheets ✅, and a free QR code generator 🔳.

Sometimes the simplest tools are exactly the right ones 🧠✨.

![Dancing cat](https://media1.giphy.com/media/v1.Y2lkPTZjMDliOTUyNW9pa2M1anRqNjU4bmo4dmNqamhlcDFtbGt6eXRzZ2c0ZXpyY3Y4ZSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/d3mlE7uhX8KFgEmY/200.gif)

# Defining the Problem 🧩

The requirements were simple.

Each activity followed the same flow:

1. Complete the activity 🎯.
2. Record your score 📝.
3. Move on to the next station 🚶.

At the end of the night, the participant with the highest combined score would win a gift card 🏆🎁.

The biggest constraint was that there would be no dedicated scorekeeper. I didn't want someone stuck at a laptop 💻 entering results while everyone else enjoyed the party.

The scoring system needed to be completely self-service 🙌.

# Building the Forms 🛠️

I already had the guest list, so creating the forms was straightforward.

Each activity received its own Google Form with the same predefined list of participants. This avoided spelling mistakes ✏️ and ensured submissions could be matched correctly across activities.

At each station, I printed a QR code linking directly to the appropriate form. After completing an activity, participants simply scanned the code 📱, selected their name, entered their score, and submitted the form.

![qr](https://github.com/mattkumar/shinysave/blob/main/qr.jpg?raw=true)

# Bringing Everything Together 🔗

Each Google Form fed responses into its own worksheet within a shared Google Sheet 📊.

From there, I built a master scoreboard that combined all three activities, calculated total scores, and generated a live leaderboard 📈.

As scores were submitted, the **leaderboard updated in real time** and was displayed on a television throughout the evening for people to monitor 📺✨.

It ended up feeling far more polished than expected for something built almost entirely with spreadsheet formulas.... lol

![score](https://github.com/mattkumar/shinysave/blob/main/score.png?raw=true)


# An Unexpected Development Tool 🤖

The most interesting part of this project wasn't Google Sheets itself—it was how I built the system.

The concept, workflow, and overall design were mine 💡. The LLM helped me turn that idea into a working system by acting as a technical collaborator and a sanity check throughout the process 🤖.

While I still had to create the Google Forms, generate and print the QR codes, and set up the initial spreadsheet structure, the LLM helped operationalize the idea—guiding architecture decisions 🏗️, troubleshooting Google Sheets formulas ➗, debugging issues 🐛, and refining the leaderboard logic one step at a time.

The experience felt much closer to pair programming 👥 than simply asking an AI to generate code and copying the result. It was a fast feedback loop where I could propose an approach, test assumptions, and iterate quickly.

For a small project like this, that feedback loop was incredibly valuable ⚡. I went from an idea 💡 to a working prototype in about an hour.

# Takeaways 💭

As developers, it's easy to default to the technologies we're most comfortable with.

This could have become another Shiny application 📱, but it didn't need to.

Google Forms and Google Sheets were more than capable of solving the problem while keeping the experience simple for everyone involved. UX matters!

The result was a reliable, live scoring system 🏆 that ran the entire evening without requiring anyone to manage it.

Sometimes the best engineering decision isn't choosing the most powerful technology 🚀—it's choosing the simplest one that gets the job done ✅.

Until next time 🍻
