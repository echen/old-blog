---
date: '2011-03-14 04:21:12'
layout: post
slug: pca-transpose-trick
status: publish
title: PCA Transpose Trick
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





Suppose we want to perform PCA on an $latex m \times n$ observation matrix $latex A$, where each row is an observation and each column is a dimension of the observation. For example, in the context of [eigenfaces](http://en.wikipedia.org/wiki/Eigenface), each row may be an image and each column a pixel.





Let's suppose we have already normalized the columns of $latex A$ to have zero mean, so that to find the PCA of $latex A$, we need to compute the eigenvectors of the $latex n \times n$ covariance matrix $latex A ^ T A$.





It's often the case that $latex n >> m$ (i.e., we have many more dimensions than datapoints), so finding the eigenvectors of the large $latex n \times n$ matrix $latex A ^ T A$ is computationally difficult. How can we make this problem more tractable?





It turns out that the eigenvectors of $latex A ^ T A$ have a simple relationship with the eigenvectors of $latex A A ^ T$, so we can solve the simpler problem of finding the eigenvectors of the smaller $latex m \times m$ matrix $latex A A ^ T$ instead. More precisely, **if $latex v$ is an eigenvector of $latex A A ^ T$, then $latex A ^ Tv$ is an eigenvector of $latex A ^ T A$ with the same eigenvalue**.





# Proof





Here's a proof of the above fact. Let $latex v$ be an eigenvector of $latex A A ^ T$ with eigenvalue $latex \lambda$. Then





$latex (A A ^ T) v = \lambda v$





$latex A ^ T(A A ^ T v) = A ^ T(\lambda v)$





$latex (A ^ T A)(A ^ T v) = \lambda (A ^ T v)$





so $latex A ^ Tv$ is an eigenvector of $latex A ^ T A$, with eigenvalue $latex \lambda$. Thus, instead of finding the eigenvectors of $latex A ^ T A$ directly, we can instead find the eigenvectors of $latex A A ^ T$ and multiply these on the left by $latex A ^ T$.





# Pseudocode





To summarize, here's how to perform a PCA using this trick:







  * Let $latex A$ be an $latex m \times n$ matrix with observations in rows and dimensions in the columns.


  * From each column of $latex A$, subtract the column's mean, so that each column now has zero mean.


  * We now need to find the eigenvectors of the covariance matrix $latex A ^ T A$. If $latex A A ^ T$ is a smaller matrix, it will be easier to find the eigenvectors $latex v$ of $latex A A ^ T$. Then $latex A ^ T v$ are the eigenvectors of $latex A ^ T A$.


