---
draft: false
title: Let's Encrypt
date: 2020-02-12T00:41:39+0530
description: An effort to make HTTPS the default
tags: [software, security]
---
In a era when paradigms of privacy and security are dictating the government rules and business ideas, serving web content over a secure connection is becoming important. Search engines rank your web content higher if your website is `HTTPS` enabled. There was a proposal to make all connections secure by default in `HTTP/2` protocol. Though it did not make it into the final draft, [Many implementations only support secure HTTP/2 and no major browser supports HTTP/2 over unencrypted channels] you can understand the importance given to having a secure connection.

It has also become cheap (free) to convert an `HTTP` website into an `HTTPS` website. [Let’s encrypt](https://www.letsencrypt.org) is one such effort in helping you get a `TLS` certificate for your website. And they recommend using [*certbot*](https://certbot.eff.org) to get an `HTTPS` certificate. Lets-Encrypt is a certificate authority. And Certbot is a software utility which helps you create a certificate and patch your web-server to use it. Instructions are pretty clear on the *certbot* website and how to run their command an application. You can choose between a host of combinations of web servers and operating systems.

For example, if you have an `Nginx` web-server which is running on `Debian 10`,  visit [this](https://certbot.eff.org/lets-encrypt/debianbuster-nginx "Certbot for Nginx and Debian 10") web-page and follow the 4 step instructions.
1. Make sure that you have `Certbot` and `python-certbot-nginx`
2. Run `certbot --nginx` as the root, which will obtain a certificate and also patch the Nginx configuration file
Or optionally just run `certbot certonly --nginx` to just obtain a certificate without patching the Nginx configuration file
3. Test automatic renewal with the `certbot renew --dry-run` command and verify if a cron job is added for the same
4. Visit your website (and verify). And never see an `Insecure Connection` warning again!
