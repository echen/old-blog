---
date: '2011-06-14 23:32:04'
layout: post
slug: spork-spoon-or-fork
status: publish
title: 'Spork: Spoon or Fork?'
wordpress_id: '318'
categories:
- projects
tags:
- image classification
- scikit-learn
- spork
- svm
- wall-e
---

There's an adorable scene in _WALL-E_ where, unable to decide whether a spork belongs with his spoon collection or fork collection, WALL-E places it in the middle.



[youtube=http://www.youtube.com/watch?v=ruJ76-o5lxU]

  




This led me to the following timeless question: is a spork more spoon or fork?





To answer, I did a little digging. First, I pulled images of spoons and forks from [Bing](http://www.bing.com/images) (natch) and used these to train a spoon-vs.-fork SVM (using the excellent [scikit-learn](http://scikit-learn.sourceforge.net/) package).





Using leave-one-out cross-validation, the classifier showed roughly 85% accuracy: 4 out of 20 spoons were misclassified as forks, and 2 out of 20 forks were misclassified as spoons. Not bad, considering the limited dataset and lack of tuning.





Finally, I applied the classifier to my spork images.





The results? 2 out of 20 sporks were classified as forks and the remaining 18 were classified as spoons, thereby definitively proving that **a spork is 10% fork and 90% spoon**.





[![Spork Decomposition](http://dl.dropbox.com/u/10506/blog/spork/spork-decomposition.png)](http://dl.dropbox.com/u/10506/blog/spork/spork-decomposition.png)
