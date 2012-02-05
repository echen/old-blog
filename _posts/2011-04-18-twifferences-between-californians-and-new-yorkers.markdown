---
date: '2011-04-18 03:41:39'
layout: post
slug: twifferences-between-californians-and-new-yorkers
status: publish
title: Twifferences Between Californians and New Yorkers
wordpress_id: '27'
categories:
- projects
tags:
- natural language processing
- nlp
- twitter
---

How do people in Silicon Valley compare to those in New York City? For a data-driven answer, I pulled a couple days' worth of Twitter data around the two areas.





## Silicon Valley vs. NYC





So let's take a look. To compare the two places, I trained a simple Naive Bayes model on user profiles. Here are the words most predictive of being from Silicon Valley vs. NYC:





### Silicon Valley




    
    <code>word                    Prob(Silicon Valley | word)
    cloud                   0.9053263586466359
    stanford                0.8947378473880241
    hacker                  0.8759014372329466
    dev                     0.8684686297323906
    giants                  0.8522440881548609
    mac                     0.8453052631578948
    support                 0.8453052631578948
    ux                      0.8453052631578948
    engineer                0.8321693229113796
    software                0.8223647630482606
    google                  0.8199372672025093
    yahoo                   0.8095254553623891
    ui                      0.7978356566397651
    board                   0.7978356566397651
    programmer              0.7978356566397651
    health                  0.7946855178965604
    game                    0.7846171884159925
    bike                    0.7846171884159925
    gadgets                 0.7846171884159925
    surfer                  0.7846171884159925
    lead                    0.7846171884159925
    green                   0.7758225129356634
    product                 0.7707827422373662
    engineering             0.7662790401791395
    data                    0.7662790401791395
    biz                     0.7522143788498717
    games                   0.7503363731499477
    cto                     0.7474653744372272
    startup                 0.7474653744372272
    cofounder               0.745373899785155 
    team                    0.7399904460289096
    mobile                  0.7395369397321055
    entrepreneur            0.7346495409451503
    before                  0.7320595099183198
    corporate               0.7320595099183198
    companies               0.7320595099183198
    enterprise              0.7320595099183198
    careers                 0.7320595099183197
    help                    0.7320595099183197
    jobs                    0.7226147417213892
    systems                 0.7183120188916491
    dude                    0.7183120188916491
    solutions               0.7146518581802648
    startups                0.7146518581802648
    instructor              0.7146518581802648
    founder                 0.7136727946906866
    advocate                0.7119786767011602
    community               0.7107516339869281
    local                   0.7083355385022493
    cyclist                 0.7083355385022493
    formerly                0.7083355385022493
    tech                    0.7034995094145681
    dad                     0.699465571148113 
    developer               0.6933557437157872
    evangelist              0.6886440677966102
    architect               0.6886440677966102
    experience              0.6875894616006009
    designer                0.6861009534875773
    app                     0.6861009534875773
    gamer                   0.6701428216249068
    geek                    0.6699839438296025
    friend                  0.6692937011181566
    married                 0.6692937011181566
    past                    0.6670653907496013
    yoga                    0.6670653907496013
    baseball                0.6670653907496013
    iphone                  0.65665476702241  
    guy                     0.6396064208138196
    running                 0.6323876017254413
    </code>



  




### New York City




    
    <code>word                    Prob(New York | word)
    bbm                     0.9235374771480804
    mets                    0.9165294616574365
    teamfollowback          0.9165294616574365
    nyu                     0.9165294616574365
    columbia                0.8848747591522158
    actress                 0.8682158330051202
    chick                   0.845920058942715 
    theatre                 0.8010386109569492
    money                   0.7935205183585313
    publishing              0.7854119457864808
    moment                  0.7854119457864808
    self                    0.7854119457864808
    ya                      0.7545697268432944
    intern                  0.7545697268432944
    makeup                  0.7512175173798283
    financial               0.7512175173798283
    studio                  0.7329822041337483
    records                 0.7329822041337483
    magazine                0.7272706101537029
    history                 0.7249169653720938
    fashion                 0.718105290117341 
    myself                  0.7118622174381054
    soul                    0.7072308553828924
    peace                   0.7072308553828924
    dancer                  0.7017521519889981
    night                   0.687114269683935 
    president               0.6871142696839349
    event                   0.6577157178660937
    dreams                  0.6577157178660937
    model                   0.6577157178660937
    read                    0.6577157178660937
    journalism              0.6577157178660937
    filmmaker               0.6530588061027995
    news                    0.6466488313151225
    mother                  0.6466488313151224
    entertainment           0.6466488313151224
    party                   0.640842613712599 
    political               0.640842613712599 
    producer                0.6372663804691904
    communications          0.6222197132211811
    actor                   0.6169228655604573
    journalist              0.616094753936313 
    website                 0.6133083363295495
    radio                   0.6133083363295495
    executive               0.6058707124010555
    </code>



  




Some findings:







  * Silicon Valley is much more **tech**- (_cloud, hacker, dev, engineer, software, programmer_) and **startup**-driven (_startup, entrepreneur, founder_). New York is much more into **arts/entertainment** (_actress, theatre, publishing, studio, records, magazine, journalism, filmmaker, news_) and **finance** (_money, financial_). (Another way to look at it: Silicon Valley higher-ups call themselves _ctos_ and _founders_ and sit on _boards_, while New York higher-ups call themselves _presidents_ and _executives_.)


  * New Yorkers care a lot about **looks** (_makeup, fashion_). Silicon Valley folks care a lot about **sports**, **health**, and the **outdoors** (_bike, surfer, cyclist, yoga, running, health_).


  * Silicon Valley folks describe themselves through their **past** (_before, formerly, past, former_). New Yorkers describe themselves through their **future** (_dreams_).


  * Silicon Valley is big on **community** (_support, team, help, helping, community_). New York is focused on the **individual** (_self, myself_).


  * Silicon Valley has a larger proportion of **men** (_dad, geek, dude, guy_). New York has the **women** (_mother, chick_).


  * New York uses BlackBerrys (_bbm_ is short for BlackBerry Messenger), while Silicon Valley uses _iPhones_.


  * Silicon Valley is more into the **locavore** movement (_green, local_).


