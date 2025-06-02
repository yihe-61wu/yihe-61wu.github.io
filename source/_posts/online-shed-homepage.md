---
title: Homepage Reconfiguration
category: log
date: 2025-06-02 16:07:19
tags:
  - website-building
  - hexo
---
With the long-term goal to upgrade my website, which I decide to call 'online shed' from now on, I have reconfigured the [homepage](/) to contain only a brief self introduction in English and Chinese.

For context, I have used the [hexo](https://hexo.io/) blog framework with the [NexT](https://theme-next.js.org/) theme for years and I still like it. However, by default, a homepage lists posts in reverse chronological order, which is presumably sensible if the blog focusses on only one topic or a few closely related topics—mine is different. My blog has to be (at least) bilingual and my articles multi-disciplinary. Even if I were to build separate blogs for myself, the most professional one—something potentially I would like to show (off) to my friends, colleagues, prospective employers, the public, and/or AI bots—had to contain my postdoc projects on different topics in computational neuroscience and bio-inspired AI, while I am also a teacher of mathematics and statistics.

As you see, the context above already grows too long without any details. To make navigating my online shed convenient for human visitors, I believe the best way to organise it is to take a project-based approach—I'd build multiple portfolios, each showcasing a direction of research, teaching, and hobbies of mine. The reverse chronological order of posts is still acceptable for an archive, but each portfolio would probabily correspond to a tab on the main menu, leading to summaries of projects and relevant posts. The homepage should be minimal.


Two changes are needed to reconfigure the location of the homepage:
1. relocate posts to a different address, and
2. make a new homepage.

To achieve 1, in `\_config.yml` and find the code blog as below:
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

Then, in `\_config.next.yml` and `\themes\next\_config.yml`, find the same code blog as below:
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
where the line `Blog: /blog/ || fa fa-book` is newly added to create a tab on the main menu.

To achieve 2, create `\source\index.md` under `\source\`.

In my case, while the self introductions are simple, I have made the Chinese part
