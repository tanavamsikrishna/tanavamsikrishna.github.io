---
draft: false
title: "Programming Contest Analysis"
date: 2019-02-11T12:05:00+05:30
description: What is the programming language of choice ? Or what should be
tags: [programming, human-side-o-software-development, tech, programming-contest]
---

What is the programming language of choice ? Or what should be?

---

Codeforces.com is one of the many websites which organize online programming contests. And what's better is that they plan contests almost twice a week, and they support a good list of languages. Close to a 10,000 contestants take part regularly. I myself try/want to wrestle it out in as many of them as possible.

They have organized `Codeforces Round #548` recently in which I have taken part. But that was not where my curiosity ended. I wanted to know:

What the programming language of choice was of the contestants?
How well did they fare on the basis of their selection of programming choice?
What conclusions can I draw?
Codeforces provides API to get a list of submissions made with their details. I used it to fetch all the submissions made over the course of the 2 hours of the contest. Using this API I found out that a total of `32515` submissions were made for evaluation.

## Data analysis

### Firstly, a graph :

(All the graphs I show are high resolution and can be opened in a new tab or downloaded for a peek at the details)
![](../ok-not-ok.png)
This bar chart shows us the number of submissions for each languages and segregates them into statuses with a unique colour per status . In the legend, all categories except `OK` are of `Non-OK` types. All `Non-OK` types are stacked one over the other. Quite a few `WRONG_ANSWER` types in brown.

### One more graph:

![](../submissions.png)
This is a bar graph of submissions across all languages all statuses combined. So, `GNU C++14`, `GNU C++17`, `GNU C++11`, `Java 8`, `Python 3`, `GNU C11`, `MS C++ 2017`, `PyPy 3`, `MS C++` are the top 9 programming languages with the most submissions in that order. I haven't merged `GNU C++14`, `GNU C++17`, `GNU C++11` into a single language because there is an important conclusion that can be drawn from those 3 data points. While there are a total of 25 languages which had at least one submission, the rest of the 16 languages were not popular in this programming contest, and thus have lesser data backing them, and thus are not very useful for us to draw any conclusions.

### One final one:

![](../success-percentage.png)
This graph shows us the percentage of successes (blue) per programming language. That one guy who used `Ruby` is a rock star. Aaand `JavaScript` did not fare well. (But, let's not draw any conclusions on these languages because of insufficient data on them)

## Conclusions

Now the reason I have not merged `GNU C++14`, `GNU C++17`, `GNU C++11` into a single language is the follows. For programming contests of this type contestants avoid using higher level and version specific constructs. Like templates and custom classes. Their solutions must be very functional and similar using basic language features. That means programming effort in all those 3 languages was very similar. The close success rates (only `2%` margin) of these 3 versions of `GNU C++` imply our data is valid to draw conclusions from. I am still using only the top 9 most popular languages as a basis for our analysis.

The 9 most popular languages used have a success rate between `35%-40%` except `MS C++` & `GNU C11` which were around `30% & 25%` respectively. I would say a success rates in the range `35%-40%` means they are pretty close.

So, the anti-conclusion is that betting on a programming language for better programmer productivity doesn't provide results.

What else does our data show? That the contestants love to use C++ (which ever version) by a huge margin

## Caveats

This analysis is hugely directed towards programming contests with little design involved. Despite being the most popular language by a margin in this contest, C++ is likely less enjoyable to work with to develop a huge back-end server. Availability of frameworks decide our tech stack when developing a non-algorithmic product
