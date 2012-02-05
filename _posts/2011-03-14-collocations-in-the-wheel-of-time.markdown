---
date: '2011-03-14 04:19:36'
layout: post
slug: collocations-in-the-wheel-of-time
status: trash
title: Collocations in the Wheel of Time
wordpress_id: '29'
categories:
- projects
tags:
- nlp
- wheel of time
---

I went yesterday to a talk on the use of collocations in information retrieval, so I decided to try generating some collocations of my own. I've had a digital copy of the Wheel of Time idling around my computer for a while, so I used that as my dataset.





# What is a collocation?





A collocation is basically a set of words that occur together more often than chance, particularly when the meaning of the phrase they form has some degree of non-compositionality. For example, "green frog" isn't a collocation (it simply means, well, a frog that is green), while phrases like "New York", "make a decision", and "ice cream" are.





# Collocation Algorithm





Surprisingly, the stupid-simple algorithm of taking the top N bigrams without stopwords works fairly well.




    
    
    collocation     count
    aes sedai       535
    dark one        196
    two rivers      186
    emonds field    152
    tar valon       150
    dont know       92
    one power       63
    master gill     63
    common room     61
    rand thought    59
    false dragon    55
    moiraine sedai  55
    green man       54
    rand looked     47
    deep breath     47
    looked around   45
    one hand        44
    fal dara        43
    shadar logoth   43
    dark ones       41
    even more       40
    aes sedais      39
    thom merrilin   37
    first time      37
    one another     36
    






 




As we can see in the above table, phrases like "aes sedai", "dark one", and "two rivers" are highly ranked collocations, as they should be.





However, there are a couple false positives and poor rankings: "dont know" and "rand thought" aren't really collocations, and while "common room" is a collocation, it probably shouldn't be ranked higher than "shadar logoth". So let's see if we can do a little better.





# Ranking Collocations





One easy way of improving our collocations is to use a t-statistic to measure the strength of collocation.





(Note that using the t-statistic as a significance test to _find_ collocations is pretty useless, since almost all bigrams show significance at even obscenely low alpha levels (because language isn't random), but it could be used to _rank_ collocations.)




    
    
    collocation     count   t-statistic
    aes sedai       535     23.10211862394927
    dark one        196     13.860521362953332
    two rivers      186     13.615459778209466
    emonds field    152     12.323718154590404
    tar valon       150     12.244452473366913
    dont know       92      9.516646625330717
    master gill     63      7.930564321120657
    one power       63      7.854015842542644
    common room     61      7.803239461942459
    false dragon    55      7.413095406607586
    green man       54      7.315379491245222
    rand thought    59      7.313973672504267
    moiraine sedai  55      7.217000758676086
    deep breath     47      6.846741606876571
    looked around   45      6.593645173571997
    shadar logoth   43      6.556984737299105
    fal dara        43      6.556752559170743
    rand looked     47      6.452169813860899
    dark ones       41      6.385667051407403
    one hand        44      6.370313000597064
    aes sedais      39      6.233831744841447
    thom merrilin   37      6.075408500541748
    even more       40      6.04920369742659
    first time      37      5.991228217950062
    bel tine        35      5.915727507160708
    






However, ranking with the t-statistic doesn't appear to help much in this case. The reason might be that the t-statistic assumes a sample from a normal distribution, and our probabilities are too low for the normal approximation to kick in.





So let's instead use a chi-square statistic, which non-parametrically measures the deviation between our observed pair count and the expected null pair count. And here we do see an improvement in our collocations:



 
    
    
    collocation     count   t-statistic             chi-square-statistic / 1000
    shayol ghul     33      5.744257564397729       310.6960000000001
    shadar logoth   43      6.556984737299105       310.696
    tar valon       150     12.244452473366913      308.63741770798373
    bel tine        35      5.915727507160708       302.0645834523452
    dai shan        18      4.242504132149704       294.34263164315354
    lews therin     30      5.476925875837552       291.27562521808125
    aes sedai       535     23.10211862394927       258.5338408522448
    fal dara        43      6.556752559170743       247.39731703714295
    emonds field    152     12.323718154590404      230.60908878892494
    amyrlin seat    18      4.242244674325305       147.16231884576544
    cenn buie       24      4.898228520718306       125.04423333965258
    false dragon    55      7.413095406607586       108.46072265958233
    taren ferry     35      5.914487027562771       107.48605331880918
    true source     33      5.742973327787289       100.04535811321102
    two rivers      186     13.615459778209466      94.53034990989171
    womens circle   19      4.358127670566016       91.54402382607543
    mistress alys   22      4.689129771670375       71.04890022543866
    queens blessing 22      4.689123595619235       70.74665912266121
    master gill     63      7.930564321120657       66.67757296412702
    common room     61      7.803239461942459       61.20963448192468
    padan fain      19      4.357584935157578       57.20889364602492
    four kings      21      4.5806220400573965      45.61709876735164
    captain domon   20      4.470309309018544       45.36645244865389
    trolloc wars    23      4.792872111791751       35.13663301361639
    deep breath     47      6.846741606876571       34.10366973274088
    
