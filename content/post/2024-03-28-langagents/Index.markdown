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

I'll assume from here on in you haven't been living under a
rock 🗿 for the past year and have heard and (hopefully) tried
ChatGPT yourself 👨‍💻

## The Problem

"A picture is worth a thousand words." In this case, *a picture of words is
worth saving me a thousand keystrokes:*

![problem](https://github.com/mattkumar/shinysave/blob/main/problem.png?raw=true)


One of the reasons ChatGPT can't give
responses based on real-time information because the underlying model
was trained with data up to a certain point in time. You're interacting with something fixed.

## Langchain

Enter Langchain. Specifically Langchain Agents.

![matrix-agents](https://qph.cf2.quoracdn.net/main-qimg-9935661f2ef938ba6a60d4e0c4447a09-lq)

I'm not going to go into an exposition on them ([read the docs 📗📘📙](https://python.langchain.com/docs/modules/agents/quick_start))
but I want to show how we can leverage them to do things for us.

At a high level, I'll create a "tool" 🔨 to do a task. I'll make this tool available to the LLM via Langchain to use (or not 🤔) based on my prompt 🗯

## My First Agent

Let's call him Smith 👤

Smith is a generic Python 🐍 function that will: 

- Access a public API that suggests activities to someone who is bored 📡
- Return a random response 🔙
- Parse the response to a string 👷



```python
# Define Smith
def Smith():
    res = requests.get('https://www.boredapi.com/api/activity?participants=1')
    return res.json()['activity'] + ' Key:' + res.json()['key']
```

Here's an example of a return:


```python
'Bake pastries for you and your neighbor Key:8125168'
```

We get a single recommendation, followed by a reference 🔑. I've included the 🔑 for so I can verify where the response came from 🎯: you can visit this [link](http://www.boredapi.com/api/activity?key=8125168) to verify yourself. 

Now, what if when you asked "ChatGPT" to suggest you an activity it used `Smith()` to get an answer? We need a way to make `Smith()` accessible to our LLM. That's precisely where Langchain comes in ⚡

## LLMs and Smith

In this section I'll show very briefly how to include `Smith()` inside of a Langchain agent call.


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

That's about it.  Lets try running it with the following prompt:


```python
agent.run("I am bored, suggest me a few activities. Provide me a key for each activity so I can reference it later.")
```



👇 👇 👇  Below is a log of the agent reasoning and final answer


```
> Entering new AgentExecutor chain...
I should think about a variety of activities that can help alleviate boredom.
Action: suggestions for boredom
Action Input: 
Observation: Do something nice for someone you care about Key:8321894
Thought:I should also consider activities that I enjoy doing alone.
Action: suggestions for boredom
Action Input: 
Observation: Start a daily journal Key:8779876
Thought:I should also consider physical activities to help pass the time.
Action: suggestions for boredom
Action Input: 
Observation: Study a foreign language Key:9765530
Thought:I now know the final answer
Final Answer: Do something nice for someone you care about (Key: 8321894), start a daily journal (Key: 8779876), and study a foreign language (Key: 9765530).

> Finished chain.
```

💣💥 Pretty neat, right? This log shows the reasoning of the agent through `Action`, `Observation`, `Thoughts` sequences until it arrives at a final answer. The point here is that it used `Smith()` to reply because it was determined the tool was the right fit 💯

## My Second Agent

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

Cool, so what? So, our goal is similar to above where now we want to expose `Johnson()` to our LLM and answer the original problem statement 🤩. But why stop there?

## Agent Mania

Let's see how we can utilize `Smith()` and `Johnson()` together 👥 to answer a more meaningful question :


```python
agent.run("Suggest me a few activities to do today, I am bored. If the activities are outdoors, comment on the weather. I am located in Toronto. Comment on whether the weather will be an issue for each activity.")
```


```
> Entering new AgentExecutor chain...
I should suggest some activities and check the weather for Toronto to see if they are feasible.
Action: get the current weather
Action Input: Toronto
Observation: -2°C Snow
Thought:I should suggest some indoor activities to avoid the cold weather.
Action: suggestions for boredom
Action Input: indoor activities
Observation: Repaint a room in your house Key:4877086
Thought:I should also suggest some outdoor activities that are feasible in the current weather.
Action: suggestions for boredom
Action Input: outdoor activities
Observation: Improve your touch typing Key:2526437
Thought:I now know the final answer

Final Answer: Some indoor activities you can do today are repainting a room in your house, and improving your touch typing skills. If you want to go outdoors, the current weather in Toronto is -2°C with snow, so it may not be ideal for outdoor activities.

> Finished chain.
```

🤯 😱 🤯 Just take a few seconds and re-read that response log and digest what's happening 😱 🤯 😱

🔥 Absolutely.  🔥 Positively.  🔥 Wild.

## Wrap Up

I hope this short demo of custom Langchain agents will be useful in your own work, the skies the limit 🚀

![power](https://github.com/mattkumar/shinysave/blob/main/smithflex.jpg?raw=true)

Langchain already has a set of predefined "tools" for agentic modeling you can use including weather  ([OpenWeather](https://python.langchain.com/docs/integrations/tools/openweathermap)) and internet search ([SerpAPI](https://python.langchain.com/docs/integrations/providers/serpapi)). 

The point here was to show how to do this yourself in case you have custom requirements in your work for which no off-the-shelf tool exists 💪💪🏻💪🏼

Till next time 🍻🙏 !
