---
title: Lessons I Learned from Fourier and Laplace Transforms
mathjax: true
category: log
date: 2020-09-01 22:22:22
tags:
  - mathematics
  - Laplace
  - Fourier
---

It was in the first half hour of my PhD viva, when one examiner asked me why I used the _Laplace transform_ instead of the _Fourier transform_, and the other examiner kept smilence[^1]. He surely knew that I cited his papers in which the two transforms are treated in the same way: the _Laplace_ dances with the theoretical deduction in the main text, while the _Fourier_ hides in the numerical calculation in the appendix.<!-- more -->

The _Laplace-Fourier_ relationship (not that of the two great mathematicians) remained unsettled in my heart even after I passed the viva, for I had spent several weeks digging into the literature, yet I only saw claims that the two transforms are related, on top of their apparently similar mathematical expressions. To summarise roughly, they both transform a function from the time domain into the frequency domain. In common practice, the _Laplace transform_ is unilateral, while the _Fourier transform_ is bilateral, meaning that the former acts only on the positive time line ($t>0$), but the latter on the entire time line. Conventionally they are applied in different areas, although they can be used in (almost) the same way to solve linear differential equations.

There are more subtle differences between the two transforms. One seemingly important difference lies in the frequencies: the _Fourier_ frequencies are treated mostly as real numbers, and the _Laplace_ frequencies are complex-valued. Such characteristics are reflected in the two inverse transforms. The _inverse Laplace transform_ is much more a pain, and is usually performed by looking up tables in theoretic deductions, or by the equivalent _inverse Fourier transform_ in numerical calculations (as in my thesis). However, to any mathematician, this difference is superficial as one can simply extend the real-valued _Fourier_ frequency to a complex number. So, why don’t we get rid of the two names? Or, why don’t we have a _Laplace-Fourier transform_? As a matter of fact, some people do use this combined term, but why don’t we popularise it?

I believed that mathematics was extremely pure and elegant, so there had to be a reason that people kept the two transforms distinct by mostly addressing them with different terms, instead of a combined one. I was naive, and very likely I was stupid. My concerns about the _Laplace-Fourier_ relationship was soundly cleared recently, thanks to this Dr. Steve Brunton’s YouTube lecture, [_The Laplace Transform: A Generalized Fourier Transform_](https://www.youtube.com/watch?v=7UvtU75NXTg&list=PLMrJAkhIeNNT_Xh3Oy0Y4LTj0Oxo8GqsC&index=38&t=0s). I strongly recommend to anyone who, like me, is ever puzzled by the relationship between the two transforms. In very simple pseudo-mathematical language,

> Laplace = Fourier ∘ Heaviside,

where _Heaviside_ is a transform of an arbitrary function which multiplies it by the _Heaviside step function_, and ∘ means composition of the two transforms.

Once getting the idea, everything seems intuitive and trivial. I can now easily navigate myself on the Wikipedia page of _Laplace transform_, and find a short piece of description on the _bilateral Laplace transform_, that does mention the multiplication by the _Heaviside step function_, which links to the main article _Two-sided Laplace transform_, that does claim explicitly its equivalence to the _Fourier_ transform. Although the younger me did notice their similarity and used them in a complementary way, I got lost; there were too many articles, books and other learning sources that I could access, but I missed a single Wikipedia page.

The lessons I learned were more than the technical details of the _Laplace-Fourier_ relationship, or even the intuitive idea behind. Perhaps, not like the naive me, you have had a crystal clear understanding of the two transforms. I say you are lucky, because either you are smarter, or you must have learned from a great lecturer or a great book. By ‘great’, I mean no longer purity and elegance in mathematics, but simplicity and easy-to-access. Yet for the true ‘easy-to-access’ mathematics I think there is a long long way ahead[^3].

[^1]: Smile and keep silence ([Urban Dictionary](https://www.urbandictionary.com/define.php?term=smilence)). This is a Chinglish word, somewhat old-fashioned.  
[^2]: I’m saying the last sentence in the particular tune of a neuroscientist.