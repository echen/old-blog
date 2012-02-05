---
date: '2011-05-01 15:23:31'
layout: post
slug: eigensheep
status: publish
title: Eigensheep
wordpress_id: '41'
categories:
- projects
- visualizations
tags:
- image recognition
- mechanical turk
- pca
- r
---

Aaron Koblin's [Sheep Market](http://www.thesheepmarket.com/) visualization is an awesome use of Mechanical Turk. But it'd be even more awesome if the grid were _ordered_, so inspired by the use of [eigenfaces](http://en.wikipedia.org/wiki/Eigenface) in facial recognition, I decided to try projecting the sheep onto two dimensions.


# Principal Sheep Components


After screenshotting the first 50 sheep from the market and normalizing their size and color, here's what a PCA projection looks like ([click](http://dl.dropbox.com/u/10506/eigensheep.png) for a larger view):

[![Projected Sheep](http://dl.dropbox.com/u/10506/eigensheep.png)](http://dl.dropbox.com/u/10506/eigensheep.png)

Notice how the stroke widths get thicker as we move to the right (i.e., **the first principal component seems to measure the blackness of the sheep**), and the amount of wool on the sheep's body increases as we move up (i.e., **the second principal component seems to measure the wooliness of the sheep**).

It's also pretty neat how all the sheep with black heads and black legs (sheep 35, 16, 32, 31, and 19) get clumped together:

[![Projected Sheep, Black Heads/Legs Circled](http://dl.dropbox.com/u/10506/eigensheep-black-heads.png)](http://dl.dropbox.com/u/10506/eigensheep-black-heads.png)

And I think the sheep on the left (next to and inside the dense cluster) seem much more poorly drawn -- they look more like camels, dogs, unicorns, or bugs than actual sheep.
