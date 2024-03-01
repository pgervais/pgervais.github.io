---
layout: post
title:  "Datasets are never finished"
date:   2024-02-25
categories: eng ai
---

So, you've launched a great ML model in production, and it works great. What's left? Quite a lot actually.

Obviously you want to improve the model so that it works even better. So you spend a lot of time trying new model architectures, new hyperparameters, etc., to improve your metrics (since you have a [great test set](/eng/ai/2024/01/27/test-set-as-metric.html)). 

But after a while, improvements on the metrics don't seem to correlate with a better product. What could be going wrong?

![A picture of bolts](/assets/simon-kadula-TnlsqwNhbCA-unsplash.jpg)

It turns out that nobody took care of the datasets. When the team finally get to look at them they discover a range of issues:

- There is **not enough data anymore**. The model got bigger and bigger, and at some point the limitation becomes the size of the dataset - for training as well and validation/test data. It's the simplest thing you can do: gather more data. Remember that GenAI and LLMs wouldn't exist at all if it wasn't for some massive datasets.

- The product has been in production for a while, usage has shifted and data hasn't been updated to reflect that change (**data drift**). Any improvement to the model that the team made is now done in a slightly wrong direction. If you're doing a really good job at creating models that generalize better and better, you can get away with it for a while, but ultimately you'll have to update the datasets.

- **The test set contains too much noise**. Past a certain level of model quality, noise in the dataset will become a limitation. If you have 2% of incorrect labels in your test set and the model accuracy is around 3%, what you're measuring is essentially random. Spending time improving the situation is time well invested. Note that since it's the ratio of incorrect samples that matters you can fix the issue by simply adding more higher-quality data - and you'll make the dataset bigger at the same time, which is great.

There are other reasons to spend time grooming the datasets that are not necessarily directly related to model quality. For example:

- **Make the dataset smaller, so that model trains faster**. There are ways to simply drop samples from the training set that are redundant. It will have only a minor impact on performance, but the model will train faster. It also seems that depending on the dataset size, the impact depends on how difficult dropped samples are for the model: for small datasets, try dropping hard samples, for big datasets, try dropping easy samples.

- **Improving the ground truth to unlock new capabilities**. Image classification? Add more classes. OCR? add character segmentation, or font style. Translation? Add alternative translation to make things more inclusive (some languages like Turkish don't have gendered pronouns), etc.

What I hope you'll take away: as soon as you're maintaining an ML model used in production, it becomes necessary to treat your datasets as evolving entities, just like code. The past years have seen massive improvements due to better model structures, but improving data is still crucial. 

--- 

Photo by <a href="https://unsplash.com/@simonkadula">Simon Kadula</a> on <a href="https://unsplash.com/photos/a-pile-of-metal-screws-that-are-stacked-on-top-of-each-other-TnlsqwNhbCA">Unsplash</a>

[LinkedIn Post](https://www.linkedin.com/posts/activity-7167612754638393344--qh9) - if you have comments.
