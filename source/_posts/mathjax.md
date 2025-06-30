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

The maths part seems alright, but `pandoc` complaints a lot. I was stunned by so many warnings. Indeed, some formatting appeared odd.