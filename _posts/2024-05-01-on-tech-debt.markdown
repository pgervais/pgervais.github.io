---
layout: post
title:  "A Personal Take on Tech Debt"
date:   2024-05-01
categories: eng tidbits
---

In software engineering the concept of "technical debt" is ubiquitous. Everybody who worked on the same codebase for more than a few months knows how it feels: this impression of wasting time because you have to rewrite some part of the code, or because you need to put some effort just to keep the lights on. At the same time, my experience is that most software engineers disagree on the exact definition of technical debt. This post is an attempt at understanding why that is.

![A picture of a man in a hoody sitting on a couch with his hands over his face, looking tired, in a messy room full of empty cardboard boxes.](/assets/christian-erfurt-sxQz2VfoFBE-unsplash.jpg)

[Wikipedia defines technical debt](https://en.wikipedia.org/wiki/Technical_debt) (as of today) as:

> [...] implied cost of future reworking required when choosing an easy but limited solution instead of a better approach that could take more time.

It's a rather restrictive definition that implies two things:
- Tech debt occurs consciously: you know there is a better solution.
- Tech debt comes from easy solutions. Good solutions take time and effort.

It also has vague overtones of accusation: if teams were doing a proper job, tech debt wouldn't exist.

I believe this take is misguided because __most of the time you do not know what the best solution is ahead of time__, and sometimes the "easy solution" (hear: lazy) is the best one.

I'd like to propose this definition instead:

> Technical debt happens when you lose a bet on how the software will evolve and that lost bet causes unexpected extra work.

Every time you write a modification to a piece of code, you do so because you're betting it will be beneficial. I'm talking about betting because it's usually impossible to know for sure that it'll be a net plus. Will users like the feature? Will it scale enough? Will it be shipped fast enough? Will it be bug-free enough? Will it enable evolving the product easily in two years? Nobody really knows. 

In other words, __there is usually no way to tell whether the change you're doing right now is/will be technical debt or not__. For the purists out there: this is not to say that all practices are equivalent: we know that some actions will cause more problems than others. But it's _situational_, not _structural_. That explains why it's essentially impossible to write a tool that tells you whether your change has tech debt or not: you would have to predict the future for that to work. 

Examples:

**No tests**. This is usually presented as the canonical example of tech debt. No tests == tech debt. But when you look a little deeper, things are not so simple. Google's [Risk-Driven Testing post](https://testing.googleblog.com/2014/05/testing-on-toilet-risk-driven-testing.html) has a great example: you write a piece of code whose sole purpose is to turn down a feature. You will need that code for a few months only (that's the bet). Writing extensive tests is likely a waste of time because manual testing will achieve the same level of safety and will take less effort. Losing the bet here means needing the code more much longer than expected, in which case the cost of accumulated manual testing can surpass the cost of automated testing.

**Using an email address to identify an account**. Typical sign up flow: when registering a user, ask them for their email address and use that as a key in the database. This solution has plenty of nice properties given that email addresses are guaranteed unique worldwide. It's a bit tricky when a user wants to update their login, but doable. A few years in, with the assumption that users are identified by email address baked everywhere in the codebase, comes WhatsApp that identifies people by phone number. Suddenly you're faced with users who do not even have an email address. The entire codebase becomes a giant pile of tech debt. You just lost a bet that you didn't even know you made. Could that have been avoided? It depends on the context. In 2002, probably not. In 2020? Definitely yes.

**Working under time pressure**. Cutting corners temporarily is a useful tool when what matters is time-to-ship. Let's say you've hired people for one month to do some manual work for you, and that depends on a piece of software you're maintaining. As the project progresses you find several issues that are slowing people down. It's not practically possible to ship the fixes fast and have a very polished codebase. You're faced with two main options: 

1. keep the code quality very high, ship "late". The final output of the external team will be low. Bet: it will be compensated for by related longer-term gains.
2. ship as fast as possible, with a lower code quality. It will maximize the external team's output. Bet: engineers are able to deliver working fixes with a lower code quality, and the code will be improved once the rush phase is over.

I would (and did) take bet number 2, even though I know it deliberately creates work right after the project ends. It's definitely a case where we know ahead of time that the work is subpar, but the actual extent of the damage still depends on external factors: mainly the team's willingness/ability to spend time consolidating the codebase after the project is over. This is were having a good relationship with stakeholders - especially managers - is essential. Documenting the bet very clearly could help with making everybody aware of the tradeoffs and making the consolidation period more acceptable.

I've also seen the reverse, where you do things very well so that your future selves do not have extra work. Sadly, the same framework applies: you never know that all the effort you've put in will pay off, because your project might be cancelled tomorrow, user feedback is so bad that you need to rework a lot of things, one of your dependencies changes a lot (Tensorflow, I'm looking at you), etc. Programming is always a balancing act between too much and not enough.

Last but not least, **another uncertainty is about *who* will do the future extra work**: often it's not the person who made the initial modification. It's very easy this way to dump grungy work onto someone else without asking, and it happens often. Not wonder most people are upset about tech debt! ~~If~~ When you're on the receiving side of tech debt, remind yourself that the sender likely bet on something and lost. You did it too :)

My takeaways:

- Tech debt cannot be defined outside of a context: it's situational, no structural.
- Tech debt is unavoidable in general because you cannot predict the future. Budget time to tackle it.
- Corollary: best practices are just heuristics. They work well most of the time, but keep an eye out for the corner cases were breaking them is a better solution.

Related reading: [There's Nothing Like Real Usage](/eng/tidbits/2024/03/01/nothing-like-real-usage.html).

---

Photo by <a href="https://unsplash.com/@christnerfurt">Christian Erfurt</a> on <a href="https://unsplash.com/photos/man-covering-face-with-both-hands-while-sitting-on-bench-sxQz2VfoFBE">Unsplash</a>
