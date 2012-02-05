---
date: '2011-06-27 17:19:42'
layout: post
slug: topic-modeling-the-sarah-palin-emails
status: publish
title: Topic Modeling the Sarah Palin Emails
wordpress_id: '336'
categories:
- projects
tags:
- latent dirichlet allocation
- lda
- nlp
- r
- sarah palin
- topic models
---

# LDA-based Email Browser





Earlier this month, several thousand emails from Sarah Palin's time as governor of Alaska were [released](http://sunlightlabs.com/blog/2011/sarahs-inbox/). The emails weren't organized in any fashion, though, so to make them easier to browse, I've been working on some topic modeling (in particular, using latent Dirichlet allocation) to separate the documents into different groups.





I threw up [a simple demo app](http://sarah-palin.heroku.com/) to view the organized documents [here](http://sarah-palin.heroku.com/).





# What is Latent Dirichlet Allocation?





Briefly, given a set of documents, LDA tries to learn the latent topics underlying the set. It represents each document as a mixture of topics (generated from a Dirichlet distribution), each of which emits words with a certain probability.





For example, given the sentence "I listened to Justin Bieber and Lady Gaga on the radio while driving around in my car", an LDA model might represent this sentence as 75% about music (a topic which, say, emits the words _Bieber_ with 10% probability, _Gaga_ with 5% probability, _radio_ with 1% probability, and so on) and 25% about cars (which might emit _driving_ with 15% probability and _cars_ with 10% probability).





If you're familiar with latent semantic analysis, you can think of LDA as a generative version.





(For a more in-depth explanation, I wrote an introduction to LDA [here](http://blog.echen.me/2011/08/22/introduction-to-latent-dirichlet-allocation/).)





# Sarah Palin Email Topics





Here's a sample of the topics learnt by the model, as well as the top words for each topic. (Names, of course, are based on my own interpretation.)







  * [**Wildlife/BP Corrosion**](http://sarah-palin.heroku.com/topics/24): game, fish, moose, wildlife, hunting, bears, polar, bear, subsistence, management, area, board, hunt, wolves, control, department, year, use, wolf, habitat, hunters, caribou, program, denby, fishing, …


  * [**Energy/Fuel/Oil/Mining**](http://sarah-palin.heroku.com/topics/0): energy, fuel, costs, oil, alaskans, prices, cost, nome, now, high, being, home, public, power, mine, crisis, price, resource, need, community, fairbanks, rebate, use, mining, villages, …


  * [**Trig/Family/Inspiration**](http://sarah-palin.heroku.com/topics/19): family, web, mail, god, son, from, congratulations, children, life, child, down, trig, baby, birth, love, you, syndrome, very, special, bless, old, husband, years, thank, best, …


  * [**Gas**](http://sarah-palin.heroku.com/topics/6): gas, oil, pipeline, agia, project, natural, north, producers, companies, tax, company, energy, development, slope, production, resources, line, gasline, transcanada, said, billion, plan, administration, million, industry, …


  * [**Education/Waste**](http://sarah-palin.heroku.com/topics/12): school, waste, education, students, schools, million, read, email, market, policy, student, year, high, news, states, program, first, report, business, management, bulletin, information, reports, 2008, quarter, …


  * [**Presidential Campaign/Elections**](http://sarah-palin.heroku.com/topics/15): mail, web, from, thank, you, box, mccain, sarah, very, good, great, john, hope, president, sincerely, wasilla, work, keep, make, add, family, republican, support, doing, p.o, …






Here's a sample email from the wildlife topic:





[![Wildlife Email](http://dl.dropbox.com/u/10506/blog/palin-browser/wildlife-email.png)](http://sarah-palin.heroku.com/emails/6719)





I also thought the classification for [this email](http://sarah-palin.heroku.com/emails/12900) was really neat: the LDA model labeled it as 10% in the [Presidential Campaign/Elections](http://sarah-palin.heroku.com/topics/15) topic and 90% in the [Wildlife](http://sarah-palin.heroku.com/topics/24) topic, and it's precisely a wildlife-based protest against Palin as a choice for VP:





[![Wildlife-VP Protest](http://dl.dropbox.com/u/10506/blog/palin-browser/wildlife-vp.png)](http://sarah-palin.heroku.com/emails/12900)





# Future Analysis





In a future post, I'll perhaps see if we can glean any interesting patterns from the email topics. For example, for a quick graph now, if we look at the percentage of emails in the [Trig/Family/Inspiration topic](http://sarah-palin.heroku.com/topics/19) across time, we see that there's a spike in April 2008 -- exactly (and unsurprisingly) the month in which Trig was born.





[![Trig](http://dl.dropbox.com/u/10506/blog/palin-browser/trig-topic.png)](http://dl.dropbox.com/u/10506/blog/palin-browser/trig-topic.png)
