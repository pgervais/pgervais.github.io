---
layout: post
title:  "Your Test Set Is Your Metric"
date:   2024-01-27
categories: eng ai
---

Your test dataset is your model's performance metric.

Wait, isn't that obvious? It's one of these obvious things which can have serious consequences if overlooked.

Imagine you're in a company providing OCR services. Your model takes an image as input and returns the Unicode representation of all the text present in the image. The latest model you trained has much better performance on your test set, so you just go ahead an push it to production. A few days later, complaints from users trickle in. The new model has a lot of difficulties transcribing certain numbers which is essential when processing invoices: your clients are losing money fixing errors. After checking a few other things, you finally decide to look into the characters that are present in the test set. Numbers 3, 6 and 7 are not represented. Oops. 

Your metric has been ignoring those characters all along.

Wait. You've been relying on that metric for a while though and so far everything worked, why have things suddenly started to break? There could be many reasons for this: a change in the regularization during training, a change in the training set, bugs in the data augmentation pipeline, etc. 

It's like unit testing: if the coverage is not good enough, you'll miss bugs. It doesn't matter where they're from.

Non-exhaustive list of things that can go wrong with a test set:
- you have none (yes, that happens)
- it has identical data points as in the training set. Few people make this mistake, but it's good to always double-check.
- the number of data points is too low, which means you have a high uncertainty around your metric. Then you may see improvements when it's just random fluctuations.
- blind spots or near blind-spots in coverage: e.g. some characters or classes, some characteristic of the input (image size, type of device used for data acquisition, sequence length, etc.). What coverage means depends on your application and your end users, so there is no single rule to define it.
- misalignment with the kind of data you have in production: you have a good metric but it's looking in the wrong direction. This is the trickiest of all and, sadly, also the most important.

These can have massive implications for a production system. Remember [Google photo's gorilla debacle](https://www.bbc.com/news/technology-33347866)? It's already a company's nightmare, and this one is only a mild example (think about models used to help judges with sentencing instead). 

Grooming your test set is an important part in avoiding these consequences.

Follow-up post: [Test Set and Random Sampling](/eng/ai/2024/02/03/test-set-random-sampling.html)

[LinkedIn post](https://www.linkedin.com/posts/activity-7156984896891097088-jVZk)