---
draft: false
title: "Build Websites From Scratch"
date: 2018-10-01T12:13:00+05:30
description: what are the tools I used to build my website
tags: [tech, build-website]
feed:
  limit: 10
---

### Inspiration

I am sure you think of the other practical applications of the knowledge you gained at work or at leisure.

- If you are a content writer at work, you might be inspired to write a book or articles or maintain a personal blog.
- If you are a chartered accountant, you might want to track your expenditure, analyse the data you collected and, well, make wiser spendings.
- And, if you have dealt with web technologies for software development, like me, you want to build and maintain a website.

Over the course of my software engineering experience I have come across everything I need to build a website. I might not have actually gone into gaining a detailed knowledge of configuring and extending of all of them, but I have experimented with so many of them, that find it naturally compelling to find some recreational ways of using them.

So what are the tools I used to build my website? **I hope this blog post inspires you to explore similar creative ideas using these tools.**

### Tools Used

- [Google Cloud Compute engine](https://cloud.google.com/compute/ "GC Compute Engine")
- [Docker](https://www.docker.com "Docker")
- [Grav CMS](https://getgrav.org "Grav CMS") - [Chalk Theme](https://github.com/paulmassen/grav-theme-chalk "Chalk theme")
- [Google Cloud Stackdriver Logging agent](https://cloud.google.com/logging/)

### DIY Manual (Outline; Details in the links above)

1. Buy a domain at domains.google.com
2. Create a docker image which runs the web server
   1. PHP > 5.5
   2. Git
   3. Install Grav-CMS. Useful grav plugins are:
      1. admin console plugin
      2. git-sync
   4. Install google-cloud's Stackdriver logging agent
3. Create a compute engine VM
4. Deploy the docker image on the created VM
5. Allocate a static IP address to the VM and add appropriate DNS entries
   1. Use Google Domain's DNS Records entry page, or...
   2. Set up a DNS Server at Google Cloud (which I did)
6. Add Content ! Write a blog post!

### Alternatives

This article outlines a hands-on process of creation of the website. There are other methods like maintaining a Wordpress blog and linking it with a custom domain. But then, unless you go premium you need to show a few google ads.
