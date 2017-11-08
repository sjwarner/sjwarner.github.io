---
layout: post
title: "Hacktoberfest 2017 - Part Three"
date: 2017-11-01
tags: work black-pepper software life hacktoberfest 2017
---

<img src="/assets/hacktoberfest-orange.png" alt="Hacktoberfest Banner" style="width: 100%;"/>

October is over for another year, and along with it Hacktoberfest 2017. It hasn't been a slow month for me by any means. Between going back to my parent's house, days out (I had a fantastic time at the British Library recently), work, and hanging out with friends, I haven't had much free time. However, in all the mayhem I did manage to find time to contribute to the world of open source software for the very first (and second, and third...) time.

If you have read my other two blog posts about Hacktoberfest 2017, you'll know that my workplace has been fantastically supportive in getting employees involved with Hacktoberfest and open source, and you'll have seen my top 5 tips about going out there and doing it yourself! If you haven't, where have you been?! But seriously - a quick catchup. Hacktoberfest is an annual event that dedicates October to contributing to open source software, in collaboration with DigitalOcean and GitHub. Programmers the world over find a project they are interested in, contributing to thousands of repos. Upon completing 4 pull requests, participants are promised a glorious t-shirt, sticker pack and most importantly gain the pride of saying that they completed Hacktoberfest 2017.

I've been taking part for the last month, and today I'll be talking about my own experiences, my first adventures in open source software, and what exactly I contributed where.

So, in my previous post, I talked about how I've found being part of a healthy and active community has really helped me become more involved in code contributions and not become discouraged when my pull requests need amending. The community that I have been part of for October (and going forward I want to stay very involved) is 'Exercism'.

Exercism is a learning tool founded by Katrina Owen, designed to pick up / progress / refine skills in a variety of programming languages. It is a completely free online tool that promotes test-driven development in a friendly and conducive environment. Each user is given an unimplemented exercise and some failing unit tests, and has to make their implementation pass all of the tests. Solutions are then viewable on the website [exercism.io](exercism.io), where others that have already completed the exercise may comment and discuss each different program.

I've been using Exercism since joining Black Pepper as a way of quickly ramping up in new languages when appropriate, and have greatly enjoyed the experience. As such, I thought it might be a good idea to give back, as the entire project is open source.

As a newbie to contributing, I started out small. Exercism is currently about to undergo a large transition to a brand new shiny website, which at the minute is in [beta](v2.exercism.io). As part of this, the way in which users will unlock exercises in a different way - and to allow this, all exercises needed tagging with a list of topics, so each problem can unlock other relevant problems. Hardly the most glamorous of code, but it needed doing and was a grand way of dipping my toes in the water.

After a couple of contributions in this ilk, and some documentation updates, I was feeling more confident. Repository admins were friendly, seemed really excited that I was helping out, and offered constructive criticism in order to make both their own and my life easier! I decided to pick up something a bit meatier...

I decided to implement an exercise. Most of the groundwork is already done for you. Due to the fact that there are many language tracks, each using the same problems, a lot of the canonical data is centralised in a [project-specifications](https://github.com/exercism/problem-specifications/) repo. This means that READMEs are already mainly there, and the unit tests just need to be converted from a language-agnostic file to whichever language you are implementing the exercise in.

Because both the Python and Java tracks were flooded with helpful Hacktoberists (is that a word?), I chose to create my exercise in a less popular language that also had a working knowledge of. I chose to implement an atbash cipher exercise in the Bash language track. Atbash in Bash. Atbash Bash. Atbashbashatbashbashatbash. I already liked the way it sounded. After double checking the `Contributing.md` file in the exercism's Bash repository, I set about coding. It was quite simple really - all you had to do was implement the tests listed in the canonical data, make a more language-specific version of the README.md provided, update the `config.json` with details (including a difficulty rating and list of related topics), and finally make an example program that passes all unit tests.

It sounds like a lot, but broken down into the constituent parts, it really isn't. The entirety of my pull request was less than 150 lines of code. And by breaking it in to smaller tasks, I was more confident that I was doing it all right. Eventually, after a day of head scratching and making it perfect (this was my baby, after all), I submitted the PR. And it sat there, waiting approval. The Travis CI build passed. And I waited. It was agonising, watching and waiting... So I picked up another task!

This time an implementation of the typical starter program 'Two-fer'. It's barely a step up from 'Hello World', but it was still exciting. Because it was such a basic exercise, I chose to implement it in a language I had less experience with - erlang. As a large number of you probably know, erlang is a general-purpose functional programming language, and one of the quieter tracks on exercism. This made it easier for me to find an open issue and claim it.

So I set about coding, once more. I got familiar with the syntax, and implemented the exercise, in the same manner that I did with my atbash cipher. README, config, tests, example... And submitted it.

This one got much more immediate feedback. Lots of edits. But I wasn't discouraged - I wanted to get this done, I wanted it to be part of exercism, and I wanted my t-shirt! So I fixed it up. It was up for a few minutes before more changes were requested. All of them reasonable, and quick enough to do. I fixed my little erlang baby up, and updated the PR. More edits. This little back and forth happened a couple of times before it was merged in - but I didn't mind. It was accepted. I had passed all the barriers. I was part of exercism - and not just a small tagging part - I had a whole exercise that was à la moi. I was overjoyed.

And then I thought... Hang on - what about my bash baby?! My atbash cipher?! Where was the feedback - the erlang admin had been so prompt and nice, my was my atbash cipher being ignored?

These were the thoughts of a panicked parent. The dad that worries his son has been tackled too hard in the primary school football match. The mum that worries her daughter isn't being paid enough attention by the teachers.

What I failed to think about was that Hacktoberfest was possibly the most busy the poor exercism admins had been. They were ran off their feet, and eyes couldn't possibly be cast everywhere. After taking some deep breaths and thinking a little more sensibly, I popped on the exercism gitter channel (an amazing tool to connect with amazing pepople). I flagged the issue here, and soon enough, it was reviewed and pulled in - no edits necessary! Boy, was I proud. My t-shirt was earnt way before this point, but that didn't matter.

And it still doesn't. I contributed all the way up to the end of October, and even now in November I have some bugs and features I have picked up and plan to fix or implement soon. My t-shirt and sticker pack are in the post, but I still want to give. I've found it such a good way to learn and contribute to tools I use daily - and the first time I found (and used) my own code on exercism, I was truly excited. I still get that rush when I stumble across my code - even when it is for the 10th time.

If you're interested in seeing my contributions, you can take a look [here](https://hacktoberfest.digitalocean.com/stats/sjwarner-bp).

I'll just finish off by saying that Hacktoberfest 2017 has been a great personal success, and I hope many of you out there have also found it the same. I cannot speak of it highly enough, and urge readers to take part next year (or even pick a project to contribute to in the meantime). It's only 11 more months...
