---
title: "LLM monitoring"
author: "Matthew Kumar"
date: "2025-01-02"
slug: llmlogging
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

# Forward

To kick off the new year, I wanted to share a development in an AI-enabled R Shiny application I’ve been working on. 🍾 ✨

If you’re curious about the application, you can check out the video and slides from the presentation at R/Pharma Gen AI Day last year:

- [video](https://www.youtube.com/watch?app=desktop&v=0XDVYdyuNGc&ab_channel=RinPharma) - [slides](https://github.com/mattkumar/blog/raw/main/content/event/rpharma/NarromaticAI.pdf) 

# Taking Stock: R and Gen AI

Unlike languages such as Python 🐍 or JS, R has received comparatively limited official support for SDKs and frameworks that enable the use of LLMs from platforms like OpenAI and LangChain. These tools have become essential for building feature-rich generative AI applications, but as an R user, I'm not expecting parity anytime soon.

Fortunately, the R community has stepped up, building innovative solutions to bridge the gap. Simply search CRAN for examples. Posit has also made strides with packages like [`httr2`](https://httr2.r-lib.org/), [`elmer`](https://ellmer.tidyverse.org/), and [`shinychat`](https://posit-dev.github.io/shinychat/), which streamline LLM integration for R users. Their parallel work in the Python 🐍 ecosystem has further improved the experience for Shiny Python developers too.

# LLM Logging

One challenge I tackled was building a logging system to monitor the utilization and costs 🤑 of my app, which relies on LLMs for text generation and figure interpretation. 

With a growing user base 👥, tracking this data is crucial for planning and forecasting future resources. Beyond cost management, this system provides insights into user behavior, helping me refine the app’s performance and user experience 🕵.

While tools like [LangSmith](https://www.langchain.com/langsmith) do these tasks natively, integration with R or Shiny isn’t straightforward — so I decided to roll my own solution.👷 🔨 👨‍🔧


# Building a Recipe

To begin, I needed persistent storage ⬆️ for logging. Since **our** Posit Connect lacks persistent storage, I opted for AWS S3 buckets due to their ease of setup.

Next, I determined what to log and how to capture it 🤔. My app uses custom JavaScript for API requests to internal LLM instances. This is something that I had the unpleasant task of figuring out how to do - namely - pulling out relevant pieces of information from responses and relaying it back to R 🔄. 

> Alright, it wasn't *that* bad, but I feel unnecessary. Remember the lack of R support? We went with a custom JS early in development because streaming was vital to our UX. At the time there was no other (easy) way to do it. 

Each time a user clicks a "submit to LLM" button on a shiny module, I log:

From the JS side:

- ✅ Cost (in dollars) 💲
- ✅ Token usage (completion, prompt, total) 🌔
- ✅ Latency (⌚️ start and completion time)

From the R side:

- ☑️ User ID 👤
- ☑️ A unique session ID (generated using `{uuid}`) 🐾🐾
- ☑️ Date 📅
- ☑️ Order ID (tracks order in which LLMs are called)
- ☑️ Module used 📗📘📙
- ☑️ LLM model name used

I simply collect this information into a data frame which begins to build the foundation of a session log 📝.

# Integration

Using the `{aws.s3}` 📦, I configured secure access to our S3 buckets. In the app’s global server, I initialized a reactive data frame to store log data of a users session. Each time a user interacted with an LLM in a module, that information was added to the log via `bind_rows()`.

To persist logs when sessions ended (often when users closed their browsers), I used `session$onSessionEnded` to **automatically** write the log to an S3 bucket as a CSV file 📤. A consistent naming convention ensured easier future retrieval 📥. 

The key functions here were `shiny::isolate`, `utils::write.csv`, and `aws.s3::put_object`.

Here's a diagram of it's final implementation:

![problem](https://github.com/mattkumar/shinysave/blob/main/map.png?raw=true)
# Retrieval 

After local testing, I deployed this solution to a test instance. To my surprise, it worked flawlessly 🤩.

Here’s an example of retrieving a log in R for inspection:

![problem](https://github.com/mattkumar/shinysave/blob/main/snapshot.jpg?raw=true)

I also wrote helper functions to pull logs (by date range or all at once), concatenate them, and prepare them for analysis.

# Next Steps

Further testing and optimization are needed, but the system is functional. My next goal is to build a Shiny dashboard for aggregating, slicing and visualizing metrics 📉 📊. This will provide data-driven insights and strengthen my case for additional funding if and when required.

# Takeaways

I didn't have access to something fancy and out of the box like `LangSmith`. However, I was able to still build the functionality I required using available tools which has the benefit of adding further customization, control and utility.

Till next time 🍻🙏 !




