---
title: Homepage Reconfiguration
category: log
date: 2025-06-02 16:07:19
tags:
  - website-building
  - hexo
---
# Why
With the aim to upgrade my personal website, which I decide to call 'online shed' from now on, I have reconfigured the [homepage](/) to contain only a brief self introduction in English and Chinese.

For context, I have used the [hexo](https://hexo.io/) blog framework with the [NexT](https://theme-next.js.org/) theme for years and I still like it. However, by default, a homepage lists posts in reverse chronological order, while I'd like to organise my online shed based on projects[^1].

Two changes are needed to reconfigure the location of the homepage:
1. relocate posts to a different address, and
2. make a new homepage.

# How
## 1. Post Relocation
There are two steps to achieve 1.

Firstly, in `\_config.yml` and find the code blog as below:
```
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: blog
  per_page: 10
  order_by: -date
```
where the value `blog` after `path:` is newly added to relocate posts to `\blog\`. By default, there is no value for `path` (the homepage address is always `\`). 

Secondly, in `\_config.next.yml` and `\themes\next\_config.yml`, find the same code block as below:
```
# ---------------------------------------------------------------
# Menu Settings
# ---------------------------------------------------------------

# Usage: `Key: /link/ || icon`
# Key is the name of menu item. If the translation for this item is available, the translated text will be loaded, otherwise the Key name will be used. Key is case-sensitive.
# Value before `||` delimiter is the target link, value after `||` delimiter is the name of Font Awesome icon.
# External url should start with http:// or https://
menu:
  Home: / || fa fa-home  
  Blog: /blog/ || fa fa-book
  #about: /about/ || fa fa-user
```
where the line `Blog: /blog/ || fa fa-book` is newly added to create a tab on the main menu. There were some weird behaviours when the two blocks in the two files were inconsistent, but I haven't got time to explore or learn the logic behind.

## 2. New Homepage
To achieve 2, simply create `\source\index.md` under `\source\`.

This is rather straightforward given my brief self introduction, except the slightly non-trivial formatting for the Chinese part, vertical writing as in traditional Chinese—the characters are arranged from top to bottom in columns instead of rows, and the columns should flow from righ to left.

## 2-1. Vertical Writing
As markdown doesn't care about formatting and hexo doesn't support vertical columns natively[^2], the desired formatting is achieved by embedding the following html block inside `\source\index.md`:
```
<div style="display: flex; justify-content: flex-end;">
<div style="
  writing-mode: vertical-rl;
  text-orientation: upright;
  text-align: right;
">
  <h1>苏至清</h1>
  潇潇兮暮雨<br>
  浩浩兮无涯<br>
  洋洋兮流水<br>
  渺渺兮予怀<br>
</div>
</div>
```
I found `writing-mode: vertical-rl; text-orientation: upright;` rather self-explanatory, but `text-align: right;` a bit confusing, as `right` here actually means 'bottom'—`writing-mode` effectively rotates the orientation of writing, which is different from `text-orientation`, as well as the orientation of `text-align`. 

Finally, to align the text to the right of a webpage `div style="display: flex; justify-content: flex-end;"` is used.

# What's Next
As mentioned earlier, I'd like a project-based organisation of my online shed[^1], so reconfiguring the homepage—a minimal doorwary to the shed—is just the very first step. I'm planning to add tabs for multiple portfolios, each showcasing a direction of research, teaching, and hobbies of mine, composed of individual projects and posts. 

The homepage would perhaps use more tweaks for clearer navigation of the shed and hopefully more impressive digital presence of mine. However, I'm not going to over and prematurely optimise the design without adding actual posts.

As detailed in [this previous post](/2025/06/02/online-shed-prologue), one of my greatest motivations to renovate my shed is for the preservation of *'what I have learned and produced from the past'*. So, I'm going to add old posts published on (or unwillingly removed from) other platforms—I have been working on this transition for years, but I'm going to push myself on it from now on.

A final note I want to make here is about the use of AI. I asked ChatGPT to help me with the reconfiguration of this website, the homepage, and vertical writing, and it did point me to the right direction. However, it was easier for me to tweak details directly with trial and error, e.g., the html code for vertical writing, to get what I really desired—it felt harder for me to deliver all the nuances through prompt engineering and I want to pick up some html anyway. According to the Internet and some friends, generative AI is extremely good at front design, which I'd like to have a try—perhaps starting with my homepage.



[^1]: The reverse chronological order is presumably sensible if the blog focusses on only one topic or a few closely related topics—mine is different. My blog has to be (at least) bilingual and my articles multi-disciplinary. Even if I were to build separate blogs for myself, the most professional one—something potentially I would like to show (off) to my friends, colleagues, prospective employers, the public, and/or AI bots—had to contain my postdoc projects on different topics in computational neuroscience and bio-inspired AI, while I am also a teacher of mathematics and statistics. So, to make navigating my online shed convenient for human visitors, I believe the best way to organise it is to take a project-based approach.
[^2]: Apparently, Hexo was originally created by Tommy Chen, who blogs in traditional Chinese.



