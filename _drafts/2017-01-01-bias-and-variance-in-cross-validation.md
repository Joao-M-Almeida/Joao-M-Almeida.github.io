---
layout: post
title: Bias and Variance in Cross Validation strategies
tldr: Cross Validation is not as simple as it might seem at first. There are many different strategies to find "the best" model and to evaluate its performance. On this post I cover some of the most important approaches and try to convey the intuitions behind them.
---

<!-- Alternative title: How to do proper cross validation  -->

## __TL;DR__

Cross Validation is not as simple as it might seem at first.
There are many different strategies to find "the best" model and to evaluate its performance.
On this post I cover some of the most important approaches and try to convey the intuitions behind them. The main takeaway: Don't trust your cross validation score.

------

## Why the focus on Cross Validation ?

I have been discussing with [Lídia](https://github.com/lidiamcfreitas) her Machine Learning projects.
These are [Kaggle](https://www.kaggle.com/) competitions in the traditional format where the goal is to maximize the performance of a model measured in a test dataset.
Usually there is a public leaderboard where the contestants can know their performance on half the test data, but the final result of the competition is based on the performance on the other unknown half of the test data.
There's a large risk of overfitting the public leaderboard and getting a worst performance than expected in the private test set.

Thinking and reading about __Cross validation__ and how to estimate the performance of Machine Learning models led me to realize that it is a much more complex topic than what I thought.
So I decided to explore it and to write this post as a summary of I what I learned.

In this post I won't focus on the evaluation metric, let's just assume it's defined and we want to find a model that will have the best performance on real world data measured by that metric.
It can be the F1-score, accuracy, precision etc.

## Why do we need Cross Validation ?

Cross validation is a strategy to evaluate the performance of a model and is generally used as guide to tune its parameters.

The __naive approach__ to estimating the quality of a model is to train the model on all the available data and then test it in that same data.
One clear way to see how problematic this approach is is to think about the K Nearest Neighbors model when K = 1.
In that situation the model will classify all data points correctly, achieving a perfect performance.
It is however clear that this is an artificial performance.
Moreover it has severe __bias__ problems and is very prone to __overfitting__.

The next logical step would be to train the model in a subset of the data and test it on the remainder.
This is called the __hold-out__ method and although it still suffers from large bias and being prone to overfitting it at least presents the model with new samples during testing.
The usual size of the held out data varies between __15__ and __50 %__.
As you can easily see this is not an efficient use of the available data, your model is not


## K-Fold cross validation: the default



## Cross Validation Nested Loops


### Implementing with Scikit-learn

TODO: Add code

## More advanced Cross Validation Techniques

- Bootstrap
- Stratified Cross Validation
- Balanced Stratified Cross Validation
- Stratified Bootstrap

## Sources and Further reading:

- [Link](http://appliedpredictivemodeling.com/blog/2014/11/27/vpuig01pqbklmi72b8lcl3ij5hj2qm)

__CrossValidated Answers:__

- [Link ](http://stats.stackexchange.com/questions/14474/compendium-of-cross-validation-techniques?noredirect=1&lq=1)
- [Link ](http://stats.stackexchange.com/questions/61783/variance-and-bias-in-cross-validation-why-does-leave-one-out-cv-have-higher-var/244112#244112)
- [Link ](http://stats.stackexchange.com/questions/90902/why-is-leave-one-out-cross-validation-loocv-variance-about-the-mean-estimate-f?noredirect=1&lq=1)
- [Link ](http://stats.stackexchange.com/questions/61546/optimal-number-of-folds-in-k-fold-cross-validation-is-leave-one-out-cv-always?noredirect=1&lq=1)

__Pappers:__

- [Link](http://web.cs.iastate.edu/~jtian/cs573/Papers/Kohavi-IJCAI-95.pdf)
- [Link](http://www.jmlr.org/papers/volume5/grandvalet04a/grandvalet04a.pdf)
