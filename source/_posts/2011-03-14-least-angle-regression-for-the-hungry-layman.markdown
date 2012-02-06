---
date: '2011-03-14 04:27:10'
layout: post
slug: least-angle-regression-for-the-hungry-layman
status: publish
title: A Layman's Explanation of Least Angle Regression
comments: true
wordpress_id: '53'
categories:
- expository
tags:
- lasso regression
- least angle regression
- regularization
- statistics
- variable selection
---

(I wrote up a more mathematical explanation of least angle regression [here](/2011/04/21/a-mathematical-introduction-to-least-angle-regression/).)

Suppose you're at a buffet. You don't want to just grab everything and overeat (overfit), so how do you decide which dishes to take? Here are some possibilities.


# Forward Selection


On your first trip to the buffet, take a plateful of your favorite dish, bring it back, and eat it. On your second trip, take a plateful of the dish that _now_ looks most appetizing, bring it back, and eat it. And so on.

The problem with this method is the following: suppose your favorite food is spaghetti, followed closely by macaroni. Ideally, you'd like to take half a plate of spaghetti and slightly less than half a plate of macaroni, but under this method, you have to first take and eat a plateful of spaghetti, and now you're sick of pasta and don't want macaroni anymore.


# Forward Stagewise


To remedy the greediness of the above method, another option is to take smaller morsels at a time. On your first trip to the buffet, you take a thimbleful of your favorite dish; on your next trip to the buffet, you take a thimbleful of the currently most appetizing dish; and so on again.

Now, after getting your thimbleful of spaghetti, pasta still looks delicious to you, so you can get your thimbleful of macaroni as well.

The problem with this method is that because you're only eating a thimbleful at a time, you have to make many trips to the buffet and so dinner takes forever.


# Least Angle Regression


A much more efficient method works as follows. Suppose your favorite dishes are, in order, spaghetti, macaroni, salad, and chili. On your first trip, you grab a bunch of spaghetti. You know that as you eat spaghetti, you start to get slightly sick of it, so it becomes less and less appetizing, until eventually it becomes just as appetizing as macaroni (but still more appetizing than salad and chili). So only grab an amount X of spaghetti, so that after eating X, spaghetti and macaroni are equally appetizing.

On your second trip, spaghetti and macaroni are equally appetizing. Grab both spaghetti and macaroni, in proportions such that spaghetti and macaroni stay equally appetizing while you eat. Again, you know exactly how much spaghetti and macaroni you can eat until salad becomes just as appetizing, so only grab this amount.

On your third trip, spaghetti, macaroni, and salad look equally delicious. Again, grab the three foods in proportions that stay equally appetizing while you eat, and only grab enough to make chili look just as tasty.

And so on.

Note that:



	
  * This method works better than forward selection, because we get to eat both spaghetti and macaroni.

	
  * This method works much faster than forward stagewise, because we make much fewer trips. (If we want to eat $latex n$ dishes, we only need to make $latex n$ trips.)

	
  * We're always eating whatever looks most appetizing to us.




# Reversing the Analogy


Replace buffet with linear regression and dishes with variables, and you now have three tasty model selection methods to choose from.

For a more mathematical explanation of least angle regression, see [here](http://edchedch.wordpress.com/2011/04/21/a-mathematical-introduction-to-least-angle-regression/).
