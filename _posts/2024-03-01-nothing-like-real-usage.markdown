---
layout: post
title:  "There's Nothing Like Real Usage"
date:   2024-03-01
categories: eng tidbits
---

Prototypes are great tools to derisk an idea: their purpose is to quickly make sure your idea can work, without getting into the details. Often though there is a big gap between that and a great product, because you need to answer the question: is the product actually useful?

If regardless of the answer you're facing months of developments - for example you're building a video call app and need a very scalable backend - you'd better make sure the end result will be usable from the user's perspective as early as possible.

![A picture of UI drawings](/assets/amelie-mourichon-h3kEAHMl1k4-unsplash.jpg)

I'm of the opinion that the only way to answer this question of usefulness is to have some implementation that can be used in **real situations to discover the unknown unknowns**. It's a big conceptual difference from a prototype: the tool needs to be reliable enough and have just enough features to be used, but it's not an MVP either because you need to be able to overhaul it entirely if needed (remember the sunk-cost fallacy).

A trivial example: with video calls, latency and audio quality is often more important than video quality. But if your target audience is Deaf people who sign, audio doesn't matter and maybe video quality is more important than latency. There are many other things that could make or break the product, and just asking your potential users is not enough. Only in real situations will they be able to tell you what is critical.

How is a prototype not enough for this? 

My experience tends to show that when we manually test something we unconsciously avoid existing problems. Our brains are really effective at learning the quirks of anything and build ways around them. So you'll end up testing what already works over and over, which may or may not matter in practice. **Real usage forces you to go where the product doesn't work yet.**

For a similar point on this topic, I recommend Andy Matuschak's [Effective system design requires insights drawn from serious contexts of use](https://notes.andymatuschak.org/z7EQ2nVGus5B1rS9CqT18g6) and the links therein.

--- 

Photo by <a href="https://unsplash.com/@amayli">Amélie Mourichon</a> on <a href="https://unsplash.com/photos/black-android-smartphone-and-pink-case-h3kEAHMl1k4">Unsplash</a>
  
[LinkedIn Post](https://www.linkedin.com/posts/activity-7169692930713067520-YRbB) - if you have comments.