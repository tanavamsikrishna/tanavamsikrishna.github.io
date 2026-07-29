---
draft: true
title: My Experiment with Rust
date: 2026-07-30T00:23:33+0530
description: How not to go about a Software project
tags: [programming, software-product-development]
---

Inspired by this article: [I spent 18 months rebuilding my algorithmic trading platform in Rust. I’m filled with regret.](https://medium.com/codex/i-spent-18-months-rebuilding-my-algorithmic-trading-in-rust-im-filled-with-regret-d300dcc147e0), I want to come out clean about my own misadventures with Rust.

I will just go chronologically in this article.

## 2019 & Early 2020
Rust was making it into the developer news, memorably as the “most loved programming language". Stackoverflow developer survey has been putting it at the top of that category consistently since then. I started by trying to understand the top paradigms of the language. Compiler tells you what’s wrong! It makes total sense. Why would you ever want to let the program have 2 mutable references?? It perfectly tickled my “ideals” searching mentality. I was convinced anybody who was not adopting Rust right away is a subpar developer.

But at that time Rust still has got nowhere near the adoption it got today.

## Mid 2020
Like it was in vogue during that time, I quit my job, which is not ideal. One thing led to another and I wanted to create a SaaS Product, detailed of which are irrelevant to this article. To layout the components there would be a backend (or may be 2), a front-end, a browser plugin while leveraging Firebase.

> Of course, the backend had to be in Rust.

I had no prior serious, or any, work experience with Rust. But I can go through a book in a couple of days if I had to. So that is what I did with the one they listed on their website.

## End of 2020

There is another wrong decision which can be deduced from the content of the article upto this point. It was the Firebase + Rust combo. Firebase does not maintain a Rust SDK. But as there was an HTTP API, making HTTP calls directly was the plan. And Firebase’s API, like any large service’s API, is fine-tuned for each call. By that I mean, you are going to see multi-part file uploads which need binary demarkations between each part. Handling User SSO authentication (“Signing with Google”) and validating JWT. Backend access token refresh. Building the object of firebase DB’s document which has nuanced schema. And more. All of which I built by hand. It was at this point it become clear to me that the whole thing was a stupid mistake. The trigger was … *the incessant compiler errors*. It was the cocktail of:
* can’t borrow a captured outer variable in a FnMut
* async on trait functions not allowed
* variable x doesn’t live long enough
* ...

> Do I even know the ABC of software development?

Some parts was of my own making. I jumped straight into using `proc_macros`, `macro_rules`, excessive lifetime specification.
