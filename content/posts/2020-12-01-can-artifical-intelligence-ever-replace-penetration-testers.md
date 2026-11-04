---
template: post
title: Can Artificial Intelligence ever replace penetration testers?
slug: ai-pentesting
socialImage: "/media/aipentesting/v2osk-1Z2niiBPg5A-unsplash.jpg"
draft: false
date: 2020-12-01T01:50:34.453Z
description: Can Artificial Intelligence ever replace penetration testers?
category: "Artificial Intelligence"
-tags:
	- "Artificial Intelligence"
---

- [Machine Learning](#machine-learning)
	- [Supervised Learning](#supervised-learning)
	- [Unsupervised Learning](#unsupervised-learning)
	- [Reinforcement Learning](#reinforcement-learning)
		- [AlphaGo](#alphago)
			- [Learning from the greats](#learning-from-the-greats)
			- [Teaching itself](#teaching-itself)
		- [Creativity](#creativity)
- [Applications in InfoSec](#applications-in-infosec)
	- [1. Learning from others](#1-learning-from-others)
	- [2. Learning from itself](#2-learning-from-itself)
	- [Blue Team](#blue-team)
- [Humans vs AI](#humans-vs-ai)
- [Conclusion](#conclusion)

In this blog post we'll explore _if_ machines can fully replace pe

Something to note is that predicting the future is hard and this is all entirely my opinion. Many people will have differing ideologies.

<hr>

## Machine Learning

Typically when we think of artificial intelligence, we may think of machine learning. Specifically, supervised machine learning.

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

But something important to note is that supervised learning is **only for classification**. That means it won't be able to "hack" things like we imagined. 

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

A good use case is disease symptoms. Given a bunch of patients, what symptoms do they all share in common?

This methodology is unsuited for a machine that can replace a penetration tester. 
1. It can't hack
2. All it'd say is something like "hackers typically use Metasploiit".

Although in a blue team environment, if you are repeatedly hacked and you're unsure as to why it may be helpful. But it'd be quicker to read the logs!

### Reinforcement Learning

This brings us onto the last type of artificial intelligence. The one I just so happened to study for 3 years and write a dissertation on! Reinforcement learning.

According to [Sutton & Barto](http://incompleteideas.net/book/the-book.html)

>  Of all the forms of machine learning, reinforcement learning is the closest to the kind of learning that humans and other animals do, and many of the core algorithms of reinforcement learning were originally inspired by biological learning systems.

Reinforcement learning is doing things by reinforcement. Humans learn not to touch the hot stove because it's hot. 

<figure>
	<img src="/media/aipentesting/loop.png" alt="Agent performs an action on the environment which returns a state (of the agent in the environment) and a reward.">
	<figcaption>Agent performs an action on the environment which returns a state (of the agent in the environment) and a reward.</figcaption>
</figure>

We perform an action (take our the rubbish) on our environment (the rubbish bin). This returns a reward (our mum gives us sweets and a "thank you") and a state (we are now cold, outside by our bins).

Reinforcement Agents learn the same way. This is called the action-reward loop.

Rewards can also be negative, which can discourage behaviour.

In fact, it is common to include both positive & negative rewards in the same system.

My hypothesis is that reinforcement agents _can_ learn to replace penetration testers. Let's explore this in more depth.

#### AlphaGo

Let's explore how Google's Deep Mind teaches their agents to learn how to play games.

<iframe width="560" height="315" src="https://www.youtube.com/embed/WXuK6gekU1Y" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This video is very good, but I'll explain roughly how it learns as well.

Firstly, Go is a game where the space of possible moves is vastly larger than in chess. Meaning that using any sort of exhaustive search (calculating all possible moves) is out of the question.

Our algorithm has to _learn_. 

##### Learning from the greats

Our algorithm **watches** how the best players play and _learns_ from them. The idea of [AI learning by watching](https://www.slashgear.com/nvidia-powered-robot-ai-learns-by-watching-humans-20531321/) isn't new. But the fact that the greatest Go players have played so many games allows the AI to learn all the tricks and tips of the masters.

This is a good idea to match the masters, but not a good idea to surpass them.

Humans make mistakes all the time. Our AI has to be perfect, so matching humans is not enough.

How do we get AlphaGo to be better than the masters?

##### Teaching itself

<figure>
	<img src="/media/aipentesting/fanhuang.png" alt="">
	<figcaption>https://www.nature.com/articles/nature16961</figcaption>
</figure>

How did AlphaGo become better than Fan Hui?

AlphaGo plays against itself hundreds of millions of times. The loser gets deleted, the winner gets chosen as the start of the next AI.

The AI has a base child that we choose at each iteration. This child is slightly modified (evolves) and this evolution is what makes it better over time. 

In this way, the AI:
* Starts off at Master level (after learning from the masters).
* Evolves and teaches itself to get better.

However, humans suck. Humans can never play perfectly. We make mistakes. We cause problems. We invovle emotions.

So, Google Deep mind created a new version of AlphaGo. _AlphaGo Zero_ as it has _zero_ knowledge of how other people play.

AlphaGo zeros starts off with a rule set and all possible moves it can make, and it teaches itself how to play.

<figure>
	<img src="/media/aipentesting/alphazero.gif" alt="">
	<figcaption>https://deepmind.com/blog/article/alphago-zero-starting-scratch</figcaption>
</figure>

After 3 days, it reaches the master level. After 5 days it can beat Lee Sedol. After 40 days it is so good that it can defeat the "world beater" version (the one that beat Lee Sedol) in 100 / 100 matches. 

*Fun fact*: While the one that beat Lee Sedol was a server, AlphaGo Zero (which can beat the Lee Sedol one in 100/100 games) uses **only 1 machine**.

<figure>
	<img src="/media/aipentesting/1machine.webp" alt="">
	<figcaption>https://deepmind.com/blog/article/alphago-zero-starting-scratch</figcaption>
</figure>

#### Creativity

One of the key aspects to being a great penetration tester is being creative. 

Can machines be creative? It's an oft asked question. I say yes. Neural networks are based on how the brain works. If the brain can be creative, I don't see why machines cant.

Furthermore we have seen creativity in the wild. AlphaGo's famous [Move 37](https://www.wired.com/2016/03/two-moves-alphago-lee-sedol-redefined-future/) is a genius & creative move that turned the course of the entire game and even flummoxed Lee Sedol.

<hr>

## Applications in InfoSec

Now let's apply what we learnt from AlphaGo to our own theoretical neural network to become a penetration tester.

We'll base our neural network roughly on how AlphaGo works.

There are 2 ways we can do this. For both of these methods, we will have to give the machine knowledge of the keyboard. As in, each key would have to be mapped to a certain input and our AI will have to learn what keystrokes make what words which makes what results.

<iframe width="560" height="315" src="https://www.youtube.com/embed/qv6UVOQ0F44" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In the above video we can see all the controls to Mario being mapped in the neural network. We'd hade to o the same for the AI but with the entire keyboard.

### 1. Learning from others

This is likely the first method that will appear. The AI watches others and learns:
* Commands to use.
* Techniques / tips.
* "Rules" of the engagement.

And gains some human intuition.

This works great, because as you may imagine the first few million generations of our AI will do almost nothing. It will be entirely based around learning what the keys do, and what words result in what things.

We also have a problem, what is the reward for our AI? We could say the reward is a reverse shell on the target machine. But all of our experts would have to get reverse shells for our AI to learn.

While this sounds impossible now, know that advancements of technology will make this possible in the future. All we need is more hacking videos (there are thousands on Youtube already) and better hardware to speed up the training process.

This version of the AI is unlikely to replace good penetration testers, but it can sure replace all beginner penetration testers.

### 2. Learning from itself

This is the AlphaGo Zero version. The AI starts with nothing but some basic rules. These rules might be:
* Don't shut down a target computer.
* Don't DoS a server.
* Don't download & publish customer information.

And then, from nothing else, it teaches itself how to hack.

This is much, much harder than watching other people and will require significantly more resources. But, the machine won't make mistakes like humans will. And it'll show creativity in knowing what to do. 

### Blue Team

Here's a fun idea for an AI that learns from itself.
* AI 1 defends their network.
* AI 2 attacks the network.

Then each evolution we only pick the best defender and best attacker. By the time we're finished, we'll have automated blue team && red team which are best in class.

<hr>

## Humans vs AI

As you can probably guess, penetration testers aren't really at threat any time soon. 60 or 70 years out at most. 

However, we are using AI in our security systems already and over time we'll use better & better systems. I predict the timeline to look like:
1. Create basic AI systems that rule out beginner penetration testers.
2. Beginners have to learn new skills, such as using the AI systems or just being better.
3. Because there's less beginners, expert penetration testers get paid more and eventually consult in building the AI.
4. Expert penetration testers are replaced by the AI system.
5. The top 0.1% of penetration testers remain as consultants for the AI.

As we saw with AlphaGo, even with it beating Lee Sedol it still had a consultant that helped build it (in the documentary).

However, I think this timeline might be more likely (carrying on from 3. in the last timeline)

1. Penetration Testers go from hacking directly to using automated systems with AI.
2. Penetration testers work with the AI to be the best.

This is what I like to call Human & Machine Synthesis. Machines are great, but unfortunately a machine might DoS a website, delete a production database or worse -- try to explain to HR why handing out your password to anyone that asks is a bad idea.

Humans & Machines together are stronger. Imagine if the machine gave the human a list of paths it thinks is vulnerable, for example:

```
sql injection -> database server -> domain admin
```

And the human can check for this. It would also help the fact that any large organisation would prefer humans to deal with private confidential information rather than an automated blackbox machine.

Garry Kasparov argues that machines can never be as creative as humans in his book [Deep Thinking](https://www.amazon.co.uk/Deep-Thinking-Machine-Intelligence-Creativity/dp/1473653509) which contradicts my opinion, but is worth reading.

<hr>

## Conclusion
To sum up:
* AI has the potential to replace humans.
* Not for a very, very long time/
* Even though it can, it likely won't because humans prefer humans over machines.

If you want to hear from people with differing opinions to I, check out these books:
* [Deep Thinking](https://www.amazon.co.uk/Deep-Thinking-Machine-Intelligence-Creativity/dp/1473653509)
* [Superintelligence](https://www.amazon.co.uk/Superintelligence-Dangers-Strategies-Nick-Bostrom/dp/0198739834/ref=sr_1_1?dchild=1&keywords=superintelligence&qid=1606857920&s=books&sr=1-1)
* [Life 3.0](https://www.amazon.co.uk/Life-3-0-Being-Artificial-Intelligence/dp/0141981806/ref=sr_1_1?dchild=1&keywords=life+3.0&qid=1606857924&s=books&sr=1-1)