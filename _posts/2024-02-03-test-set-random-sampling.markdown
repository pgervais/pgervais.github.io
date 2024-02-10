---
layout: post
title:  "Test Set and Random Sampling"
date:   2024-02-03
categories: eng ai
---

[Last time](/eng/ai/2024/01/27/test-set-as-metric.html) I talked about the test set defining your metric. I'll point out some interesting consequence. 

If you search on the web for "train/valid/test splitting", you'll essentially find elaborate explanations of how to use `np.randn()`. It's clear for everyone that once you have a big pile of data points, you just split them randomly, let's say 10% in the validation and test sets, and 80% in the training set. End of the story, let's get to the interesting part, that is: training a model.

Wait wait wait wait. If you just randomly split your data points, it means that the data distribution in the test set is determined by whichever distribution you happen to have in the data you started from... hence you have no control over your metric. 
If you have a lot of data you can in theory adjust the data distribution before doing the random split. In practice that would mean dropping a lot of data points, which is not practical. 

**Measuring what you need to measure with the test set means you cannot use random splitting.** You'll need something more sophisticated than `sklearn.model_selection.train_test_split` to split your data.

Not having the same data distribution between the training and the test sets will sound heretical to some people, but deep learning practitioners have been doing it for a while without even realizing in. As long as the training pipeline includes some form of data augmentation, you are effectively changing the training set's statistical properties. So why not embrace this new flexibility and see what we can gain?

What about measuring model generalization? Examples: a good handwriting recognition model should generalize to writing styles that are not present in the training set ; a good image classifier should work well with new camera models, etc. By adding to the test set cases that the model never saw during training, you have the possibility of assessing whether your model can truly generalize. And more importantly **you can define** what generalization means.

If you find this intriguing, a lot has been written about a special case of this: compositional generalization. A possible starting point is the two papers introducing the [CLEVR](https://arxiv.org/abs/1612.06890) and [CLOSURE](https://arxiv.org/abs/1912.05783) datasets.

[LinkedIn post](https://www.linkedin.com/posts/activity-7159610253846675456-swZB)_