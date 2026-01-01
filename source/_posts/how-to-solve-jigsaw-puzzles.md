---
title: How to Solve Jigsaw Puzzles
category: 随笔
date: 2026-01-01 10:40:12
tags:
---

My partner and I were dealing with jet lag yesterday, Hogmaney of 2025. We pulled out an old jigsaw puzzle and cracked on it--Apparently, as you must know, a jigsaw puzzle is always initiated in a 'cracked' state, and the goal is to put (uncrack?) the pieces together. So started our quality time.

There were a few challenges. The jigsaw puzzle consisted of small pieces, the Scottish daylight in this time of winter was poetically soft, and both my partner and I had had our eyesights deteriorated (luckily not too much) in the past year(s), plus everything feeling misplaced due to jet lag.

More seriously, we didn't have the full (completed) picture. As we produced a few 'islands' and became more frequently stuck with how to expand and/or connect them, in my mind grew a daunting idea--This old jigsaw puzzle may have lost a few pieces--It would never be complete again...

After an hour or two, *'One is all, All is one'*[^1]. 

[^1]: A quote from *Fullmetal Alchmist*--perhaps more relevant to jigsaw puzzles figuratively than literally.

Indeed, the entire process felt like conducting scientific research, similar to the analogy commonly attributed to *The Structure of Scientific Revolutions* by Thomas S. Kuhn, but different due to the lack of the full picture (the dominant paradigm). In terms of personal feelings, the most similar part was to fight against the daunting idea that failure was inevitable, to keep faith in the completeness of the puzzle, and to proceed with constant patience and intermittent enlightments.

Apparently, compared to human beings, machines are much more patient. Consequently, we try to build Articial Intelligence (AI) by assembling enlightments, strategies, tricks, etc. So this morning I asked Gemini (3 Flash, as on 01/01/2026), 'are there any AI system that can solve jigsaw puzzles'? Gemini did some online search and returned the response below:

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

I haven't verified all the details but [Alphazzle](https://deepai.org/publication/alphazzle-jigsaw-puzzle-solver-with-deep-monte-carlo-tree-search) seemed legit[^2]. Anyway, the three main steps are exactly the same as I had imagined, and I also like Gemini's mention of physical puzzles. 

[^2]: I haven't reproduced all the results so you trust either me or the authors. It's commendable if you trust neither and try to reproduce their work--I'd appreciate it more if you let me know your results.

It's not trivial for a robot to recognise and assemble all the pieces--It takes a while to seggrate pieces from a pile, pieces facing down need to be flipped over at early stages, and they need to be lifted and put down in assembly--especially for a robot hand. Note jigsaw puzzle pieces are usually made of hardboard sheets, i.e., papers, and they can be thin and tiny.

For now, let's pretend there exist a perfect system capable of accurate and fast visual recognition and precise and subtle robot manipulation to focus on the main steps. The computational problem--how to reorder all the pieces--is difficult, because, as Gemini states, 'the number of possible arrangements grows exponentially ($N!$ for $N$ pieces)'. I obtain this $N!$ scaling by considering the following: Whenever $K$ pieces are correctly assembled, one can arbitrarily pick one empty slot adjacent to the assembled, and repeat step 2 (Feature Extraction and Compatibility Measurement) for $N-K$ times.

However, as human beings, my partner and I did not take this approach when solving our jigsaw puzzles. Assuming the final full picture to be rectangular, we knew pieces on the four corners were different from those on the edges and both of them different from all the rest (the majority) in shape. Starting from these minority special pieces on the corners and edges is a well-known strategy, but it didn't help us much as the final full picture wasn't available. 

We thus built 'islands' first. We used visual similarity, similar to