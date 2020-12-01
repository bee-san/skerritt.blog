---
template: post
title: Can Artifical Intelligence ever replace penetration testers?
slug: ai-pentesting
socialImage: /media/p2p.jpg
draft: true
date: 2020-12-01T01:50:34.453Z
description: Can Artifical Intelligence ever replace penetration testers?
category: "Artificial Intelligence "
---

# Introduction

In this blog post we'll explore _if_ machines can fully replace pe

* Machine learning
* Reinforcement learning
* Can machines be creative? Alphago!
* replaces low skilled pentesters -> pentesters have to learn to work with these AI tools -> human & machine synethesis

## Machine Learning

Typically when we think of artifical intelligence, we may think of machine learning. Specifically, supervised machine learning.

### Supervised Learning

In supervised learning, we have follow the formula:

> Labelled input -> machine learns -> machine outputs

The labelled input is the largest part here. We have to provide the machine learning algorithm with a table like:

| Label | 4 Legs | Barks |
|-------|--------|-------|
| True  | True   | True  |
| False | True   | False |

This table answers the question:

> Is that a dog?

We give it features. That's the _4 legs_ and _Barks_ features. 

And we label it True / False if it is a dog or not. Humans have to label it true / false, machines cannot. This is wwhy supervised learning is quite slow. But also, we face 2 problems with supervised learning:
* We need **a lot** of data (millions of data points with billions of features) for high accuracy
* We need the labels to be accurate 

As you can tell, in the real world these 2 points are hard to find combined. So hard in fact, IBM once said:

> "Anyone can build an AI with 99.9% accuracy. The issue is building the dataset."

Our labels are often binary, True and False. They can be other things such as categories or classifications.

But something important to note is that supervised learning is **only for classiifcation**. That means it won't be able to "hack" things like we imagined. 

However our supervised learning algorithm will learn what exploits _might_ work given a port scan, but it won't be able to hack it for us.

This idea of Human + Machine synthesis is something we'll explore later.

### Unsupervised Learning

We've seen supervised, but what about unsupervised?

Given data, our algorithm attempts to find patterns. 

| 4 Legs | Barks |
|--------|-------|
| True   | True  |
| True   | False |

Our algorithm may say:

> Things that bark are dogs, but not all things with 4 legs are dogs

This requires a monumental amount of data, but it can find patterns much better than humans can provided the data is correct. 

A good use case is disease symptoms. Given a bunch of paitents, what symptoms do they all share in common?

This methodology is unsuited for a machine that can replace a penetration tester. 
1. It can't hack
2. All it'd say is something like "hackers typically use Metasploiit".

Although in a blue team environment, if you are repeatedly hacked and you're unsure as to why it may be helpful. But it'd be quicker to read the logs!

### Reinforcement Learning

This brings us onto the last type of artifical intelligence. The one I just so happened to study for 3 years and write a disseration on! Reinforcement learning.

According to [Sutton & Barto](http://incompleteideas.net/book/the-book.html)

>  Of all the forms of machine learning, reinforcement learning is the closest to the kind of learning that humans and other animals do, and many of the core algorithms of reinforcement learning were originally inspired by biological learning systems.

Reinforcement learning is doing things by reinforcement. Humans learn not to touch the hot stove because it's hot. 

<figure>
	<img src="/media/aipentesting/action-reward-loop.svg" alt="Agent performs an action on the environment which returns a state (of the agent in the environment) and a reward.">
	<figcaption>Agent performs an action on the environment which returns a state (of the agent in the environment) and a reward.</figcaption>
</figure>

We perform an action (take our the rubbish) on our environment (the rubbish bin). This returns a reward (our mum gives us sweets and a "thank you") and a state (we are now cold, outside by our bins).

Reinforcement Agents learn the same way. This is called the action-reward loop.

Rewards can also be negative, which can discourage behaviour.

In fact, it is common to include both positive & negative rewards in the same system.

My hypothesis is that reinforcement agents _can_ learn to replace penetration testers. Let's explore this in more depth.

#### Reinforcement Learning in Penetration Testing

Let's explore how Google's Deep Mind teaches their agents to learn how to play games.