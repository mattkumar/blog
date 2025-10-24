---
date: "2025-10-24T00:00:00Z"
external_link: ""
image:
  focal_point: Smart
links:
- icon: r-project
  icon_pack: fab
  name: View App
  url: https://mattkumar.github.io/sl-qr/
- icon: github
  icon_pack: fab
  name: View Repo
  url: https://github.com/mattkumar/sl-qr
slides: example
summary: Generating and using QR codes in R and Shiny Apps
tags:
- Data Visualization
- Statistical
- Simulation
- Animation
title: QR Codes
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

## Overview
<hr>
<br>

This application is a small example that highlights how to integrate the `{qrcode}` package 📦 into shiny. 

This might at first seem trivial — “just generating a QR code?” — but when paired with the right information, QR codes can actually become a powerful way to communicate data and metadata 📦

For example, imagine embedding metadata about how a figure was generated — the selected Shiny inputs, slider values, and filters applied. That’s instant context.
String interpolation is your friend here 🎯

Try it yourself 👇 by scanning the QR with your 📞

<div class="centered-wide-iframe">
  <iframe
    src="https://mattkumar.github.io/sl-qr/"
    style="border:none; width:100%; height:600px;">
  </iframe>
</div>

<style>
.centered-wide-iframe {
  /* Base width slightly wider than article content */
  width: 120%;              /* 20% wider than the text column */
  max-width: 1200px;        /* optional cap for huge monitors */
  margin-left: -10%;        /* shift left by half of the extra width */
  margin-right: -10%;       /* shift right symmetrically */
  position: relative;
  overflow: visible;
  z-index: 1;
}

.article-container,
.article-style {
  overflow: visible !important;
}
</style>


## 🧩 Data and Metadata Examples
<hr>
<br>

You can easily enrich your QR codes with:

🕒 System information: date, time, session ID

👤 User info: pulled automatically (e.g., session$user in Posit Connect)

📊 Data provenance: source files, query timestamps, or version numbers

When your app runs on Posit Connect, this becomes even more useful — you can automatically tag content with who generated it and when via the session object.

## 💡 Why It Matters
<hr>
<br>

On a more thematic level, QR codes offer a new layer of tractability in your analytics workflow.
If your app generates outputs — say, plots or reports — you can encode contextual details about the data source or analysis parameters directly into a QR code.

It’s like leaving a digital breadcrumb trail for reproducibility 🧵

## 🧱 Where to Use Them
<hr>
<br>

QR codes are super flexible — you can insert them into:

📈 Plots via {ggplot2} or {patchwork} (e.g. inset, or adjacent)

📄 Documents (PDF, DOCX, PPTX) using {officer}

🖥️ Directly inside your Shiny app’s UI

## 🔗 Resources
<hr>
<br>

If you find creative uses ️💡 for them, I'd love to know about it. Be sure to also check out the other features of the `{qrcode}` package:

- 🌐 [`Package Website`](https://thierryo.github.io/qrcode/)  
- 💻 [`Github Repository`](https://github.com/ThierryO/qrcode/)  

<br>
<br>
<br>
Till next time,
🍻🌴