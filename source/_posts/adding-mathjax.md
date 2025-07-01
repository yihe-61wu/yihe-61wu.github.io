---
title: Adding MathJax in Hexo.NexT
category: log
date: 2025-06-30 14:54:17
tags: 
mathjax: true
---

# Why

Although my research is mostly about or inspired from brains, I identify myself largely as a mathematician. LaTeX is a must-have, especially when I'm writing (blogging) something technical.

For example, below is something from my undergraduate (handwritten) notebook that becomes quite puzzling to me now:

$$\begin{align}
\forall R > 0, U \in D'(I; R), X(U) \in H(D'(I; R)) \\
\exists n \in \mathbb{Z}, X(U) = \sum_{n=-\infty}^{+\infty} C_n (U - I)^n \\
\forall m \in \mathbb{Z}, \exists n < m, C_n \neq 0
\end{align}$$

<!-- more -->

Rendering LaTeX wasn't possible within old blogging platforms I used, which was fine as I blogged mostly non-technical, personal thoughts in Chinese, but no longer fitted for this blog.

Besides, I've been aware of the feature of maths equetions in NexT for long. It should be as simple as Overleaf, isn't it?

# How

The official documentation for Math Equations in NexT can be found [here](https://theme-next.js.org/docs/third-party-services/math-equations).

I enabled `mathjax` as `katex` seemed more restrictive in terms of mathematical notations, but I did not enabled `math` for `every_page`.

Then, I uninstalled the original renderer `hexo-renderer-marked`, and installed `hexo-renderer-pandoc` by:

```
npm un hexo-renderer-marked
npm i hexo-renderer-pandoc
```

It turned out that I didn't have `pandoc` on my machine at all, so I installed it.

The maths part seems alright, but `pandoc` complaints a lot when rendering. I was stunned by so many warnings. Moreover, some formatting is indeed problematic (see <a href="#how-to-fix">**How to Fix**</a>).


# Failed Attempt

My first thought was that I might have installed `hexo-renderer-pandoc` incorrectly. After all, `npm` reported vulnerabilities and some of them were high and even critical. I ran `npm audit fix` and some vulnerability remained unresolved, requiring manual inspection.

With little knowledge of `npm`, I consulted `Gemini 2.5 Flash` and decided to address the only vulnerability with a high rating, which was related to `hexo-footnote`. The suggestions were mostly confusing to me, except one reminding me of possibilities that some dependencies could be outdated. As I only restarted updating this website but not yet updated hexo, I thought I should update things first.

I updated `Node.js`, which was the **only right thing** I did within this failed attempt.

Consequently, however, commands like `hexo clean` yielded `command note found` errors (but `npx hexo clean` worked), which was fixed by `npm install -g hexo-cli`.

I then updated hexo, or I thought I did. Luckily I used Git and found the 'new' hexo was actually outdated and the previous hexo version was quite up-to-date. I thus reverted hexo version. 

I double-checked that there were no more critical vulnerabilities with `npm audit` (ignoring the non-critical). Nevertheless, warnings in rendering remained.


<h1 id="how-to-fix">How to Fix</h1>

The rendering issues were rooted in `pandoc` being more versatile in dealing with different syntax and consequently being more strict about the syntax.

## Soft Line Break
Given
```
first line
second line
```
will be rendered by For example, `hexo-renderer-marked` as:

first line  
second line

However, `hexo-renderer-pandoc` yields:

first line
second line

To achieve soft line break with `pandoc`, two extra spaces need to be added after `first line  `.

## Bullet Point, Numbered List, and Block Quotation
With `hexo-renderer-pandoc`, extra blank lines were needed before and after such blocks. 

If such a block is to be nested in another, the space is between markers are important, e.g., `> 1.` works, but not `>1.`

An extra line is also necessary before any **(sub-)title**.

## Backslash
It is recommended to use `\`, because `/`  may be interpreted as an escape, which may mess up rendering. I used `/` in footnote and the rendering was clearly broken.


# Final Warnings

**I have not got rid of all warnings.** 

Gemini told me such warnings might be false positives from `pandoc`, but I don't have a solid answer or solution yet.

