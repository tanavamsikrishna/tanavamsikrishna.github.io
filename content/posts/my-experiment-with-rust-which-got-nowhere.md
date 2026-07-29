---
draft: false
title: My Experiment with Rust
date: 2026-07-30T00:23:33+0530
description: How not to go about a software project
tags: [programming, software-product-development]
---

Inspired by this article: [I spent 18 months rebuilding my algorithmic trading platform in Rust. I’m filled with regret.](https://medium.com/codex/i-spent-18-months-rebuilding-my-algorithmic-trading-in-rust-im-filled-with-regret-d300dcc147e0), I want to come clean about my own misadventures with Rust.

## 2019 & Early 2020
Rust was making it into the developer news, memorably as the “most loved programming language". Stack Overflow developer survey has been putting it at the top of that category consistently since then. I started by trying to understand the top paradigms of the language. The compiler tells you what’s wrong! It makes total sense. Why would you ever want to let the program have 2 mutable references?? It perfectly tickled my “ideals” searching mentality. I was convinced anybody who was not adopting Rust right away was a subpar developer.

But at that time Rust still had got nowhere near the adoption it got today.

## Mid 2020
Like it was in vogue during that time, I quit my job, which is not ideal. One thing led to another and I wanted to create a SaaS Product, details of which are irrelevant to this article. To lay out the components there would be a backend (or maybe 2), a front-end, a browser plugin while leveraging Firebase.

I had no prior serious, or any, work experience with Rust. But I can go through a book in a couple of days if I had to. So that is what I did with the one they listed on their website.

"Of course, the backend had to be in Rust."
## End of 2020

There is another wrong decision which can be deduced from the content of the article up to this point. It was the Firebase + Rust combo. Firebase does not maintain a Rust SDK. But as there was an HTTP API, making HTTP calls directly was the plan. And Firebase’s API, like any large service’s API, is fine-tuned for each call. By that I mean, you are going to see multi-part file uploads and multi-file uploads which need specific binary code demarcations between each file. Handling User SSO authentication (“Signing with Google”) and validating JWT. Periodic backend access token refresh. Building the objects of Firebase DB’s related calls which had nuanced schema. And more. All of which I built by hand. But it was also at this point it became clear to me that the whole thing was a stupid mistake. The trigger was … *the incessant compiler errors* on each incremental addition of a feature. It was the cocktail of:
* can’t borrow a captured outer variable in a FnMut
* async on trait functions not allowed
* variable x doesn’t live long enough
* ...

"Do I even know the ABC of software development?"

Some parts of it were of my own making. I jumped straight into using `proc_macros`, `macro_rules`, excessive usage of lifetime constructs on variables.

"No to the “bulky" `String` and use `Cow<'a, str>` instead"

It was something wholly avoidable with lesser technical ambitions.

_On the topic of macros, are we supposed to remember a whole new weakly structured language called Rust macros? For example to use `serde` in the macros style?_

Building the frontend in Svelte, a language I haven’t used before, was a pleasure.
