---
date: '2011-03-14 04:25:09'
layout: post
slug: a-kernel-density-approach-to-outlier-detection
status: trash
title: A Kernel Density Approach to Outlier Detection
wordpress_id: '47'
categories:
- expository
tags:
- fraud detection
- kernel density estimation
- machine learning
- outlier detection
- r
- statistics
---

I describe a kernel density approach to outlier detection on small datasets. In particular, my model is the set of prices for a given item that can be found online.


# Introduction


Suppose you're searching online for the cheapest place to buy a stats book you need for class.

You initially find the following prices:

    
    $50 - Amazon
    $55 - Barnes & Noble
    $52 - Walmart
    $50 - Borders


You're about to buy it from Amazon when you whimsically decide to try searching again. This time you find an eBay listing for the book at the low price of $30.

Should you buy it from eBay? Or is the listing just a scam? What if, instead, the price distribution of the other sellers were more widely dispersed?

    
    $50 - Amazon
    $75 - Barnes & Noble
    $60 - Walmart
    $90 - Borders


In other words, given the price distribution of the other sellers, you'd like to know how likely it is that a price of $30 is legitimate.

I describe a solution to this problem based on kernel density estimation.


# Other Approaches


Let's consider some other approaches first. Suppose we have a set of prices $latex {x _ {min}} cup {x _ 1, ldots, x _ n}$, where $latex x _ {min}$ is strictly less than all the other prices in $latex X = {x _ 1, ldots, x _ n}$.


## A Normal Approach


One simple approach to determining how cautious we should be of the price $latex x _ {min}$ is to calculate the mean $latex mu _ X$ and standard deviation $latex sigma _ X$ of $latex X$, and flag $latex x _ {min}$ if it falls some number of standard deviations below the mean.

However, this approach is flawed for several reasons. First, what if the prices in $latex X$ are all equal, say $latex X = {$50, $50, $50}$, so that $latex sigma_x = 0$? Then any $latex x_{min} < 50$ will be flagged, even $latex x _ {min} = $49$, which we don't want.

A simple heuristic (say, flag $latex x _ {min}$ only if it also falls at least $latex 10%$ below $latex mu _ X$) can fix this problem, though, so a more glaring problem is that the approach assumes prices follow a normal distribution, which they often do not. For example, bimodal distributions such as the following

    
    $20 - Amazon
    $25 - Barnes & Noble
    $22 - Walmart
    $21 - Borders
    
    $45 - eBay
    $40 - Books Inc.
    $43 - Waldenbooks


often arise, in which sellers seem to fall into two sets, one with higher prices and one with lower. (For example, perhaps a paperback version of a book was just released, and the megastore booksellers have slashed the price of the hardback version accordingly, while the small-scale booksellers have yet to react.)

In general, it is unclear what distribution prices fall into (they do not have a lognormal distribution either), so it seems that we must look at non-parametric approaches instead.


## An IQR Approach


One non-parametric method (which we all learn in grade school) is the interquartile method, in which we calculate the interquartile range of $latex X$ (the difference between the price falling in the $latex 75$th percentile of $latex X$ and the price falling in the $latex 25$th percentile of $latex X$) and view $latex x _ {min}$ with caution if it falls below $latex mu _ X - cIQR(X)$ for some positive constant $latex c$.

Again, though, this method fails. For example, in the bimodal distribution above, the 75th percentile of the prices is 41.50 and the 25th percentile is 21.5, giving a rather large interquartile range of 20.00. Even with a conservative choice of $latex c = 1.5$, we flag outliers only if they fall below $latex mu _ X - 1.5($20) = $latex 30.86 - 1.5($20) = $latex 0.86$, which doesn't seem correct.

We need, then, a non-parametric approach which also takes into account the dispersion and clusters of prices.


# A Kernel Density Approach


Recall that the kernel density estimate of a price $latex x$ given prices $latex X = {x _ 1, ldots, x _ n}$ is

$latex KDE(x) = frac{1}{n} sum _ {i = 1} ^ n Kleft(frac{x - x _ i}{h}right),$

where $latex K$ is some kernel function and $latex h$ is a bandwidth parameter.

In my tests, I used a Gaussian kernel with bandwidth $latex 0.1x _ i$,

$latex Kleft(frac{x - x _ i}{0.1x _ i}right) = frac{1}{sqrt{2pi}} e ^ {frac{-(x - x _ i) ^ 2}{2(0.1x _ i) ^ 2}}.$



For example, given a set of original prices $latex {50, 55, 52, 50, 90, 95, 93}$





[![Original Prices](http://dl.dropbox.com/u/10506/blog/kde-outlier-detection/original%20prices.png)](http://dl.dropbox.com/u/10506/blog/kde-outlier-detection/original%20prices.png)





here are the kernel density estimates of a new set of prices:





[![Kernel Density Estimate of New Prices](http://dl.dropbox.com/u/10506/blog/kde-outlier-detection/kernel%20density%20estimates.png)](http://dl.dropbox.com/u/10506/blog/kde-outlier-detection/kernel%20density%20estimates.png)





Notice the two humps around 50 and 90, which match the two clusters in our original set of prices.



Finally, to take care of cases where all prices were widely dispersed, I compared the kernel density estimate of $latex x _ {min}$ to the average kernel density estimate over all prices in $latex X$:

$latex OutlierScore(x _ {min}) = frac{KDE(x _ {min})}{frac{1}{n}sum _ {x _ i in X} KDE(x _ i) },$

and flagged $latex x _ {min}$ if its outlier score fell below some threshold.


## Adding Sophistication with Local Comparisons


While the attempt above accounts for price dispersion in our outlier score by dividing against the average kernel density estimate of all prices, a better approach (e.g., in the case of bimodal distributions) would be to take the average only over points $latex N(x _ {min})$ near $latex x _ {min}$:
$latex OutlierScore(x _ {min}) = frac{KDE(x _ {min})}{frac{1}{|N(x _ {min})|}sum _ {x _ i in N(x _ {min})} KDE(x _ i) }.$

For example, I experimented both with taking the $latex m$ nearest neighbors of $latex x _ {min}$, and with performing a $latex k$-means clustering on the prices and taking the points in the same cluster as $latex x _ {min}$, where I estimated $latex k$ using the gap statistic and prediction strength tests.

Although this method didn't produce significantly better results than the method that ignored clusters in prices, perhaps due to the relative rarity of distinct price groups in small datasets, the method should be more robust as the number of online retailers and prices per item grows.
