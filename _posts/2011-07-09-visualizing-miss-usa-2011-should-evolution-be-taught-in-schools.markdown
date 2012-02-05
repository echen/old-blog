---
date: '2011-07-09 13:02:05'
layout: post
slug: visualizing-miss-usa-2011-should-evolution-be-taught-in-schools
status: publish
title: 'Visualizing Miss USA 2011: Should Evolution be Taught in Schools?'
wordpress_id: '351'
categories:
- projects
- visualizations
tags:
- evolution
- hacking education
- miss usa
- visualization
---

**tl;dr** Should evolution be taught in schools? Go [here](http://miss-usa-evolution.heroku.com) to visualize what the Miss USA contestants think.


# The Visualization


Education is an area sorely in need of data crunching, so when I ran across [an amusing video](http://www.youtube.com/watch?v=9QBv2CFTSWU&feature=player_embedded#at=56) satirizing the Miss USA contestants' thoughts on teaching evolution, I thought it would be fun to transcribe [the original video](//www.youtube.com/watch?v=UkBmhM0R2A0&feature=youtu.be#at=41) and visualize the data.

[youtube=http://www.youtube.com/watch?v=9QBv2CFTSWU&feature=player_embedded#at=56]
[youtube=http://www.youtube.com/watch?v=UkBmhM0R2A0&feature=youtu.be#at=41]

  


So after some <del>tedious</del> illuminating transcription, I built [this app](http://miss-usa-evolution.heroku.com) to categorize and visualize the responses in various ways. (Mouseover states to see transcriptions, and click to jump to each contestant's response in the video.)


# Example Maps


Here are some examples of the generated maps.

First, we can look at which contestants believe in evolution (Miss California -- the winner! -- is the only contestant who explicitly states she believes in evolution; the red states explicitly state they do not believe in evolution; the grey states don't make clear what they believe):

[![Believe Evolution](http://dl.dropbox.com/u/10506/blog/miss-usa-evolution/believe-evolution.png)](http://miss-usa-evolution.heroku.com/?column=believes)

We can also see which contestants believe evolution should be taught in schools (green states say yes, red states say no, grey states say maybe or that it should be a choice):

[![Teach Evolution](http://dl.dropbox.com/u/10506/blog/miss-usa-evolution/teach-evolution.png)](http://miss-usa-evolution.heroku.com/?column=should_teach)

Here is a rough Darwin-friendliness score I assigned to each response (worst in dark red to best in dark green):

[![Score](http://dl.dropbox.com/u/10506/blog/miss-usa-evolution/score.png)](http://miss-usa-evolution.heroku.com/?column=score)

This map shows which contestants believe schools should teach creationism:

[![Teach Creationism](http://dl.dropbox.com/u/10506/blog/miss-usa-evolution/teach-creationism.png)](http://miss-usa-evolution.heroku.com/?column=teach_creationism)

And this map shows which contestants mention science in their response:

[![Mention Science](http://dl.dropbox.com/u/10506/blog/miss-usa-evolution/mention-science.png)](http://miss-usa-evolution.heroku.com/?column=mentions_science)

So while there aren't any striking patterns (I was hoping for a bright swath of red across the most religious states), the data's still fun to look at, and it's helpful to see that Alabama, whose [strongly anti-evolution](http://www.youtube.com/watch?v=UkBmhM0R2A0&feature=youtu.be#at=42) candidate is the only one colored red in both of the first two maps, does seem to be a bit of an outlier with respect to the rest of the nation.
