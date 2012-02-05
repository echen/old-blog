---
date: '2011-05-05 00:09:17'
layout: post
slug: twss-building-a-thats-what-she-said-classifier
status: publish
title: 'TWSS: Building a That''s What She Said Classifier'
wordpress_id: '245'
categories:
- projects
tags:
- naive bayes
- nlp
- twss
---

There's been a [fun paper](www.cs.washington.edu/homes/brun/pubs/pubs/Kiddon11.pdf) on [That's What She Said](http://www.urbandictionary.com/define.php?term=that's%20what%20she%20said) identification making the rounds recently, so I spent some time over the weekend building my own classifier.





**tl;dr** A simple unigram Naive Bayes model works pretty well, with performance on the lines of 0.969 precision and 0.823 recall. There's a demo [here](http://twss-classifier.heroku.com/). I also ran the classifier over some fairy tale text.





# Naive Bayes Classifier





To start, I used a super simple Naive Bayes classifier, trained on unigrams (with add-one smoothing). (See the appendix at the end for details.)





### Unigram vs. Bigram Model





Here are the most predictive features, after training a Naive Bayes model with unigrams:




    
    <code>unigram         p(twss|unigram)
    pull            0.9724889822144924
    bigger          0.9614677503890157
    wet             0.959004244327654
    hard            0.9527628206878138
    stick           0.9505783678914388
    hole            0.9443870318715991
    oh              0.9432941279908561
    replied         0.943294127990856
    fast            0.943294127990856
    longer          0.9397415371025485
    </code>



  




Just to compare, here are some of the most predictive features in a bigram model (I added START and END tokens to the beginning and end of each sentence, in order to have some contextual features):




    
    <code>bigram          p(twss|bigram)
    it in           0.9801434151851175
    START wow       0.9705079286853889
    START oh        0.9473580156961879
    its too         0.9350522640444204
    pull out        0.9187779331523677
    too big         0.9187779331523677
    START man       0.9113755525471394
    hard END        0.9113755525471394
    put it          0.9071442285463515
    that thing      0.9024886021363793
    stick it        0.9024886021363793
    my god          0.9024886021363793
    go in           0.8916207044791409
    START ugh       0.8916207044791409
    make it         0.8916207044791409
    its so          0.8916207044791409
    </code>



  




Amusingly, sentences starting with _wow_, _oh_, and _ugh_, tend to be good candidates for TWSS sentences, as well as sentences containing _it's too_ and _it's so_.





Here's a precision-recall curve comparing the two models. We see that, on our datasets, a unigram classifier handily beats a bigram classifier:





[![Precision-Recall](http://dl.dropbox.com/u/10506/blog/twss/precision-recall.png)](http://dl.dropbox.com/u/10506/blog/twss/precision-recall.png)





# Faerie Tail





Although our classifier gives excellent performance on our test set, one question is how well it generalizes to other sources of data.





I didn't have another set of positive examples to draw from, but I took a set of fairy tales on Project Gutenberg to form a new batch of negative examples. On this new set of fairy tale sentences, the classifier misclassified only 81 out of 912 of the examples (assuming they should all be classified as "not TWSS"), which is a pretty low error rate of 8.89%.





What do these misclassifications look like? Here are some of the false positives it made:





### Aladdin







  * "The African magician carries it carefully wrapt up in his bosom," said the princess; "and this I can assure you, because he pulled it out before me, and showed it to me in triumph."


  * It is vanished; but I had no concern in its removal.


  * "My son," said he, "what a man you are to do such surprising things always in the twinkling of an eye!"


  * "Sire," replied Aladdin, "I have not the least reason to complain of your conduct, since you did nothing but what your duty required."


  * "With your leave, mother," replied Aladdin, "I shall now take care how I sell a lamp which may be so serviceable both to you and me."






[![http://dl.dropbox.com/u/10506/blog/twss/aladdin.png](http://dl.dropbox.com/u/10506/blog/twss/aladdin.png)](http://dl.dropbox.com/u/10506/blog/twss/aladdin.png)





### Hansel and Gretel







  * "Oh dear," he said, "do let me go and see the hunt; I cannot restrain myself."


  * When they awoke it was dark night, and poor Grethel began to cry, and said, "Oh, how shall we get out of the wood?" But Hansel comforted her.


  * "But remember," she said, "I must lock the cottage door against those huntsmen, so when you come back in the evening, and knock, I shall not admit you, unless you say, 'Dear little sister let me in.'






### Snow White







  * One was too long, another too short; so she tried them all till she came to the seventh, and that was so comfortable that she laid herself down, and was soon fast asleep.


  * "Oh yes, I will try," said Snow-white.






Note that a lot of these really are TWSS sentences! (Now we know where [those Disney artists](http://www.snopes.com/disney/films/mermaid.asp) got their inspiration.) So the classifier appears to generalize surprisingly well.





# A Demo





I created [a small Sinatra app](http://twss-classifier.heroku.com/) to play around with the classifier, and deployed it [here](http://twss-classifier.heroku.com/).



# Appendix: Details





### Datasets





To grab some TWSS examples, my first thought was to turn to [twitter](http://search.twitter.com/search?q=twss). However, the twitter data turned out to be incredibly noisy (lots of junk obscuring not terribly funny examples), so taking a cue from the K&B paper, I pulled data from three sources:







  * First, I scraped [twss stories](http://twssstories.com) for positive training data (sentences for which a TWSS response is appropriate). Since only the last part in quotes from each submission is truly relevant to being a TWSS, I kept the quote and threw away the rest of each submission.


  * Next, I scraped [Texts from Last Night](http://textsfromlastnight.com) and [FMyLife](http://www.fmylife.com) for negative training data. Since TWSS jokes are usually made in response to _sentences_ (the last sentence you say), I split each submission into sentences, and each sentence formed a single negative training example.






Finally, I normalized each sentence by converting to lowercase and removing any punctuation.





### The Algorithm





To train and test the classifier, I used the examples I gathered to form training and test sets, each consisting of:







  * 1000 positive examples from twss stories.


  * 500 negative examples from Texts from Last Night.


  * 500 negative examples from FMyLife.






### Performance of the Unigram Model





Since we want to optimize for precision (we hope the things we classify as TWSS sentences really are TWSS sentences) over recall (it's fine if we don't always respond TWSS to every TWSS sentence), let's use 0.99 probability as our threshold for classifying a sentence as TWSS. (This is equivalent to setting a low prior for the probability of being a TWSS.)





With this threshold, a unigram Naive Bayes classifier has the following performance on a test set:







  * True positives: 823


  * False negatives: 177


  * True negatives: 974


  * False positives: 26


  * Precision = 0.969


  * Recall = 0.823


