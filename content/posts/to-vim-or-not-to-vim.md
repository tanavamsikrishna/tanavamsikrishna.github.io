---
draft: false
title: "To Vim or not to Vim"
date: 2019-04-27T18:27:00+05:30
description: This is the obligatory post on Vim
tags: [programming, vim]
---

This is the obligatory post on **Vim**. Recently I have come to appreciate the ubiquity, resourcefulness and extensibility of vim. This is not a tutorial on vim. I won't tell you how to exit vim editor. But this article is dedicated to the text editor which has been a programmers' companion for a few decades now. Whichever UNIX or Linux system you're in, whether a local system or a remote one, you can safely assume and rely on the command vi/vim to be present.

![](../vim-screenshot.png)

I have spent more than a couple of weeks studying vim. How to use vim, how to extend it, what is its future and how is vim implemented. More time spent on the former points than the last one. But it must also be very interesting to know how it is implemented because vim tends to be very responsive even after adding multiple plug-ins including external language Servers.

### A random snippet on usage

Vim commands (by that I mean **shortcuts** in the article; in vim terminology keyboard shortcuts are called **vim mappings**) can be composed together to build more complex commands. This reminds me of Indian languages where you can combine multiple characters to form a single character. Like, `((((va) + (e)) => (vi)) & (-m)) => (vim)` You could've combined `(va) + (ae)` to get `(vae)` or `(va) + (i)` to get something like `(vy)`.

We have 52 characters of capital and small case English letters on the keyboard. For commands of length 3, What is 52^3?! Vim might not have those many key-sequences working as a command but there are other keys on the keyboard apart from the alphabets and the length of a key-sequence, interpreted as a single command, doesn't really have a limit. Some go up to a length of four and above. So you can pack a lot of functionality into a few character strokes. And working with those many commands is viable because most of these combinations are intuitive and you need not actually remember all those thousands of possible commands, just the basic functionality of the single character strokes. My personal favourites are `vab` or `vap`.

### Extensibility

The other advantage of vim is its configurability and extensibility. Vim scripts are written in a language called VimL. It is not object-oriented and people generally don't like it. But it has been custom built for vim scripting and thus provides a few advantages like buffer-local variables, window-local variables, tab-local variables etc. These things don't even make sense in the context of other general purpose programming languages. There is also support for events. Surprisingly VimL has only basic support for string manipulation. Especially for multiline text manipulation. (Or maybe there is support for that. New things about vim pop-up every day!) It made me realise that vim is a "text editor" and not a "text processor"

### Neovim

> Literally the future of vim

This is how Neovim used to be described as. Its website now says

> hyper-extensible Vim-based text editor

Nevertheless, Neovim which is a spin-off of vim seems promising. It has already got a share of 40% (no way to verify this) in the vim market. Main reasons, to start Neovim as a separate project, are actually project management related. Bran Moolenaar, the original creator of vim and a current active developer, replied _"Keep me alive"_ To the question _"How can the community ensure that the Vim project succeeds for the foreseeable future?"_ [^interview-link]. Probably I am missing some context around the answer given. But on the bright side Neovim (which I generally think of vim itself) seems to be doing alright. The project was resilient to one of its lead developers exiting the project.

Neovim already has made progress in improving the vim plugin ecosystem. Neovim has introduced remote plugins (a Neovim instance connects to an external program via one of the available connection types. Via sockets, rpc, stdio, fileio). Neovim has already provided language clients (libraries) in multiple languages: JavaScript, rust, python etc. for the purpose. An alternative to remote plugins is writing the plugin/script in Lua. Neovim comes with a built-in Lua v5.1 interpreter (Yep, Lua interpreter is embeddable). For the most part, there is no overhead of using Lua instead of VimL. `call MyVimLFunc()` in VimL gets translated to `lua MyLuaFunc()` in Lua. And Lua is often hailed as the fastest interpreted language.

Another reason for starting Neovim as a separate project was that the Vim code base was just ugly. I am not sure how Neovim is faring though. But, no complaints yet. I am optimistic about the future of Neovim. I am looking forward to a better UI support (like floating windows etc.) and inbuilt LSP support which are already planned for the upcoming releases.

[^interview-link]: https://www.binpress.com/vim-creator-bram-moolenaar-interview
