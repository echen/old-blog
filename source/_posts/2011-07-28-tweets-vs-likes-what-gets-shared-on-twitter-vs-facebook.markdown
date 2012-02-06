---
date: '2011-07-28 07:55:29'
layout: post
slug: tweets-vs-likes-what-gets-shared-on-twitter-vs-facebook
status: publish
title: 'Tweets vs. Likes: What gets shared on Twitter vs. Facebook?'
comments: true
wordpress_id: '423'
tags:
- facebook
- flowingdata
- likes
- new scientist
- r
- social networks
- twitter
- xkcd
---

It always strikes me as curious that some posts get a lot of love on Twitter, while others get many more shares on Facebook:

[![Twitter Beats FB](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/twitter-beats-fb.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/twitter-beats-fb.png)

[![FB Beats Twitter](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/fb-beats-twitter.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/fb-beats-twitter.png)

What accounts for this difference? Some of it is surely site-dependent: maybe one blogger has a Facebook page but not a Twitter account, while another has these roles reversed. But even on sites maintained by a single author, tweet-to-likes ratios can vary widely from post to post.

So what kinds of articles tend to be more popular on Twitter, and which spread more easily on Facebook? To take a stab at an answer, I scraped data from a couple of websites over the weekend.

**tl;dr** Twitter is still for the *techies*: articles where the number of tweets greatly outnumber FB likes tend to revolve around software companies and programming. Facebook, on the other hand, appeals to *everyone else*: yeah, to the masses, and to non-software technical folks in general as well.

# FlowingData

The first site I looked at was Nathan Yau's awesome [FlowingData](http://www.flowingdata.com) website on data visualization. To see which articles are more popular on Facebook and which are more popular on Twitter, let's sort all the FlowingData articles by their # tweets / # likes ratio.

Here are the 10 posts with the lowest tweets-to-likes ratio (i.e., the posts that were especially popular with Facebook users):

[![FlowingData Facebook](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-facebook2-small.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-facebook2.png)

* [What your state is the worst at – United States of shame](http://flowingdata.com/2011/01/30/what-your-state-is-the-worst-at-united-states-of-shame/)
* [Plush statistical distribution pillows](http://flowingdata.com/2011/05/13/plush-statistical-distribution-pillows/)
* [Are gas prices really that high?](http://flowingdata.com/2011/03/22/are-gas-prices-really-that-high/)
* [Hey Jude flowchart](http://flowingdata.com/2011/01/21/hey-jude-flowchart/)
* [Women’s dress sizes demystified](http://flowingdata.com/2011/04/28/womens-dress-sizes-demystified/)
* [America is not the best at everything](http://flowingdata.com/2011/02/22/america-is-not-the-best-at-everything/)
* [What you need to get together](http://flowingdata.com/2011/06/10/what-you-need-to-get-together/)
* [Dexter’s victims through season five](http://flowingdata.com/2011/01/27/dexters-victims-through-season-five/)
* [Correlating dog](http://flowingdata.com/2011/05/06/correlating-dog/)
* [Valentine’s Day importance](http://flowingdata.com/2011/02/14/valentines-day-importance/)

And here are the 10 posts with the highest tweets-to-like ratio (i.e., the posts especially popular with Twitter users):

[![FlowingData Twitter](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-twitter-small.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-twitter.png)

* [Delicious mass exodus](http://flowingdata.com/2011/01/04/delicious-mass-exodus/)
* [Pew Research raw survey data now available](http://flowingdata.com/2011/05/25/pew-research-raw-survey-data-now-available/)
* [Stock market predictions with Twitter](http://flowingdata.com/2011/02/03/stock-market-predictions-with-twitter/)
* [Growth and usage of foursquare in 2010](http://flowingdata.com/2011/01/25/growth-and-usage-of-foursquare-in-2010/)
* [Sunlight Labs opens up Real Time Congress API](http://flowingdata.com/2011/02/17/sunlight-labs-opens-up-real-time-congress-api/)
* [Open-source Data Science Toolkit](http://flowingdata.com/2011/03/25/open-source-data-science-toolkit/)
* [Explore your LinkedIn network visually with InMaps](http://flowingdata.com/2011/01/24/explore-your-linkedin-network-visually-with-inmaps/)
* [Perceived vs. actual country rankings](http://flowingdata.com/2011/05/03/perceived-vs-actual-country-rankings/)
* [See what you and others tweet about with the Topic Explorer](http://flowingdata.com/2011/04/20/see-what-you-and-others-tweet-about-with-the-topic-explorer/)
* [History of detainees at Guantánamo](http://flowingdata.com/2011/04/24/history-of-detainees-at-guantnamo/)

Notice any differences between the two?

* Instant gratification infographics, cuteness, comics, and pop culture get liked on Facebook.
* APIs, datasets, visualizations related to techie sites (Delicious, foursquare, Twitter, LinkedIn), and picture-less articles get tweeted instead.

Interestingly, it also looks like the colors in the top 10 Facebook articles tend to the red end of the spectrum, while the colors in the top 10 Twitter articles tend to the blue end of the spectrum. Does this pattern hold if we look at more data? Here's a meta-visualization of the FlowingData articles, sorted by articles popular on Facebook in the top left to articles popular on Twitter in the bottom right (see [here](http://flowingdata-melted.heroku.com/) for some interactivity and more details):

[![FlowingData MetaViz](http://dl.dropbox.com/u/10506/blog/flowingdata-metaviz/flowingdata-metaviz.png)](http://flowingdata-melted.heroku.com/)

It does indeed look like the images at the top (the articles popular on Facebook) are more pink, while the images at the bottom (the articles popular on Twitter) are more blue (though it would be nice to quantify this in some way)!

Furthermore, we can easily see from the grid that articles with no visualizations (represented by lorem ipsum text in the grid) cluster at the bottom. Grabbing some actual numbers, we find that 32% of articles with at least one picture have more shares on Facebook than on Twitter, compared to only 4% of articles with no picture at all.

[![Effect of a visualization](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-viz-effect.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-viz-effect.png)

Finally, let's break down the percentage of articles with more Facebook shares by category.

[![FlowingData Categories](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-categories.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-categories.png)

(I filtered the categories so that each category in the plot above contains at least 5 articles.)

What do we find?

* Articles in the Software, Online Applications, News, and Data sources categories (yawn) get 100% of their shares from Twitter.
* Articles tagged with [Data Underload](http://flowingdata.com/category/projects/data-underload/) (which seems to contain short and sweet visualizations of everyday things), [Miscellaneous](http://flowingdata.com/category/miscellaneous-data/) (which contains lots of comics or comic-like visualizations), and [Infographics](http://flowingdata.com/category/visualization/infographics/) get the most shares on Facebook. 
* This category breakdown matches precisely what we saw in the top 10 examples above.

# New Scientist

When looking at FlowingData, we saw that Twitter users are much bigger on sharing technical articles. But is this true for technical articles in general, or only for programming-related posts? (In my experience with Twitter, I haven't seen many people from math and the non-computer sciences.)

To answer, I took articles from the [Physics & Math](http://www.newscientist.com/search?rbsection1=Physics+%26+Math&sortby=rbpubdate) and [Technology](http://www.newscientist.com/search?rbsection1=tech&sortby=rbpubdate) sections of [New Scientist](http://www.newscientist.com), and

* Calculated the percentage of shares each article received on Twitter (i.e., # tweets / (# tweets + # likes)).
* Grouped articles by their number of tweets rounded to the nearest multiple of 25 (bin #1 contains articles close to 25 tweets, bin #2 contains articles close to 50 tweets, etc.).
* Calculated the median percentage of shares on Twitter for each bin.

Here's a graph of the result:

[![Technology vs. Physics & Math](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/tech_vs_physicsmath.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/tech_vs_physicsmath.png)

Notice that:

* The technology articles get consistently more shares from Twitter than the physics and math articles do. 
* Twitter accounts for the majority of the technology shares.
* Facebook accounts for the majority of the physics and math shares. 

So this suggests that Twitter really is for computer technology in particular, not technical matters in general (though it would be nice to look at areas other than physics and math as well).

# Quora

To get some additional evidence on the computer science vs. math/physics divide, I 

* Scraped about 350 profiles of followers from each of the Computer Science, Software Engineering, Mathematics, and Physics categories on Quora;
* Checked each user to see whether they link to their Facebook and Twitter accounts on their profile. 

Here's the ratio of the number of people linking to their Facebook account to the number of people linking to their Twitter account, sliced by topic:

[![Math/Physics vs. CS/Software](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/math-physics-vs-cs-software.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/math-physics-vs-cs-software.png)

[![Math/Physics vs. CS/Software, Collapsed](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/math-physics-vs-cs-software-collapsed.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/math-physics-vs-cs-software-collapsed.png)

We find exactly what we expect from the New Scientist data: people following the math and physics categories have noticeably smaller Twitter / Facebook ratios compared to people following the computer science and software engineering categories (i.e., compared to computer scientists and software engineers, mathematicians and physicists are more likely to be on Facebook than on Twitter). What's more, this difference is in fact significant: the graphs display individual 90% confidence intervals (which overlap not at all or only slightly), and we do indeed get significance at the 95% level if we look at the differences between categories.

This corroborates the New Scientist evidence that Twitter gets the computer technology shares, while Facebook gets the math and physics shares.

# XKCD

Finally, let's take a look at which XKCD comics are especially popular on Facebook vs. Twitter.

Here are the 10 comics with the highest likes-to-tweets ratio (i.e., the comics especially popular on Facebook):

[![XKCD Facebook](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/xkcd-facebook-small.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/xkcd-facebook.png)

* [Dental Nerve](http://xkcd.com/846/)
* [Wisdom Teeth](http://xkcd.com/861/)
* [Trapped](http://xkcd.com/876/)
* [Complex Conjugate](http://xkcd.com/849/)
* [Learning to Cook](http://xkcd.com/854/)
* [Serious](http://xkcd.com/840/)
* [Explorers](http://xkcd.com/839/)
* [Mu](http://xkcd.com/815/)
* [Los Alamos](http://xkcd.com/809/)
* [Magic School Bus](http://xkcd.com/911/)

Here are the 10 comics with the highest tweets-to-likes ratio (i.e., the comics especially popular on Twitter):

[![XKCD Twitter](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/xkcd-twitter-small.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/xkcd-twitter.png)

* [Server Attention Span](http://xkcd.com/869/)
* [Illness](http://xkcd.com/818/)
* [Nanobots](http://xkcd.com/865/)
* [Manual Override](http://xkcd.com/912/)
* [The Cloud](http://xkcd.com/908/)
* [Constructive](http://xkcd.com/810/)
* [Future Timeline](http://xkcd.com/887/)
* [Good Code](http://xkcd.com/844/)
* [Golden Hammer](http://xkcd.com/801/)
* [Advertising Discovery](http://xkcd.com/906/)
* [Online Communities 2](http://xkcd.com/802/)

Note that the XKCD comics popular on Facebook have more of a layman flavor, while the XKCD comics popular on Twitter are much more programming-related:

* Of the XKCD comics popular on Twitter, one's about server attention spans, another's about IPv6 addresses, a third is about GNU info pages, another deals with cloud computing, a fifth talks about Java, and the last is about a bunch of techie sites. (This is just like what we saw with the FlowingData visualizations.) 
* Facebook, on the other hand, gets Ke$ha and Magic School Bus.
* And while both top 10's contain a flowchart, the one popular on FB is about *cooking*, while the one popular on Twitter is about *code*!
* What's more, if we look at the few technical-ish comics that are more popular on Facebook (the complex conjugate, mu, and Los Alamos comics), we see that they're about physics and math, not programming (which matches our findings from the New Scientist articles).

# Lesson

So why should you care? Here's one takeaway: 

* If you're blogging about technology, programming, and computer science, Twitter is your friend.
* But if you're blogging about anything else, be it math/physics or pop culture, don't rely on a Twitter account alone; your shares are more likely to propagate on Facebook, so make sure to have a Facebook page as well.

# What's Next?

The three websites I looked at are all fairly tech-oriented, so it would be nice to gather data from other kinds of websites as well.

And now that we have an idea how Twitter and Facebook compare, the next burning question is surely: [what do people share on Google+?!](http://finalbossform.com/post/7214184180/google-is-fast-becoming-the-leading-social)

# Addendum

Let's consider the following thought experiment. Suppose you come across the most unpopular article ever written. What will its FB vs. Twitter shares look like? Although no *real* person will ever share this article, I think Twitter has many more spambots (who tweet out any and every link) than FB does, so maybe unpopular articles will have more tweets than likes by default. Conversely, suppose you come across the most popular article ever written, which everybody wants to share. Then since FB has many more users than Twitter does, maybe popular articles will tend to have more likes than tweets anyways.

Thus, in order to find out which types of articles are *especially* popular on FB vs. Twitter, instead of looking at tweets-to-likes ratios directly, we could try to remove this baseline popularity effect. (Taking ratios instead of raw number of tweets or raw number of likes is one kind of normalization; this is another.)

So does this scenario (or something similar to it) actually play out in practice?

[![Overall Popularity vs. Facebook](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-overall-popularity-vs-fb.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-overall-popularity-vs-fb.png)

Here I've plotted the overall popularity of a post (the total number of shares it received on either Twitter or FB) against the percentage of shares on Facebook alone, and we can see that as a post's popularity grows, more and more shares do indeed tend to come from Facebook rather than Twitter.

Also, see the posts at the lower end of the popularity scale that are only getting shares on Twitter? Let's take a look at the five most unpopular of these:

* [Flowing Data is brought to you by... (March 2011 edition)](http://flowingdata.com/2011/03/31/flowingdata-is-brought-to-you-by-8/) (11 tweets, 0 likes)
* [Flowing Data is brought to you by... (July 2011 edition)](http://flowingdata.com/2011/07/05/flowingdata-is-brought-to-you-by-11/) (14 tweets, 0 likes)
* [Flowing Data is brought to you by... (June 2011 edition)](http://flowingdata.com/2011/06/06/flowingdata-is-brought-to-you-by-10/) (17 tweets, 0 likes)
* [Flowing Data is brought to you by... (May 2011 edition)](http://flowingdata.com/2011/05/09/flowingdata-is-brought-to-you-by-9/) (18 tweets, 0 likes)
* [Flowing Data is brought to you by... (May 2011 edition)](http://flowingdata.com/2011/02/28/flowingdata-is-brought-to-you-by-7/) (12 tweets, 1 like)

Notice that they're all shoutouts to FlowingData's sponsors! There's pretty much no reason any *real* person would share these on Twitter or Facebook, and indeed, checking Twitter to see who actually tweeted out these links, we see that the tweeters are bots:

* [https://twitter.com/#!/myVisualization/status/77685824224894976](https://twitter.com/#!/myVisualization/status/77685824224894976)
* [https://twitter.com/#!/InfographicTwts/status/6766861514245734](https://twitter.com/#!/InfographicTwts/status/67668615142457344
)
* [https://twitter.com/#!/guysgoogle/status/77644902510493696](https://twitter.com/#!/guysgoogle/status/77644902510493696)
* [https://twitter.com/#!/WhereIsYourData/status/77631743292735488](https://twitter.com/#!/WhereIsYourData/status/77631743292735488)

Now let's switch to a slightly different view of the above scenario, where I plot number of tweets against number of likes:

[![FlowingData Tweets vs. Likes](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-tweets-vs-likes.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/flowingdata-tweets-vs-likes.png)

We see that as popularity on Twitter increases, so too does popularity on Facebook -- but at a slightly faster rate. (The form of the blue line plotted is roughly $\log(likes) = -3.87 + 1.70 \log(tweets)$.)

So instead of looking at the ratios above, to figure out which articles are popular on FB vs. Twitter, we could look at the residuals of the above plot. Posts with large positive residuals would be posts that are especially popular on FB, and posts with negative residuals would be posts that are especially popular on Twitter.

In practice, however, there wasn't much difference between looking at residuals vs. ratios directly when using the datasets I had, so to keep things simple in the main discussion above, I stuck to ratios alone. Still, it's another option which might be useful when looking at different questions or different sources of data, so just for completeness, here's what the FlowingData results look like if we use residuals instead.

The 10 articles with the highest residuals (i.e., the articles most popular on Facebook):

* [What you need to get together](http://flowingdata.com/2011/06/10/what-you-need-to-get-together/)
* [Valentine’s Day importance](http://flowingdata.com/2011/02/14/valentines-day-importance/)
* [What your state is the worst at – United States of shame](http://flowingdata.com/2011/01/30/what-your-state-is-the-worst-at-united-states-of-shame/)
* [Plush statistical distribution pillows](http://flowingdata.com/2011/05/13/plush-statistical-distribution-pillows/)
* [Hitler learns topology](http://flowingdata.com/2011/07/01/hitler-learns-topology/)
* [Dexter’s victims through season five](http://flowingdata.com/2011/01/27/dexters-victims-through-season-five/)
* [Access to education where you live](http://flowingdata.com/2011/07/06/access-to-education-where-you-live/)
* [Watching the growth of Costco warehouses](http://flowingdata.com/2011/03/09/watching-costco-warehouses-open-nationwide/)
* [Are gas prices really that high?](http://flowingdata.com/2011/03/22/are-gas-prices-really-that-high/)
* [Flight safety-esque beer pong guide](http://flowingdata.com/2011/01/21/flight-safety-esque-beer-pong-guide/)

The 10 articles with the lowest residuals (i.e., the articles most popular on Twitter):

* [Pew Research raw survey data now available](http://flowingdata.com/2011/05/25/pew-research-raw-survey-data-now-available/)
* [Explore your LinkedIn network visually with InMaps](http://flowingdata.com/2011/01/24/explore-your-linkedin-network-visually-with-inmaps/)
* [Stock market predictions with Twitter](http://flowingdata.com/2011/02/03/stock-market-predictions-with-twitter/)
* [Delicious mass exodus](http://flowingdata.com/2011/01/04/delicious-mass-exodus/)
* [Open-source Data Science Toolkit](http://flowingdata.com/2011/03/25/open-source-data-science-toolkit/)
* [Business intelligence vs. infotainment](http://flowingdata.com/2011/04/17/business-intelligence-vs-infotainment/)
* [See what you and others tweet about with the Topic Explorer](http://flowingdata.com/2011/04/20/see-what-you-and-others-tweet-about-with-the-topic-explorer/)
* [Growth and usage of foursquare in 2010](http://flowingdata.com/2011/01/25/growth-and-usage-of-foursquare-in-2010/)
* [Flash vs. HTML5](http://flowingdata.com/2011/05/10/flash-vs-html5/)
* [Gender and time comparisons on Twitter](http://flowingdata.com/2011/06/09/gender-and-time-comparisons-on-twitter/)

Here's a density plot of article residuals, split by whether the article has a visualization or not (residuals of picture-free articles are clearly shifted towards the negative end):

[![Residuals](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/has-viz-residuals.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/has-viz-residuals.png)

Here are the mean residuals per category (again, we see that the miscellaneous, data underload, data art, and infographics categories tend to be more popular on Facebook, while the data sources, software, online applications, and news categories tend to be more popular on Twitter):

[![Category Residuals](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/category-residuals.png)](http://dl.dropbox.com/u/10506/blog/likes-vs-tweets/category-residuals.png)

And that's it! In the spirit of these findings, I hope this article gets [liked](http://blog.echen.me/2011/07/28/tweets-vs-likes-what-gets-shared-on-twitter-vs-facebook/?share=facebook&nb=1) a little and [tweeted](https://twitter.com/share?original_referer=http%3A%2F%2Fblog.echen.me%2F2011%2F07%2F28%2Ftweets-vs-likes-what-gets-shared-on-twitter-vs-facebook%2F&source=tweetbutton&text=Tweets%20vs.%20Likes%3A%20What%20gets%20shared%20on%20Twitter%20vs.%20Facebook%3F%3A&url=http%3A%2F%2Fwp.me%2Fpy9AS-6P) lots and lots.