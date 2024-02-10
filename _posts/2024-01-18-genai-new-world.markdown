---
layout: post
title:  "GenAI is a new world"
date:   2024-01-18
categories: eng ai
---

Why I think recent GenAI / LLMs are a step into a new (computer) world.

My LinkedIn feed is full of posts from excited software engineers talking about LLMs in relation to programming languages, API, algorithms, etc. The scientific literature is regularly claiming to have proved "guarantees" about such and such training algorithm and modeling technique. A lot of effort is put towards making LLMs reliable, consistent, etc.

I think all of this misses a very important point: I believe LLMs are fundamentally of a different nature than algorithms.

(for the nitpicky out there: yes, I know, LLMs are implemented using algorithms. Bear with me). LLMs emerged after decades of effort to build a model of the human brain: it's not surprising that they share some of our quirks, like having unreliable memory, having difficulty with exact computation, and coming up with all kinds of stories. Trying to coerce LLMs into behaving like an algorithm is like trying to drive an airplane on the highway: it sort of works, but as soon as you try to go fast, it's very hard to maintain the illusion that you're driving a car.

What is happening is that for the first time ever we have an effective way to represent meaning. It's not perfect, but that's likely structural. Look at the seemingly simple problem of image classification: giving the name of an object in an image. Such system could know about cars, airplanes, cats, dogs, people, utensils, plants, screwdrivers, PC connectors, plushes, and many other concepts. What is the system supposed to answer when showed an image of a plush car? plush, car, something else? And when you think about it, what exactly is a car? how much of it do you need to see in the picture to qualify as a car? If you only see the driving wheel, is it still a car or is it a driving wheel? What if it's a car cut into two halves? if part of it is physical missing? etc. Humans have no issues with all those cases because they know how much context to add or drop when manipulating those concepts. An simple image classifier can't do it, but a visual LLM can.

People tried to represent meaning with algorithms, taxonomies, formal grammars, and mostly failed. These tools are too rigid and too specific to effectively represent the complexity of the world. There is a reason why life developed those fuzzy neural networks: a pocket calculator stood no chance in evolution. It's also no mistake that AI already found great applications in biology. It's very hard to model biological systems with algorithms: it's just too complex and fuzzy. But it's a perfect fit for neural networks.

Conclusion? computers are finally breaking free from math. LLMs are only the first step. Rejoice!

[LinkedIn post](https://www.linkedin.com/posts/activity-7153488666248564737-WMgR)