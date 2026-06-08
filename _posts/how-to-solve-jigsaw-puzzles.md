---
title: How to Solve Jigsaw Puzzles
category: reflection
date: 2026-01-01 10:40:12
tags:
  - jigsaw-puzzle
  - AI
mathjax: true
---

My partner and I were dealing with jet lag yesterday, Hogmaney of 2025. We pulled out an old jigsaw puzzle and cracked on it. As you must know, a jigsaw puzzle is always initiated in a 'cracked' state, and the goal is to assemble (uncrack?) the pieces into a final, full picture. So started our quality time.

There were a few challenges. The jigsaw puzzle consisted of small pieces, the Scottish daylight in this time of winter was poetically soft, and both my partner and I had had our eyesights deteriorated (luckily not too much) in the past year(s), plus everything feeling misplaced due to the jet lag.

As we became stuck more frequently and for longer, in my mind grew a daunting idea--This old jigsaw puzzle may have lost a few pieces--It would never be complete again...<!-- more -->

After an hour or two, *'One is all, All is one'*[^1]. 

[^1]: A quote from *Fullmetal Alchmist*--perhaps more relevant to jigsaw puzzles figuratively than literally.

Indeed, the entire process felt like conducting scientific research, similar to the analogy commonly attributed to *The Structure of Scientific Revolutions* by Thomas S. Kuhn, but different due to the lack of the full picture (the dominant paradigm). In terms of personal feelings, the most similar part was to fight against the daunting idea that failure was inevitable, to keep faith in the completeness of the puzzle, and to proceed with constant patience and intermittent insights.

# A Machine Approach
Apparently, compared to human beings, machines are much more patient, tireless with repetitive work (if well powered and maintained). Additionally, we try to make them smart(er) by embedding Artificial Intelligence (AI) and to build AI by formalising insights, strategies, tricks, etc., as algorithms.

## Thus Spoke Gemini
So, this morning I asked Gemini (3 Flash, as on 01/01/2026), 'are there any AI system that can solve jigsaw puzzles'? Gemini did some online search and gave the response below:

---

Yes, there are AI systems that can solve jigsaw puzzles. This is an active area of research and development in **computer vision** and **machine learning**, especially using techniques like deep learning and genetic algorithms.

### 🧩 How AI Solves Jigsaw Puzzles

AI systems tackle the jigsaw puzzle problem, which is essentially a challenging combinatorial optimization task, by breaking it down into several steps:

1. **Image Processing/Piece Recognition:**
    
    - The system first needs to identify the individual puzzle pieces from an input image (like a scan or a photo of the scattered pieces).
        
    - This involves techniques like **edge detection**, **contour identification**, and **segmentation** to isolate each piece.
        
    - For physical puzzles, this is often handled by a robotic arm system that uses an attached camera and object detection models (like YOLO) to see and track the pieces.
        
2. **Feature Extraction and Compatibility Measurement:**
    
    - The AI extracts features from each piece, focusing on two main types of information:
        
        - **Shape/Geometry:** Analyzing the intricate shape of the edges (tabs and blanks) to determine which pieces physically fit together.
            
        - **Visual/Color Information:** Analyzing the color and pattern along the edges to see if the image flows seamlessly across the boundary.
            
    - **Deep Learning** models, such as **Siamese Neural Networks (SNN)**, are often trained to calculate a **compatibility measure**—a score that predicts how well two pieces should fit together both geometrically and visually.
        
3. **Piece Orientation and Reordering/Assembly:**
    
    - Once compatibility scores are available for all possible adjacent pairs, the system uses a **solver algorithm** to assemble the entire puzzle.
        
    - Since the number of possible arrangements grows exponentially ($N!$ for $N$ pieces), algorithms are needed to efficiently explore the solution space.
        
    - Common solving strategies include:
        
        - **Genetic Algorithms (GA):** These algorithms simulate natural selection, iteratively combining "parent" solutions (partial assemblies) that have high-fitness (high compatibility scores) to create better "child" solutions.
            
        - **Reinforcement Learning (RL) and Monte Carlo Tree Search (MCTS):** These methods treat puzzle solving as a sequential decision-making process, where the AI learns the optimal _actions_ (which piece to place next and where) to maximize the reward (a completed or highly-compatible puzzle). Examples include systems like **Alphazzle**.
            
        - **Combinatorial Optimization:** Framing the problem as finding the shortest path in a graph or a linear assignment problem, which can be solved using efficient algorithms like **Dijkstra's algorithm** or techniques like **Quadratic Programming**.
            

These systems can range from purely software-based tools that solve digital versions of puzzles, to **AI-powered robotic systems** that physically manipulate real-world puzzle pieces.

Would you be interested in learning more about the **different types of AI algorithms** used for puzzle solving, like Genetic Algorithms versus Deep Reinforcement Learning?

---

The three main steps are almost the same as I had imagined. I haven't verified all the details, but [Alphazzle](https://deepai.org/publication/alphazzle-jigsaw-puzzle-solver-with-deep-monte-carlo-tree-search) seemed legit[^2]. I also like Gemini's mention of physical puzzles, because it's not trivial for a robot to visually recognise and physically move all the pieces. 

## Caveats and Assumptions
Real-world ambient lighting is constantly changing. Small, individual pieces may not contain sufficient underlying visual features of the final picture. Perfeclty assembled pieces still have cracks--they may interfere with, if not dominate, some underlying visual features. It takes some effort to seggrate pieces from a pile, pieces facing down need to be flipped over, and during assembly pieces need to be lifted and put down. These tasks can be particularly challenging for a robot hand, because jigsaw puzzle pieces, many made of paperboard, are brittle. As ours, they can even be thin and tiny.

[^2]: I haven't reproduced all the results so you trust either me or the authors. It's commendable if you trust neither and try to reproduce their work--I'd appreciate it more if you let me know your results.

For now, let's pretend there exist a perfect robot system capable of accurate and fast visual recognition and precise and subtle piece manipulation. In other words, let's focus solely on the computational problem of how to reorder all the pieces based on their appearance. For greater formalisation, we further assume individual pieces have the identical shape of a square--no curved sides, knobs, or sockets--so that the appearance of any piece is entirely and only determined by its pixels.


## Model Complexity
Despite all the abstractions and simplifications, the computational model remains difficult. As Gemini states, 'the number of possible arrangements grows exponentially ($N!$ for $N$ pieces)'. 

I didn't ask Gemini how this statement was obtained, as I expected this $N!$ scaling by considering the following: Whenever $K$ pieces are correctly assembled, one can arbitrarily pick one empty slot adjacent to the assembled $K$ pieces, repeat step 2 (Feature Extraction and Compatibility Measurement) $4$ times (corresponding to $4$ directions) for each of the remaining $N-K$ pieces, and then determine the new configuration that maximises the compatibility. Therefore, $4(N-1)!$ iterations are required in total.

Note the operation of picking one empty slot (that indeed needs to be filled) is feasible and inexpensive, because we assume, as most jigsaw puzzles, the final, full picture is a rectangle of $L\times W$. Even if $L$ and $W$ are unknown beforehand, one can factorise $N$. If there are multiple ways of factorisation, it's more likely for $L$ and $W$ to be as close as possible.

While such weaker assumptions will lead to more iterations, I have no intention to go into the details to prove both lower and upper bounds grow exponentially--explicitly for a usual jigsaw puzzle that is 2D--as an exponential growth can be clearly shown with a 1D jigsaw puzzle.

A 1D jigsaw puzzle can be easily constructed by vertically (or horizontally) cutting a rectangular (full) figure into thin slices. Again, starting with $N$ slices, the goal is to reorder them and assemble them into a final, full figure. In this 1D setup, at iteration $K$ there are exactly $2$ empty slots on the left or right of the assembled $K$ pieces, one should maximise compatibility by testing each of the remaining $N-K$ pieces exactly $2$ times (upright and upside down) in both slots, and therefore in total $4(N-1)!$ iterations, again, are required (but we do not worry about which empty slot to pick at all).


# A Human(-like) Approach
While the machine approach guarantees success by iteratively adding jigsaw puzzle pieces one by one to a focused well-assebled group, my partner and I did not take the approach as it felt non-human and boring.

We built 'islands' first. We picked small number of pieces into a handful of groups based on visual similarity, similar to compatibility but an instinct first approximation and then with trial and error assemble some pieces into an island and others into another one. We worked simultaneously with a few islands. They were isoldated and grew first at the beginning. As we proceeded, it became harder and harder to find new pieces to add to them. However, as the islands grew bigger, it became easier for us to spot a way to merge/connect two islands into a bigger one. There were two factors: the visual semantics became clearer, and there were less remaining, isolated pieces.

Amongst modern AI models, visual transforms may be a particularly effectivfe candidate for solving jigsaw puzzles by emulating such human-like fast-and-slow thinking. Unlike other visual recognition tasks, solving jigsaw puzzles requires inferring spatial proximity from visual semantics. Most other visual AI models have built-in inductive bias of spatial proximity--they learn semantics based on spatial proximity, a one-way relation, while a visual transform are free from such bias and learns a two-way relation.

## Improved Efficiency
In general, this is a clever strategy (worked well for us!). Assuming the total $N$ pieces can be quickly sorted into $2$ piles, one consisting of $M$ pieces that will be assembled into an island and the rest $N-M$ pieces not so clear. Now step 2 needs to be repeated for $4(M-1)!$ in total for the first pile, followed by $4(N-M)!$ times for the remaining pieces, and $4(M-1)! + 4(N-M)! < 4(N-1)!$ is always true! Following the same reasoning, one can conclude quicker reordering (less iterations of step 2) is achieveable if all the pieces can be sorted into more than $2$ piles based on the instinct approximation.

The main caveat of the above reasoning is that we have overlooked the cost of the instinct approximation completely. For rigorosity, let's assume its cost to be $c_1$ and the cost of careful compatibility measurement to be $c_2$ (per piece). Then, the overall costs of the human-like and purely machine approach are $c_1 N + 4c_2 [(M-1)! + (N-M)!]$ and $4c_2 (N-1)!$.

For the human-like approach to improve efficiency, 

$$ c_1 N + 4c_2 [(M-1)! + (N-M)!] - 4c_2 (N-1)! < 0 $$

which gives 

$$ \frac{c_1}{c_2} < \frac{(N-1)! - (M-1)! - (N-M)!}{N/4} $$

Note first in the right hand side (RHS) $M$ is symmetric about $(N+1)/2$, and the closer to it $M$ is, the greater the RHS is. Unless $M=1$ or $N$, even when $M=2$ or $N-1$, the RHS is 

$$ \frac{(N-1)! - 1 - (N-2)!}{N/4} = \frac{(N-2)(N-2)!-1}{N/4} $$

which is greater than $1$, as long as $N\geq 4$. 

Therefore, as $c_1<c_2$ is implicitly assumed, the human-like approach is guaranteed to improve the overall efficiency. This is perhaps not surprising, as $c_1$ incurs a cost linear but  $c_2$ factorial in the number of pieces ($N$).




