---
title: Lessons I Learned from Reformatting LaTex Reference
category: log
date: 2025-07-07 13:58:45
tags:
  - LaTeX
  - citation
  - 论文
---

# Why

In the revision of my latest [paper](https://doi.org/10.1007/s42235-025-00695-8), I was asked by the editor to reformat the reference, so that the entries would look like:

> [1] de Croon, G. C., Dupeyroux, J. J. G., Fuller, S. B., & Marshall, J. A. (2022). Insect-inspired AI for autonomous robots. _Science robotics_, 7(67).

More specifically, while the citations needed to be numbered and ordered by their first apperance, following a more engineering style. The reference entries should resemble the APA style.

The journal, under Springer Nature, doesn't supply their own LaTeX templates, but only points authors to the generic ones supplied by Spring Nature.<!-- more -->
There are a few options, and after several attempts I settled on `sn-vancouver.bst`,
because the numbering feature is correct, and it seemed the modification to be done would be minimal.
Specifically, by default I'd get an entry (for the same citation as above) like this:

> [1] de Croon GC, Dupeyroux JJG, Fuller SB and Marshall JA. Insect-inspired AI for autonomous robots. _Science robotics_, 2022:7(67).

which almost matches the requirement, except that the year is placed after the article title.
Therefore, I dived into the sn-vancouver.bst file.

# How

While this was the first serious time I inspected a bst file, it wasn't too difficult to understand some (not all) of its syntax, especially with the help of ChatGPT.

- **First lesson: Do not play with bst files on Overleaf.**
The code is coloured wrongly (perhaps the same algorithm for tex files is used).

- **Second lesson: Make a copy of the entire project, and truncate it to minimal pieces for faster compiling.**
As the goal is only to modify the formatting style, real contents are not important.
What matters are all the packages for compatiblity check.
In particular, I'd advise to remove figures, as they can be quite large due to the requirement for publication.

- **Third lesson: AI is very helpful, in the start and the end; not so much in the middle, though.**
I started tackling the problem by feeding the bst file to ChatGPT, and asked it to locate the parts to be changed.
It did a great job. I soon confirmed that `format.journal.date` is the key variable I'd like to experiment with.

I made a copy of it and pasted the copy to the right place.
Brilliant! I had placed the year correctly!
There were only two remaining steps: 

1. removing the original `format.journal.date`, and 
2. adding parentheses to its copy now in the right place.

Step 1 took two seconds.
Step 2 took **two hours**.

- **Fouth lesson: Parentheses are not brackets.** 
The confusion was rooted in my poor understanding of these two terms. I used the word 'brackets' while 'parentheses' should be the correct one. 

- **Fifth lesson: AI is too agreeable.** 
Both ChatGPT and the Google's LLM model at that time (not Gemini) understood my inaccurate enquiry, and they even suggested the correct symbols. However, they didn't (or wasn't allowed to) lecture me explicitly on my mistakes, indulging my confusion. It took me hours, after consulting ChatGPT and checking multiple StackExchange discussions back and forth, for me to realise I had this basic misunderstanding. The mistake would perhaps embrassed me in front of a human expert, but it would probabily take no more than five minutes for them to correct me.

# Why not

After the paper was accepted by the reviewers and the editors, it went to the production team (of Springer Nature) and they made sure the formatting following the journal's requirements.

Honestly, the final production wasn't perfect, but I didn't need to spend at least three hours with the reference formatting.

Upon reflection, I learnt something new about LaTeX and that humans were not entirelly replaceable by AI.