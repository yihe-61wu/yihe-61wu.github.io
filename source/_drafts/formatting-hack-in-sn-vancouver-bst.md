---
title: First lessons I learned from reformatting reference entries in sn-vancouver.bst
tags:
---

I've been revising a paper according to one editorial advice to make an article entry in the reference list to look like:

[1] de Croon, G. C., Dupeyroux, J. J. G., Fuller, S. B., & Marshall, J. A. (2022). Insect-inspired AI for autonomous robots. _Science robotics_, 7(67).

More generally, while the citations need to be numbered and ordered by their first apperance, following a more engineering style,
The reference entries should resemble the APA style.

The journal, under Springer Nature, doesn't supply their own LaTeX templates,
and points authors to the generic ones supplied by Spring Nature.
There are a few options, and after several attempts I settled on sn-vancouver.bst,
because the numbering feature is correct, and it seemed the modification to be done would be minimal.
Specifically, by default I'd get an entry (for the same citation as above) like this:

[1] de Croon GC, Dupeyroux JJG, Fuller SB and Marshall JA. Insect-inspired AI for autonomous robots. _Science robotics_, 2022:7(67).

which almost matches the requirement, except that the year is placed after the article title.
Therefore, I dived into the sn-vancouver.bst file.

**First lesson: Do not play with bst files on Overleaf.**
The code is coloured wrongly (perhaps the same algorithm for tex files is used).

**Second lesson: Make a copy of the entire project, and truncate it to minimal pieces for faster compiling.**
As the goal is only to modify the formatting style, real contents are not import.
What matters are all the packages for compatiblity check.
In particular, I'd advise to remove figures, as they can be quite large due to the requirement for publication.

**Third lesson: AI is very helpful, in the start and the end; not so much in the middle, though.**
I started tackling the problem by feeding the bst file to ChatGPT, and asked it to locate the parts to be changed.
It did a great job.

While this was the first serious time I inspected a bst file, 
it wasn't too difficult to understand some (not all) of its syntax,
and I soon confirmed that `format.journal.date` is the key variable I'd like to experiment with.
I made a copy of it and pasted the copy to the right place.
Brilliant! I had placed the year correctly!
There were only two remaining steps: 
removing the original `format.journal.date` 
and adding parentheses to its copy now in the right place.

Step 1 took two seconds.
Step 2 took **two hours**.

**Fouth lesson: Parentheses are not brackets.** 
Again, I asked ChatGPT:
etc etc etc
..
And I went back to StackExchange again, actually the same question again.
Yes, AI (both ChatGPY and whatever LLM model Google Search relies on) understood my fuzzy enquiry correctly:
I used the word 'brackets' while I meant 'parentheses'.
And they even suggested the right symbols.
However, AI didn't (or wasn't allowed to) lecture me explicitly on my inaccurate wording,
and I never thought parenthesses should be treated differently as brackets, 
at least in the context of this bst file.
In fact, I still have no idea if this distinct should be generalised to other bst files.
