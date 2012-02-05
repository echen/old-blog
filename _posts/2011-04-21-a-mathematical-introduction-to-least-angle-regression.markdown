---
date: '2011-04-21 00:16:36'
layout: post
slug: a-mathematical-introduction-to-least-angle-regression
status: publish
title: A Mathematical Introduction to Least Angle Regression
wordpress_id: '102'
categories:
- expository
tags:
- least angle regression
- statistics
---

(For a layman's introduction, see [here](/2011/03/14/least-angle-regression-for-the-hungry-layman/).)

Least Angle Regression (aka LARS) is a **model selection method** for linear regression (when you're worried about overfitting or want your model to be easily interpretable). To motivate it, let's consider some other model selection methods:



	
  * **Forward selection** starts with no variables in the model, and at each step it adds to the model the variable with the most explanatory power, stopping if the explanatory power falls below some threshold. This is a fast and simple method, but it can also be too greedy: we fully add variables at each step, so correlated predictors don't get much of a chance to be included in the model. (For example, suppose we want to build a model for the deliciousness of a PB&J sandwich, and two of our variables are the amount of peanut butter and the amount of jelly. We'd like both variables to appear in our model, but since amount of peanut butter is (let's assume) strongly correlated with the amount of jelly, once we fully add peanut butter to our model, jelly doesn't add much explanatory power anymore, and so it's unlikely to be added.)

	
  * **Forward stagewise regression** tries to remedy the greediness of forward selection by only partially adding variables. Whereas forward selection finds the variable with the most explanatory power and goes all out in adding it to the model, forward stagewise finds the variable with the most explanatory power and updates its weight by only epsilon in the correct direction. (So we might first increase the weight of peanut butter a little bit, then increase the weight of peanut butter again, then increase the weight of jelly, then increase the weight of bread, and then increase the weight of peanut butter once more.) The problem now is that we have to make a ton of updates, so forward stagewise can be very inefficient.


LARS, then, is essentially forward stagewise made fast. Instead of making tiny hops in the direction of one variable at a time, LARS makes optimally-sized leaps in optimal directions. These directions are chosen to make equal angles (equal correlations) with each of the variables currently in our model. (We like peanut butter best, so we start eating it first; as we eat more, we get a little sick of it, so jelly starts looking equally appetizing, and we start eating peanut butter and jelly simultaneously; later, we add bread to the mix, etc.)

In more detail, LARS works as follows:

	
  * Assume for simplicity that we've standardized our explanatory variables to have zero mean and unit variance, and that our response variable also has zero mean.

	
  * Start with no variables in your model.

	
  * Find the variable $latex x _ 1 $ most correlated with the residual. (Note that the variable most correlated with the residual is equivalently the one that makes the least angle with the residual, whence the name.)

	
  * Move in the direction of this variable until some other variable $latex x _ 2 $ is just as correlated.

	
  * At this point, start moving in a direction such that the residual stays equally correlated with $latex x _ 1 $ and $latex x _ 2 $ (i.e., so that the residual makes equal angles with both variables), and keep moving until some variable $latex x _ 3 $ becomes equally correlated with our residual.

	
  * And so on, stopping when we've decided our model is big enough.


For example, consider the following image (slightly simplified from the [original LARS paper](http://www.stanford.edu/~hastie/Papers/LARS/LeastAngle_2002.pdf); $latex x _ 1, x _ 2$ are our variables, and $latex y$ is our response):

[![LARS Example](http://dl.dropbox.com/u/10506/blog/lars/lars-example.png)](http://dl.dropbox.com/u/10506/blog/lars/lars-example.png)

Our model starts at $latex \hat{\mu _ 0} $.



	
  * The residual (the green line) makes a smaller angle with $latex x _ 1 $ than with $latex x _ 2 $, so we start moving in the direction of $latex x _ 1 $.
At $latex \hat{\mu _ 1} $, the residual now makes equal angles with $latex x _ 1, x _ 2 $, and so we start moving in a new direction that preserves this equiangularity/equicorrelation.

	
  * If there were more variables, we'd change directions again once a new variable made equal angles with our residual, and so on.


So when should you use LARS, as opposed to some other regularization method like lasso? There's not really a clear-cut answer, but LARS tends to give very similar results as both lasso and forward stagewise (in fact, slight modifications to LARS give you lasso and forward stagewise), so I tend to just use lasso when I do these kinds of things, since the justifications for lasso make a little more sense to me. In fact, I don't usually even think of LARS as a model selection method in its own right, but rather as a way to efficiently implement lasso (especially if you want to compute the full regularization path).
