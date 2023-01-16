---
title: "Creating an app to solve "Mattemix"-game"
date: 2023-01-18T15:34:30-04:00
categories:
  - blog
tags:
  - AI
  - coding
---


## Why

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
comparable to the real thing. For me, this means not only doing a small POC, but also stitiching 
together the pieces required to build a real application.

A lot of technologies have been on my "To explore/learn" list for a while. I wanted to use this project to 
cross off a few of them. So, when my son got this board game for Christmas, I knew I had found the
perfect project. And this time I was determined to see it through to the end.

## Intersection of exciting stuff

So, what technologies did I want to familiarize myself with? Here's an excerpt from my list.

### [Modal](https://www.modal.com)

Modal is a complete rethink of the way we work with bulding data apps. 
I've been following one of the founders, Erik Bernhardsson, for a while.
He has written a couple of blog posts describing the vision and detailing what they want to achieve with Modal.

- [We are still early with the cloud](https://erikbern.com/2022/10/19/we-are-still-early-with-the-cloud.html)
- [What I have been working on: Modal](https://erikbern.com/2022/12/07/what-ive-been-working-on-modal.html)

A beatiful quote from the latter post:

> Somewhat ironically, software development is one of a vanishingly small subset of knowledge jobs for which the main work tool hasn't moved to the cloud. We still write code locally, thus we're constrained to things that work in the same way both locally and in the cloud. Thus, adapter tools like Docker. 
> I get this. I love writing code just on my laptop because of the fast feedback loops it creates. My laptop is full of weird-ass scripts and half-finished projects, and I haven't encountered any other tool that lets me iterate on these things as quickly, maybe with the exception of ssh into a devbox, which is something we've done for about 50 years now

That resonates with me. 
Short feedback loops are a prerequsite to work in flow. 
But short feedback loops become difficult to maintain as data, environments and compute resources grow.

### [Databutton](https://www.databutton.com/)

This is a platform that also is built with developer productivity in the front seat, and available from 
waitlist. Databutton provide a web interface, out-of-the box handling of storage, scheduling of jobs, handling of secrets and
environment for you.  

### [Streamlit](


### [Streamlit Lite]


### [Genetic Algorithm]
This is an "old" algorithm. It was invented in 1975 by John Holland.
Ever since solving a Job Shop Scheduling-problem with GA for a class some years ago, I've been looking for opportunities
to apply it to a "real" problem. 
Even though this project isn't exactly a Business problem, it's still a real problem, for which the GA might be a reasonable
approach. 

### [FastAPI]

This is a web framework that I am quite familiar with, and work with on a daily basis in my day job.
I didn't really have this on my list to learn, but I love working with it, and embrace every chance I get to 
learn more about it.

TODO: Image

## Architecture

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-filename.md`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `filename` is whatever file name you choose, to remind yourself what this post is about. `.md` is the file extension for markdown files.

The first line of the file should start with a single hash character, then a space, then your title. This is how you create a "*level 1 heading*" in markdown. Then you can create level 2, 3, etc headings as you wish but repeating the hash character, such as you see in the line `## File names` above.

## Basic formatting

You can use *italics*, **bold**, `code font text`, and create [links](https://www.markdownguide.org/cheat-sheet/). Here's a footnote [^1]. Here's a horizontal rule:

---

## Lists

Here's a list:

- item 1
- item 2

And a numbered list:

1. item 1
1. item 2

## Boxes and stuff

> This is a quotation

{% include alert.html text="You can include alert boxes" %}

...and...

{% include info.html text="You can include info boxes" %}


## Code

General preformatted text:

    # Do a thing
    do_thing()

Python code and output:

```python
# Prints '2'
print(1+1)
```

    2

## Tables

| Column 1 | Column 2 |
|-|-|
| A thing | Another thing |

## Footnotes

[^1]: This is the footnote.
