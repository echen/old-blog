---
date: '2011-03-19 04:22:16'
layout: post
slug: counting-clusters
status: publish
title: Counting Clusters
wordpress_id: '37'
categories:
- expository
tags:
- clustering
- r
- statistics
---

Given a set of datapoints, we often want to know how many clusters the datapoints form. Two practical algorithms for determining the number of clusters are the gap statistic and the prediction strength.





# Gap Statistic





The gap statistic algorithm (from [Estimating the number of clusters in a data set via the gap statistic](http://www.stanford.edu/~hastie/Papers/gap.pdf)) works as follows.





For each i from 1 up to some maximum number of clusters:







  1. Run a k-means algorithm on the original dataset to find i clusters, and sum the distance of all points from their cluster mean. Call this sum the _dispersion_.



  2. Generate a set of reference datasets (of the same size as the original). One simple way of generating a reference dataset is to sample uniformly from the original dataset's bounding rectangle; a more sophisticated approach is take into account the original dataset's shape by sampling, say, from a rectangle formed from the original dataset's principal components.



  3. Calculate the dispersion of each of these reference datasets, and take their mean.



  4. Define the ith _gap_ by [log(mean dispersion of reference datasets) - log(dispersion of original dataset)].







Once we've calculated all the gaps (note that we can add confidence intervals as well; see the original paper for the formula), we can select the number of clusters to be the one that gives the maximum gap.





For example, here I've generated three Gaussian clusters:





[![Three Gaussian Clusters](https://github.com/echen/gap-statistic/raw/master/examples/3_clusters_2d.png)](https://github.com/echen/gap-statistic/raw/master/examples/3_clusters_2d.png)





And running the gap statistic algorithm, we see that it correctly detects the number of clusters to be three:





[![Gap Statistic on Three Gaussian Clusters](https://github.com/echen/gap-statistic/raw/master/examples/3_clusters_2d_gaps.png)](https://github.com/echen/gap-statistic/raw/master/examples/3_clusters_2d_gaps.png)





(For a sample R implementation of the gap statistic, see [here](https://github.com/echen/gap-statistic).)





# Prediction Strength





Another cluster-counting algorithm is the prediction strength algorithm (from [Cluster validation by prediction strength](http://www-stat.stanford.edu/~tibs/ftp/predstr.ps)). To run it, for each i from 1 up to some maximum number of clusters:







  1. Divide the dataset into two groups, a training set and a test set.



  2. Run a k-means algorithm on each set to find i clusters.



  3. For each _test_ cluster, count the proportion of pairs of points in that cluster that would remain in the same cluster, if each were assigned to its closest _training_ cluster mean.



  4. The minimum over these proportions is the prediction strength for i clusters.







Once we've calculated the prediction strength for each number of clusters, we select the number of clusters to be the maximum i such that the prediction strength for i is greater than some threshold. (The paper suggests 0.8 - 0.9 as a good threshold, and I've seen 0.8 work well in practice.)





Here's the prediction strength algorithm run on the same example above:





[![Prediction Strength on Three Gaussian Clusters](https://github.com/echen/prediction-strength/raw/master/examples/3_clusters_2d_ps.png)](https://github.com/echen/prediction-strength/raw/master/examples/3_clusters_2d_ps.png)





(Again, for a sample R implementation of the prediction strength, see [here](https://github.com/echen/prediction-strength).)





In practice, I tend to prefer using the gap statistic algorithm, since it's a little easier to code and it doesn't require selecting an arbitrary threshold like the prediction strength does. I've also found that it gives slightly better results (though the original prediction strength paper has the opposite finding).
