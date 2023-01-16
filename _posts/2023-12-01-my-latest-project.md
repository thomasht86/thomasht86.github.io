---
title: "Building an app to solve `Mattemix` with genetic algorithm 🧬"
date: 2023-01-15T15:34:30-04:00
categories:
  - blog
tags:
  - AI
  - coding
  - update
---

## Backdrop

My son got this board game for christmas. 🎁🎄

![Mattemix](/assets/images/mattemix.png)

The premise is that you throw 14 dice, which can take a value between 1 and 15. 
As you throw, you flip an hourglass, and you have about 60 seconds to place the dice 
on a board. The score is calculated by adding the values of the dice that are placed successfully.
A placement is considered successful if an equation is correct.
This is how a board could look like if you would throw the sequence `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]`:

![Mattemix](/assets/images/board.png)

The score would be the sum of the values of the dice that are placed correctly.
In this case, `1+2+3=6`.

This got me pondering. What algorithm could I use to solve this problem?

I am quite sure that this is an [NP-complete](https://en.wikipedia.org/wiki/NP-completeness) problem.
Meaning that the solution can be verified in polynomial time, but finding the solution is not possible in polynomial time.

Calculating the score of each possible solution is easy. But knowing wheteher it is the optimal solution is not.
The solution can "easily" be brute-forced by trying out all possible combinations, but that would take a long time. 

For our case, with 14 possible positions for each of the dice, there are  ``14! = 87178291200`` possible solutions.

I wanted to try to solve this problem with a [Genetic Algorithm](https://en.wikipedia.org/wiki/Genetic_algorithm). It's a metaheuristic approach to solving optimization problems. It is inspired by the process of natural selection, where the fittest individuals are selected for reproduction (with some mutation sprinkled in) in order to produce offspring of the next generation. The hyperparameters of the algorithm are crucial to find good trade-offs between exploration (making sure not to get stuck in local minima) and exploitation (making sure we investigate the "neighborhood" of good solutions due to probability that even better solutions may exist nearby).

## Problem to be solved

I know from tinkering with genetic algorithms back in school, that it's a computationally expensive algorithm, and that you get huge benefits from parallelizing it. 
I consider myself some sort of "full-stack data scientist", but in my experience, building **production-ready** data applications, which requires different stuff to be run in different environments, while being able to scale at will, has required more time and effort than I was willing to invest for side projects.

**I want to be able to build and ship a data application in a weekend, while enjoying the process.**

For me to enjoy the process, I need short feedback loops. That has been hard to combine with scalability and environment requirements for building the really cool stuff.
Which is a main factor most of my earlier "weekend projects" have ended up as a mess of random scripts and notebooks. 🪦

I like to think that this is not just due to a lack of discipline or experience on my part. (I might be wrong, of course) 😄

But in general, I agree with Modal's founder, Erik Bernhardsson, that we are [still early with the cloud](https://erikbern.com/2022/10/19/we-are-still-early-with-the-cloud.html).

I've been following [Modal](https://www.modal.com) for a while, and I was excited to see that they had just launched their public beta. I decided to give it a try for this project.

A beatiful quote from the previously mentioned [post](https://erikbern.com/2022/10/19/we-are-still-early-with-the-cloud.html):

> Somewhat ironically, software development is one of a vanishingly small subset of knowledge jobs for which the main work tool hasn't moved to the cloud. We still write code locally, thus we're constrained to things that work in the same way both locally and in the cloud. Thus, adapter tools like Docker. 
> I get this. I love writing code just on my laptop because of the fast feedback loops it creates. My laptop is full of weird-ass scripts and half-finished projects, and I haven't encountered any other tool that lets me iterate on these things as quickly, maybe with the exception of ssh into a devbox, which is something we've done for about 50 years now

To learn more about Modal, I recommend reading [this](https://erikbern.com/2022/12/07/what-ive-been-working-on-modal.html) as well as the [docs](https://modal.com/docs/guide).

## Intersection of exciting stuff

I've always had a bunch of ideas for side projects. Most of them have been abandoned after
the initial enthusiasm. This time I wanted to try something different. I wanted to build an 
app that I would actually publish. I needed to prove to myself that I had the discipline to 
see a project through to the end, also when it is "just" a side project.

I have a real passion for learning, and I thoroughly enjoy exploring new technologies, libraries
and frameworks. I also have a passion for solving problems. I wanted to combine these two passions
in a project that would be both fun and useful (in terms of learning, maybe not the final application).

Scott Young (Author of Ultralearning) has written a lot of great content on learning and "How to
choose a project". I highly recommend reading his blog posts on the subject. One of his main points
is that you should "Do the real thing". This means that you should build something that is actually
comparable to the real thing. For me, this means not only doing a small notebook POC, but also stitiching 
together the pieces required to build a real application.

A lot of technologies have been on my "To explore/learn" list for a while. I wanted to use this project to 
cross off a few of them. So, when my son got this board game for Christmas, I knew I had found the
perfect project. And this time I was determined to see it through to the end.

## The tech stack

I wanted to use this project to explore a few things that I had been meaning to try out for a while.
- [stlite](https://github.com/whitphx/stlite)
- [numba](https://numba.pydata.org/)

Another favorite framework of mine is [FastAPI](https://fastapi.tiangolo.com/), so I was pleased to see that Modal supports it out of the box.
A cool thing I learned, is how FastAPI easily can be used to deploy static files 🤩. I used this to deploy the frontend, and will definitely use it in the future.

## The result

The app is running [here](https://thomasht86--mattemix-solver-wrapper.modal.run/). 
(As it uses stlite (powered by pyodide and WASM), it will take a while to start up the first time you visit the page)


![gif](/assets/images/mattemix-ga.gif)

It enables me to find some pretty good solutions to the problem.
For the sequence `[1,2,3,4,5,6,7,8,9,10,11,12,13,14]`, it finds the optimal solution in about 50 seconds.
The code is available on [Github](https://github.com/thomasht86/modal_mattemix_ga). You might be surprised how little code it is. 

## The takeaway

I had a really great developer experience building this small app, and can't wait too see what else I can build with it! 
❤️‍🔥🧑‍💻

DISCLAIMER: I am not affiliated with Modal in any way. I just really like their product and wanted to share my experience with it.
