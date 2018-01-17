---
layout: post
title: "Royal Hackaway 2018"
date: 2018-01-15
tags: software life hacking mlh hackathon royalholloway university london
---

Another weekend, another hackathon - the first MLH Europe hackathon of 2018. After the hectic but enjoyable Christmas period (which involved less coding than I was happy with) I was looking forward to getting stuck in to another all-night programming-fest.

After making the not-too-long journey down to Royal Holloway University of London and *eventually* finding the right building (sidenote - Royal Holloway's campus has some really beautiful areas) my teammate and myself signed in with the organisers and took our seats for the opening ceremony, where we would find out what theme(s) had been set for the next 24 hours. The room was buzzing with excitement as the theme was announced...

**Open Data**

That's it. These two words were our theme. I had a vague idea what was required - take a data set from some open source and use it. Or, slightly more accurately:

*Open data is data that can be freely used, re-used and redistributed by anyone - subject only, at most, to the requirement to attribute and sharealike.* - [The Open Data Handbook](http://opendatahandbook.org/guide/en/what-is-open-data/).

Basically, make a cool thing with whatever data you can get your hands on. API-tastic.

While I hadn't expected this as a theme (these kind of events are almost completely unpredictable) it quickly became apparent exactly how much open data there is out there. Organisers pointed us to [data.gov.uk](https://data.gov.uk/) as one amazing source of this. From more obvious data sets (for example [crime statistics](https://data.gov.uk/dataset/crime_statistics) and [road safety data](https://data.gov.uk/dataset/road-accidents-safety-data)), through to the weird and wonderful ([the ancient woodlands of England](https://data.gov.uk/dataset/ancient-woodlands-england2) and [the useages of football pitches in Plymouth](https://data.gov.uk/dataset/plymouth-football-pitches-team-use)), the possibilities were quite clearly nearly endless.

Our team of two had previously decided that it would be quite fun to have a go at a hardware hack, as neither of us are too experienced in the hardware side of these competitions and it seemed like a fun and different thing to do. After some looking around at the device lab (MLH bring a wide range of hardware for participants to use for free), we decided to pick up a Qualcomm DragonBoard 410c. Neither of us had used one before, and although they are often joked about as an impossible device to get working at many hackathons, we were up for a challenge (plus there was a prize going to the best Internet of Things hack using the DragonBoard)!

So now we just had to find an idea to fit the following:
* Use a Qualcomm DragonBoard 410c
* Make an IoT hack
* Use some 'Open Data' (though even with the fancy definition above, the edges here were fuzzy)

After a period of spitballing increasingly silly ideas (IoT all the things!) we ended up settling on a middle ground kind-of-silly-but-also-not-really concept, inspired by the Harry Potter franchise.

Now, diehard fans of the series will probably instantly know what I mean by the words 'Weasley Clock', but for the uninitiated, the [Weasley Clock](http://harrypotter.wikia.com/wiki/Weasley_Clock) was a clock owned by the Weasley family which individually monitored each of their whereabouts. The clock had a hand, for each member of the Weasley family, and in place of hours on the clock's face were a series of possible locations, for example "home," "school" and "work". When this was originally written about in 1998, the idea of a clock that tells you where people are was so fantastical. But now, with a little bit of computer wizardry (pun intended) this should be not too difficult to make...

The first thing we needed to do was to actually get the DragonBoard working. MLH supplied a little guide due to the sheer number of people that struggle to get these working at events. The first board we tried was completely unresponsive, and after half an hour of fiddling and blaming ourselves for the fault (*it can't possibly be the computer - they're so much smarter than humans*), we swapped it in for a second DragonBoard, which was up and running with a version of Debian in no time. While the WiFi was occasionally flaky, and text editors in the shell often ran in to visual bugs, it was enough to get started on.

After this, we set about finding out exactly what the DragonBoard could do, and what toys the hardware lab offered to extend it. Moving parts are obviously a must for the clock, so rooting around in the tub of DragonBoard hardware for something that would help was priority #1. In the end, we found a stepper motor and a driver board for it, both designed to work with the DragonBoard (and it's sensor mezzanine, that we were also supplied). *What a good idea for the clock's hand*. This simply plugged in to a port on the DragonBoard, and then...

Erm...

Then what? We both knew the basics of utilising GPIO pins on a board similar to this one (prior work with Raspberry Pis), but there was no documentation around how this particular driver board or stepper motor worked. We figured that it couldn't be too different to a bog standard stepper motor, so tried to apply all the normal principles. Anything we tried failed to work. 2 hours of googling and guessing, and we had zero progress to show for it. At this point, if it was my first hackathon, I might have been more nervous. I wasn't, because almost every other hackathon I've been to has taught me that roadblocks like this are par for the course. We stepped back, and took a brief pause to collect our thoughts.

Our conclusion was to return to the wonderful box of components, and try another. First, one the same (*the first DragonBoard was broken, why not the stepper motor too?*), and then a completely different motor (*maybe there will be documentation for that one SOMEWHERE*)...

Banging our heads against the same wall for the next hour or two brought us no closer. It wasn't the motor/driver board, it was us. Clearly we were lacking some fundamental piece of understanding or knowledge that was written NOWHERE on the internet (we concluded that there must have been some paper instructions supplied with the stepper motor when bought, which had been lost).

Plan B - a completely different motor. A micro-servo, a Kuman KY66 to be specific. This worked far better. After a few minutes of fiddling in Python, we had a moving thing! This was far simpler, just needing +5V, 0V, and an input to indicate if it should be turning or not. 3 GPIO pins - that's all! The drawback of using this one however was that it only moves through 180 degrees (i.e. our clock had just lost half of its possible states).

*But it moved*.

And we knew *how* to make it move. Ok, it was slightly imprecise, but whatever. A breakthrough had been made.

So, now it moved, the next thing to do was programatically define when and where it moved. To start this, we had a little search around for ways we might listen to someone's location. After poking around some Google Places development pages we realised that was a dead-end, as it didn't seem data concerning a single user was accessible. This was a shame, as this could have produced a nice continuous data stream.

Because this wasn't possible, we turned to looking for a more manual source of location data. A few possibilities came up - Facebook offer a check-in style post, you can geo-tag posts on Instagram and Twitter, and a few years ago there was even an entire application based entirely around checking-in called FourSquare.

Looking through these possibilities, we thought that FourSquare was a bit outdated (though would have worked nicely) and the act of checking-in was far less passive than on other apps. Facebook also might have been nice, but how often do you check-in to your home? Finally, Instagram was ruled out - as any young person knows, if you're serious about your selfie-game, hours can be spent touching up your photos before you post and by then you're probably no longer in the same location.

Twitter stood as our champion.

In our opinions, it made more sense. Tweeting (in our experience) was more frequent, more passive, and provided the geo-tagged goodness we needed.

Now, we just needed a way to pull down the data. Twitter facilitates application development quite nicely, and actually has a wide range of [developer tools and documentation](https://developer.twitter.com/en/docs), but to save a bit of time reading up on the wealth of information there, we used [Tweepy](http://www.tweepy.org/) to access the Twitter API. Tweepy is a Python library that allows quite powerful searches while listening to a set of Twitter users, hashtags or keywords. It also quite neatly allows tweets to be returned in a sensible JSON format (one of which, conveniently, was 'location').

This meant that by using Tweepy to listen to our single test twitter user and stripping the location from their tweets, we could determine when to move the servo. Some simple stitching together later (something like `if location == 'place' then move('place')`), we just had to make a clock housing for our little invention to live in.

At this point, I'd love to tell you that we 3D printed a fancy ornate clockface, with calligraphy-style lettering around the edges detailing each place, and beautiful decoration.

Not quite.

Unfortunately, there was no 3D printer available, so we did the best we could with the tools provided. Those tools being a delivered by a Domino's delivery driver, at midnight. Looking through the old pizza boxes for one that was clean-ish, we returned to our workstation slightly greasier, but with a piece of cardboard that smelt of victory (and melted cheese).

We wrapped it in duct-tape so it wasn't so obviously leftover waste (*duct tape fixes everything*), coloured it in and wrote on some place names. The servo was popped through the middle of the cardboard, and hey-presto, we had a magic clock. Some fine-tuning of the clock hand later (and a plastic fork blu-tack'ed on to extend the servo's tiny arm), we were done.

In 24 hours, we'd gone from nothing to this:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">The Magic Clock team used geotagged tweets and the Qualcomm Dragonboard to build a Weasly Clock <a href="https://twitter.com/hashtag/Hackaway2018?src=hash&amp;ref_src=twsrc%5Etfw">#Hackaway2018</a> <a href="https://t.co/nLc0j1YcfA">pic.twitter.com/nLc0j1YcfA</a></p>&mdash; Major League Hacking (@MLHacks) <a href="https://twitter.com/MLHacks/status/952529877781172225?ref_src=twsrc%5Etfw">January 14, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Presentation time came and went, the most eventful part of ours being the WiFi would occasionally drop in and out (not ideal for an IoT hack). Some highlights of other participants included 'SaferWay' (a mapping project that tells you how safe a route is), 'Alexa the Barbarian' (an Alexa skill to generate a D&D character) and 'Alpaca' (an NLP study companion). You can check out the submissions [here](https://royal-hackaway.devpost.com/submissions). Time and again at these events I am amazed at the sheer ingenuity of the hacks produced.

Prize-giving followed, and our little Weasley Clock actually won 'Best IoT hack'! For our troubles, we were both given a Qualcomm DragonBoard 410c, so we could continue our hack at home (major thanks to MLH and sponsors for providing such great prizes)!

The entire hackathon was a great success, and these kind of events really help expand knowledge and can provide a change of pace to everyday development. I cannot recommend MLH events highly enough.

Finally, I have to say thank you and congratulations to the organisers of Royal Holloway's first MLH hackathon - it was a great weekend and I hope these become an annual event! For anyone interested you can find the devpost for the Weasley Clock [here](https://devpost.com/software/royalhackaway2018). Let me know what you think!
