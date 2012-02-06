---
date: '2011-03-14 04:27:32'
layout: post
slug: hacker-news-analysis
status: publish
title: Hacker News Analysis
comments: true
wordpress_id: '55'
categories:
- projects
tags:
- hacker news
- r
---

I was playing around with the [Hacker News database](http://api.ihackernews.com/?db) [Ronnie Roller](http://ronnieroller.com/) made (thanks!), so I thought I'd post some of the things I looked at.

# Activity on the Site

My first question was how activity on the site has increased over time. I looked at number of posts, points on posts, comments on posts, and number of users.

## Posts
![Hacker News Posts by Month](http://dl.dropbox.com/u/10506/blog/hn-analysis/posts_by_month.png)

This looks like a strong linear fit, with an increase of 292 posts every month.

## Comments

For comments, I fit a quadratic regression:

![Hacker News Comments by Month](http://dl.dropbox.com/u/10506/blog/hn-analysis/comments_by_month.png)

## Points

A quadratic regression was also a better fit for points by month:

![Hacker News Points by Month](http://dl.dropbox.com/u/10506/blog/hn-analysis/points_by_month.png)

## Users

And again for the number of distinct users with a submission:

![Hacker News Users by Month](http://dl.dropbox.com/u/10506/blog/hn-analysis/users.png)

# Points and Comments

My next question was how points and comments related. Intuitively, posts with more points should have more comments, but it's nice to check (maybe really good posts are kind of boring, so don't lead to much discussion).

First, I plotted the points and comments of each individual post:

![All Points vs. Comments](http://dl.dropbox.com/u/10506/blog/hn-analysis/all_points_vs_comments.png)

As expected, there’s an overall positive correlation between points and comments. Interestingly, there are quite a few high-points posts with no comments.

The plot’s quite noisy, though, so let’s try cleaning it up a bit, by taking the median number of comments per points level (and removing posts at the higher end, where we have little data):

![Points vs. Median Comments](http://dl.dropbox.com/u/10506/blog/hn-analysis/points_vs_median_comments.png)

We see that posts with more points do tend to have more comments. Also, variance in number of comments is indicated by size and color, so (unsurprisingly) posts with more points have larger variance in their number of comments.

# Quality of Posts

Another question was whether the quality of posts has degraded over time. 

First, I computed a normalized "score" for each post, where a post's score is defined as the number of points divided by the number of distinct users who made a submission in the same month. (The denominator is a rough proxy for the number of active users, and the goal of the score is to provide a way to compare posts across time.)

While the median score has declined over time (as perhaps should be expected, since only a fixed number of items can reach the front page):

[![Median Score](http://dl.dropbox.com/u/10506/blog/hn-analysis/median-score.png)](http://dl.dropbox.com/u/10506/blog/hn-analysis/median-score.png)

the absolute *number* of quality posts, defined as posts with a score greater than the (admittedly arbitrarily chosen) threshold 0.01, has increased (until possibly a dip starting in 2010):

![Number of Quality Posts](http://dl.dropbox.com/u/10506/blog/hn-analysis/num_quality_posts2.png)

(Of course, without some further analysis, it's not clear how well this score measures quality of posts, so take these numbers with a grain of salt.)

# Company Trends

Also, I wanted to see how certain topics have trended over time, so I looked at how mentions of some of the big-name companies (Google, Facebook, Microsoft, Yahoo, Twitter, Apple) have changed. For each company, I plotted the percentage of posts with the company's name in the title, and also made a smoothed plot comparing all six at the end. Note that Microsoft and Yahoo seem to be trending slightly downward, and Apple seems to be trending upward.

![Mentions of Microsoft](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_microsoft.png)

![Mentions of Yahoo](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_yahoo.png)

![Mentions of Google](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_google.png)

![Mentions of Facebook](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_facebook.png)

![Mentions of Twitter](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_twitter.png)

![Mentions of Apple](http://dl.dropbox.com/u/10506/blog/hn-analysis/pct_apple.png)

![All Trends](http://dl.dropbox.com/u/10506/blog/hn-analysis/all_trends2.png)