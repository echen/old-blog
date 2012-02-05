---
date: '2011-03-14 04:21:52'
layout: post
slug: summary-factorization-meets-the-neighborhood
status: publish
title: 'Netflix Prize Summary: Factorization Meets the Neighborhood'
wordpress_id: '35'
categories:
- expository
tags:
- collaborative filtering
- machine learning
- netflix prize
- recommendation systems
---

(Way back when, I went through all the Netflix prize papers. I'm now (very slowly) trying to clean up my notes and put them online. Eventually, I hope to have a more integrated tutorial, but here's a rough draft for now.)





This is a summary of Koren's 2008 [Factorization Meets the Neighborhood: a Multifaceted Collaborative Filtering Model](public.research.att.com/~volinsky/netflix/kdd08koren.pdf).





There are two approaches to collaborative filtering: neighborhood methods and latent factor models.







  * Neighborhood models are most effective at detecting very localized relationships (e.g., that people who like X-Men also like Spiderman), but poor at detecting a user's overall signals.


  * Latent factor models are best at estimating overall structure (e.g., that a user likes horror movies), but are poor at detecting strong associations among small sets of closely related items.






Since the two approaches have complementary strengths and weaknesses, we should integrate the two; this integration is the focus of this paper.





# Preliminaries





As mentioned in previous papers, we should normalize out common effects from movies. Throughout the rest of this paper, Koren uses a baseline estimate of overall rating mean + user deviation from average + movie deviation from average for the rating of user i on movie i; estimation of the latter two parameters are done by solving a regularized least squares problem.





Koren then describes using a binary matrix (1 for rated, 0 for not rated) as a source of implicit feedback. This is useful because the mere fact that a user rated many science fiction movies (say) suggests that the user likes science fiction movies.





# A Neighborhood Model





Recall the previous paper, where we modeled each rating $latex r _ {ui}$ as





$latex r _ {ui} = b _ {ui}+ \sum _ {N \in N(i; u)} (r _ {uj} - b _ {uj}) w _ {ij},$





where $latex N(i; u)$ is the k items most similar to i among the items user u rated, and the $latex w _ {ij}$ are parameters to be learned by solving a regularized least squares problem.





This paper makes several enhancements to that model. First, we replace $latex N(i; u)$ with $latex R ^ k(i; u)$, the intersection of the k items most similar to i (among all items) intersected with the items user u rated. Also, we denote by $latex N ^ k(i; u)$ the intersection of the k items most similar to i with the items user u has provided implicit feedback for. This gives us





$latex r _ {ui} = b _ {ui} + \sum _ {j \in R ^ k(i; u)} (r _ {uj} - b _ {uj}) w _ {ij} + \sum _ {j \in N ^ k(i; u)} c _ {ij},$





where the $latex c _ {ij}$ are another set of parameters to learn.





Notice that by taking the intersection of the k items most similar to i with the items user u rated (giving perhaps a set of size less than k), rather than taking the k items most similar to i among the items user u rated, we let our model be influenced not only by what a user rates, but also by what a user does not rate. For example, if a user does not rate LOTR 1 or LOTR 2, his predicted rating for LOTR 3 is penalized.





This implies that our current model encourages greater deviations from baseline estimates for users that provided many ratings or plenty of implicit feedback. In other words, for well-modeled users with a lot of input, we are willing to predict quirkier and less common recommendations; users we have less information about, on the other hand, receive safer, baseline estimates.





Nonetheless, this dichotomy between power users and newbie users is perhaps overemphasized by our current model, so we moderate the dichotomy by modifying our model to be





$latex r _ {ui} = b _ {ui} + |R ^ k(i; u)| ^ {-0.5} \sum _ {j \in R ^ k(i; u)} (r _ {uj} - b _ {uj}) w _ {ij} + |N ^ k(i; u)| ^ {-0.5} \sum _ {j \in N ^ k(i; u)} c _ {ij}.$





Parameters are determined by solving a regularized least squares problem.





# Latent Factor Models Revisited





Typical SVD approaches are based on the following rule:





$latex r _ {ui} = b _ {ui} + p _ u ^ T q _ i,$





where $latex p _ u$ is a user-factors vector and $latex q _ i$ is an item-factors vector. We describe two enhancements.





## Asymmetric-SVD





One suggestion is to replace $latex p _ u$ with





$latex |R(u)| ^ {-0.5} + \sum _ {j \in R(u)} (r _ {uj} - b _ {uj}) x _ j + |N(u)| ^ {-0.5} \sum _ {j \in N(u)} y _ j,$





where $latex R(u)$ is the set of items user u has rated, and $latex N(u)$ is the set of items user u has provided implicit feedback for. In other words, this model represents users through the items they prefer, rather than expressing users in a latent feature space. This model has several advantages:







  * Asymmetric-SVD does not parameterize users, so we do not need to wait to retrain the model when a user comes in. Instead, we can handle new users as soon as they provide feedback.


  * Predictions are a direct function of past feedback, so we can easily explain predictions. (When using a pure latent feature solution, however, explainability is difficult.)






As usual, parameters are learned via a regularized least-squares minimization.





## SVD++





Another approach is to continue modeling users as latent features, while adding implicit feedback. Thus, we replace $latex p _ u$ with $latex p _ u + |N(u)| ^ {-0.5} \sum _ {j \in N(u)} y _ j$. While we lose the easily explainability and immediate feedback of the Asymmetric-SVD model, this approach is likely more accurate.





# An Integrated Model





An integrated model incorporating baseline estimates, the neighborhood approach, and the latent factor approach is as follows:





$latex r _ {ui} = \left[\mu + b _ u + b _ i\right] +\left[q _ i ^ T \big(p _ u + \sqrt{|N(u)|}\sum _ {j \in N(u)} y _ j \big)\right] + \left[\sqrt{|R ^ k(i;u)} \sum _ {j \in R ^ k(i; u)}(r _ {uj} - b _ {uj})w _ {ij}+\sqrt{|N ^ k(i;u)|} \sum _ {j \in N ^ k(i; u)} c _ {ij}\right].$





Note that we have used $latex (\mu + b _ u + b _ i)$ as our baseline estimate. We also used the SVD++ model, but we could use the Asymmetric-SVD model instead.





This rule provides a 3-tier model for recommendations:







  * The first baseline group describes general properties of the item and user. For example, it may say that "The Sixth Sense" movie is known to be a good movie in general, and that Joe rates like the average user.


  * The next latent factor group may say that since "The Sixth Sense" and Joe rate high on the Psychological Thrillers Scale, Joe may like The Sixth Sense because he likes this genre of movies in general.


  * The final neighborhood tier makes fine-grained adjustments that are hard to file, such as the fact that Joe rated low the movie "Signs", a similar psychological thriller by the same director.






As usual, model parameters are determined by minimizing the regularized squared error function through gradient descent.
