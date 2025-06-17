---
title: Edinburgh LeRobot Hackathon
category: log
date: 2025-06-17 10:30:24
tags:
---
The first time I visited Edinburgh was more than a decade ago. As a student tourist of a group of twenty or thirty, I didn't event remember if I visited the castle—what can be recalled is the night started earlier than anticipated when I was walking along Princess Street back and forth, trying to find a cheap place for dinner.

Last Saturday and Sunday, it was my first time participating in a hackathon, any hackathon. This event[^1], in particular, was for open-source robotics. It was the first time I worked with a robot arm, and just a few days ago when I registered for the event was the first time I learned about LeRobot. Moreoever, I had never met almost all the other participants until the event—what wasn't new to me was the local food I had for lunch.

[^1]: The primary [hackathon](https://huggingface.co/LeRobot-worldwide-hackathon) was organised by Hugging Face. The event was worldwide and free to participate—One needed to buy (or make) their own robot parts if they wanted to play with the hardware instead of simulation. Luckily I joined the local Edinburgh [event](https://lerobot-edinburgh.com/), organised by [Antreas Antoniou](http://antreas.io/) and [Pavlos Andreadis](https://people.inf.ed.ac.uk/Pavlos_Andreadis.html), where [robot arms](https://github.com/TheRobotStudio/SO-ARM100) were provided. Big thanks to all of them!

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

[^2]: I arrived at the event venue earlier the second day, trying to setup everything on my own machine, but only managed to get calibration and teleoperation work, not yet cameras.

While we were configuring the hardware and the software, we discussed what task we'd like the robot to perform. We all wanted to leverage the pre-trained [SmolVLA](https://learnopencv.com/smolvla-lerobot-vision-language-action-model/) model, but honestly it was difficult to make a feasible plan due to our unfamiliarity with the model. In particular, we only knew the model was a vision-language-action model formed from transformers and pretrained with LeRobot data on Hugging Face—we hadn't studied its architecture in detail, nor examined the pretraining data. Our vague idea was to train (or fine-tune) a model that could pick up different number of items according to natural language inputs.

We then started testing for two purposes:
1. We needed to make sure videos could be recorded, uploaded, and visualised properly, so that we'd have a working pipeline for data collection.
2. We needed to choose which item(s) to be picked by the robot.

There were two main issues, respectively:
1. The arguments for camera, e.g., id, spec, needed to be tweaked when running the script for recording—We used what it worked for the MacBook with solutions copied and pasted from online discussions, but we didn't get to the bottom of it, and the solution didn't work directly on my machine[^2].
2. Most items were not easily pickable even with teleoperation—We ended up using Play-Dough, which was deformable, so fine control of the gripper became less necessary.

Overcoming the above issues, our team started to test the SmolVLA model in the last hour before the event venue closed. Again, the official documentation was decent, and without too much trial and error, our robot begun moving under the auto-control of the pretrained model. The only issue was that we didn't find a way to run the pretrained model out of box as it was, and had to 'fine tune' it for several hundreds of steps (using video recordings during configuration).

> My understanding is that real-world experiements are fundamentally different from simulated ones in that we can never have a perfect replica of the 'environment', and therefore any pretrained model must be fine tuned for sensible performance in the new environment. 

As we didn't really fine tune the model, the robot was merely chattering—It was told to 'move a blue block to the green area' but was not even interested in the blue block. 

We found the pretraining dataset consisted of many videos from side cameras, not a camera mounted on the robot arm. We changed the setup to two side cameras, but didn't see any improvement.

'Fine-tuning with 50+ episodes' was the official recommendation, and we decided to follow it the next day.

# Second Day
As we knew our cans and can'ts better, we started with recording videos using teleoperation after 