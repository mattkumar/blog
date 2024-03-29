---
title: "custom langchain agents"
author: "Matthew Kumar"
date: "2024-03-28"
slug: purrr
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

AI, LLMs and ChatGPT have been all the 🌊 the last 12 months and I
haven't  written about it here... until now. Today I want to write
about an interesting problem that the [langchain](https://www.langchain.com/) can potentially solve. 

I'll assume from here on in you  have heard and (hopefully) tried
"ChatGPT" yourself 👨‍💻

## The Problem

"A picture is worth a thousand words." *In this case, a picture of words is
worth saving me a thousand keystrokes:*

![problem](https://github.com/mattkumar/shinysave/blob/main/problem.png?raw=true)


One of the reasons ChatGPT can't give responses based on real-time information because the underlying model
was trained with data up to a certain point in time.

## Langchain

Enter Langchain. Specifically Langchain Agents.

![matrix-agents](https://qph.cf2.quoracdn.net/main-qimg-9935661f2ef938ba6a60d4e0c4447a09-lq)

I'm not going to go into an exposition on them ([read the docs 📗📘📙](https://python.langchain.com/docs/modules/agents/quick_start))
but I want to show how we can leverage them to do things for us.

At a high level, I'll create a "tool" 🔨 to do a task. I'll make this tool available to the LLM via Langchain. When the agent is invoked, it will reason whether to use my tool (or not 🤔) based on my prompt 🗯

## My First Tool

Let's call him Smith 👤

Smith is a Python 🐍 function that will: 

- Access a public API that suggests activities to someone who is bored 📡
- Return a random response 🔙
- Parse the response to a string 👷



```python
def Smith():
    res = requests.get('https://www.boredapi.com/api/activity?participants=1')
    return res.json()['activity'] + ' Key:' + res.json()['key']
```

Here's an example of a return:


```python
'Bake pastries for you and your neighbor Key:8125168'
```

We get a single activity recommendation, followed by a reference 🔑  to verify the message came from the API. See here: [link](http://www.boredapi.com/api/activity?key=8125168)  

So our tool `Smith()` does what we want. The task at hand now is to make `Smith()` available to the LLM. And that's where Langchain comes in.

## LLMs and Smith

In this section I'll show very briefly how to include `Smith()` inside of a Langchain agent call:


```python
from langchain_openai import ChatOpenAI
from langchain.tools import BaseTool
from langchain.agents import initialize_agent
import requests

llm = ChatOpenAI()

class Smith(BaseTool):
    name = "suggestions for boredom"
    description = "useful for when you need to give suggestions for boredom."

    def _run(self, query: str) -> str:
        res = requests.get('https://www.boredapi.com/api/activity?participants=1')
        return res.json()['activity'] + ' Key:' + res.json()['key']

agent = initialize_agent(llm = llm, 
                         tools = [Smith()], 
                         agent = "zero-shot-react-description", 
                         verbose = True)
```

That's about it.  Lets try running it with the following prompt and view the output:



```python
agent.run("I am bored, suggest me a few activities. Provide me a key for each activity so I can reference it later.")
```


![output1](https://github.com/mattkumar/shinysave/blob/main/eg1.png?raw=true)

💥 Pretty neat, right? This output log shows the reasoning of the agent through `Action`, `Observation`, `Thoughts` steps until it arrives at a final answer. The point here is that it used `Smith()` to reply because it was determined the tool was the right fit 💯

## My Second Tool

Let's call him Johnson 👤

Johnson is also a Python 🐍 function. He's made with BeautifulSoup and his job is to scrape `google.ca` for the current weather for a location of my choosing.

Here he is:

```python
from bs4 import BeautifulSoup
import requests

def Johnson(query: str) -> str:
    url = f'https://google.ca/search?q=weather+{query}'
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36'}
    response = requests.get(url, headers=headers)
    soup = BeautifulSoup(response.text, 'html.parser')
    
    temp_elem = soup.find('span', id='wob_tm')
    unit_elem = soup.find('div', class_='vk_bk wob-unit')
    desc_elem = soup.find('div', class_='VQF4g')
    
    return print( temp + unit + ' ' + desc)
```

Let's see what he returns:


```python
Johnson(query = "Toronto");
```


```python
-2°C Snow
```

Cool, so learning what we did in the previous example, we can probably use `Johnson()` to get an answer to the question posed in the beginning of the article. 

But why stop there? 🤔

## Agent Mania

Let's see how we can utilize `Smith()` and `Johnson()` together 👥 to answer a more interesting question. Like before, we start with the prompt and view the output.


```python
agent.run("Suggest me a few activities to do today, I am bored. If the activities are outdoors, comment on the weather. I am located in Toronto. Comment on whether the weather will be an issue for each activity.")
```


![output-2](https://github.com/mattkumar/shinysave/blob/main/eg2.png?raw=true)


🤯 😱 🤯 Just take a few seconds and re-read that response log and appreciate what's happening here 😱 🤯 😱

🔥 Absolutely.  🔥 Positively.  🔥 Wild.

## Wrap Up

I hope this short demo of custom Langchain agents will be useful in your own work, the skies the limit 🚀

![power](https://github.com/mattkumar/shinysave/blob/main/smithflex.jpg?raw=true)

Langchain already has a set of predefined "tools" for agentic modeling you can use including weather  ([OpenWeather](https://python.langchain.com/docs/integrations/tools/openweathermap)) and internet search ([SerpAPI](https://python.langchain.com/docs/integrations/providers/serpapi)). 

The point here was to show how to do this yourself in case you have custom requirements for which no off-the-shelf tool exists 💪💪🏻💪🏼

Till next time 🍻🙏 !
