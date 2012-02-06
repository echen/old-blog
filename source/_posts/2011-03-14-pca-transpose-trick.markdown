---
date: '2011-03-14 04:21:12'
layout: post
slug: pca-transpose-trick
status: publish
title: PCA Transpose Trick
comments: true
wordpress_id: '33'
categories:
- expository
tags:
- image recognition
- linear algebra
- machine learning
- pca
---

# A simpler eigenvector calculation
Suppose we want to perform PCA on an $m \times n$ observation matrix $A$, where each row is an observation and each column is a dimension of the observation. For example, in the context of [eigenfaces](http://en.wikipedia.org/wiki/Eigenface), each row may be an image and each column a pixel.

Let's suppose we have already normalized the columns of $A$ to have zero mean, so that to find the PCA of $A$, we need to compute the eigenvectors of the $n \times n$ covariance matrix $A^T A$.

It's often the case that $n >> m$ (i.e., we have many more dimensions than datapoints), so finding the eigenvectors of the large $n \times n$ matrix $A^T A$ is computationally difficult. How can we make this problem more tractable?

It turns out that the eigenvectors of $A^T A$ have a simple relationship with the eigenvectors of $A A^T$, so we can solve the simpler problem of finding the eigenvectors of the smaller $m \times m$ matrix $A A^T$ instead. More precisely, **if $v$ is an eigenvector of $A A^T$, then $A^Tv$ is an eigenvector of $A^T A$ with the same eigenvalue**.

# Proof
Here's a proof of the above fact. Let $v$ be an eigenvector of $A A^T$ with eigenvalue $\lambda$. Then

$(A A^T) v = \lambda v$

$A^T(A A^T v) = A^T(\lambda v)$

$(A^T A)(A^T v) = \lambda (A^T v)$

so $A^Tv$ is an eigenvector of $A^T A$, with eigenvalue $\lambda$. Thus, instead of finding the eigenvectors of $A^T A$ directly, we can instead find the eigenvectors of $A A^T$ and multiply these on the left by $A^T$.

# Pseudocode
To summarize, here's how to perform a PCA using this trick:

* Let $A$ be an $m \times n$ matrix with observations in rows and dimensions in the columns.
* From each column of $A$, subtract the column's mean, so that each column now has zero mean.
* We now need to find the eigenvectors of the covariance matrix $A^T A$. If $A A^T$ is a smaller matrix, it will be easier to find the eigenvectors $v$ of $A A^T$. Then $A^T v$ are the eigenvectors of $A^T A$.

I've put a simple PCA implementation of this transpose trick on [my Github account](https://github.com/echen/pca-transpose-trick).