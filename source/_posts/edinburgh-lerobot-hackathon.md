---
title: Edinburgh LeRobot Hackathon
category: log
date: 2025-06-17 10:30:24
tags:
---
The first time I visited Edinburgh was more than a decade ago. As a student tourist of a group of twenty or thirty, I didn't event remember if I visited the castle—what can be recalled is the night started earlier than anticipated when I was walking along Princess Street back and forth, trying to find a cheap place for dinner.

Last Saturday and Sunday, it was my first time participating in a hackathon, any hackathon. This event[^1], in particular, was for open-source robotics. It was the first time I worked with a robot arm, and just a few days ago when I registered for the event was the first time I learned about LeRobot. Moreoever, I had never met almost all the other participants until the event—what wasn't new to me was the local food I had for lunch.

[^1]: The primary [hackathon](https://huggingface.co/LeRobot-worldwide-hackathon) was organised by huggingface. The event was worldwide and free to participate—One needed to buy (or make) their own robot parts if they wanted to play with the hardware instead of simulation. Luckily I joined the local Edinburgh [event](https://lerobot-edinburgh.com/), organised by [Antreas Antoniou](http://antreas.io/) and [Pavlos Andreadis](https://people.inf.ed.ac.uk/Pavlos_Andreadis.html), where [robot arms](https://github.com/TheRobotStudio/SO-ARM100) were provided. Big thanks to all of them!

# Preparation
As our local event was advertised to everybody with the only constraint on capacity of travelling to central Edinburgh but no requirement on technical knowledge or skills, I registered without too much hesitation—I've collaborated with roboticists to deploy and validated my AI model earlier and I'd love more hands-on experience playing with robots myself. For the same reason, Edinburgh participants hadn't been asked to prepare anything but a laptop that could run LeRobot and a GPU-powered one if one would like to train their AI models. Therefore, my only preparation was to install [LeRobot](https://github.com/huggingface/lerobot) on my Ubuntu laptop.

Overall, I haven't run into any real problems when following the installation instructions, but there were a few blockers:
1. When configuring the `conda` environment, I did have to specify the version of `ffmpeg=7.1.1` as noted by the instruction. If not, my machine chose version `6.X`.
2. After `pip install -e .`, I hit the first error that there was not enough space on my disk. The error was fixed by deleting some data of the simulated experiments for my previous work that has been published. In total, LeRobot takes about 9G, including `pusht` and `smolvla` (to be mentioned soon).
3. After installation LeRobot, which seemed successful as there were no errors any more. I wanted to make sure visualisation working after `pip install -e ".[pusht]"`. I didn't install other packages for simulation because I intended only to play with the hardware at the event.
4. However, I hit an error as the module `rerun` couldn't be found, which resembled online discussions, but I was running a different script on a different OS. I also consulted ChatGPT, and found `rerun-sdk` was visible to `pip` but not `conda`. As there was at least one safe suggestion amongst all, `conda install -c conda-forge rerun-sdk`, I re-installed it and the visualisation ran smoothly on my machine.

# First Day
Sitting randomly at four tables, we went through some light-touch tutorials together and started configuration with the goal of first day that we could manually operate the robot to generated real data.

The official LeRobot documentation was surely the best guidance. We managed to
1. `find_port` to get the 'names' of the hardware,
2. `calibrate` to get the feasible range for all joints, and 
3. `teleoperate` to check that the follower arm (under teleoperation) would make the same move as the leader arm (under manual control).

The main blockers were denied permission for ports and human fatigue from plugging-unplugging-replugging cables. The first one was resolved by `sudo chmod 666 [port]` and the second by having great teammates and pizza!

The next step was to add camera(s), following documentation [here](https://huggingface.co/docs/lerobot/cameras). This was the part that I personally failed to grasp, because our team gradually convered our setup work onto one teammate's MacBook, which was apparently different from my machine[^2]—I bet hardware differences are one of the greatest reasons why robotics is challenging and interesting.

[^2]: