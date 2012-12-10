---
title: "My story: Bootcamp at facebook"
date: '2012-01-07'
description:
categories:
tags: []

layout: post
type: draft
---
I've taken a non-trivial amount of time away from both the literal and the proverbial keyboard. I've had a chance to settle into the new job at facebook, get a lay of the land, and I found out (the hard way) that once you break the habit of writing, it's more than difficult to get back into it. That said, I have quite the happy backlog of topics to write about. Let's start with one that's been on ice for quite awhile. The noshit reallife guide into the first <span style="text-decoration: line-through;">6 weeks</span> 4 days as an employee at  facebook.

Please note, I've been at facebook about 10 months now. Most of this was written very early on in my experience, though.

<strong>The idea of bootcamp</strong>

Bootcamp is facebook's six week intro to facebook. During this time, you get frequent lectures from engineers about the tools/services and you get tasks from all over the company (hopefully bite-sized ones) that give you exposure to the entire codebase. You can end up with anything from javascript/CSS/UI work down to C infrastructure/services stuff. At the end of bootcamp, you get to pick the team you want to join. There's a fair bit more information about the philosophy and implementation of facebook's bootcamp online. I've merely given you enough background to understand the story that follows.

<strong>Day 1+2</strong>

Orientation. A motley collection of lectures ranging from technical information to corporate culture. Useful to a new employee, less useful as blog fodder.

For the purposes of our story, there's one thing I need to highlight. One of many oft-repeated mantras at facebook is this one: 'move fast and break things'. I should pause for a quick aside: it's pretty easy to misinterpret what this actually means in practice (maybe this is another blog post...). At any rate, during these first two days it was often repeated that facebook is a place where engineers are supposed to be truly empowered ("move fast and break things" is a statement, in my view, primarily about empowerment). If you see something you don't like, fix it. Diff it out. Send it to the owner. Yell at him until he accepts it. There's no boundaries. There's no sacred cows. If it really irks you, fix it. Be empowered. Do it.

Sounds great to a new person. Empowered! Fix ALL THE THINGS! I will admit that it's difficult as a 2-day-old employee to be anything but mildly incredulous.

<strong>Day 3</strong>

This was the day I got to sit at my computer for the first time with the rest of my 'class' of newbies and take a look at my task list. To my left was a guy coming from a startup. To my right was a guy who wrote his own language for fun. Across the way was a Y-combinator alumnus sitting next to the  South African unix guru and the girl who was previously an intern and therefore, seemingly, knew everything. I looked at my task list. My first task<strong>: fix the fucking front page of facebook.</strong> Let me repeated that. My first task at facebook was to fix the fucking front page.

It turns out that when you tried to login to facebook, using a right-to-left language (persian, hebrew, etc.), the language selector widget turns into a hot mess. This was quite apparent and incredibly ugly. I spent the entire first Wendesday digging around in the i18n code trying to figure out where the function (it had to already exist, right?) was that would automagically determine if the language was right-to-left so we could set the correct style sheet attribute. Did I mention I'm mostly a C++/systems/infrastructure programmer?

I worked all day on a 9 line day diff that 1) I could send out and 2) wasn't embarrassing. Day #1 at facebook I sent out a diff that changed the code at http://facebook.com/login.php. This is pure craziness. How many times a day do you think that code gets run? The idea of empowering programmers isn't corpo-talk. It's very, very real.

Full disclosure: I stayed pretty late on day #1 because I -really- wanted to say I got a diff out on my first day that touched login.php. At about one hour per line, it's certainty not my least productive day.

<strong>Day 4</strong>

I got to see the reviews for my first ever diff. Lots of comments on my diff, none about the content of my diff. Everyone was talking about the bizarre picture of a cat that somehow got inserted into my diff. Where did this cat come from? What the fuck is going on?

It turns out that the diff review tool at facebook has support for image macros which it does via simple text substitition. It also turns out that the author of this particular bit of software (hi eprisetly) is a fan of pokeman. It just so happens that "persian" is both a right-to-left language and a pokeman. So while I'm desperately writing up a small novella about how this diff fixes the problems with the persian language, all anyone else can do is talk about how my diff is full of pokeman cats. Seriously, what the fuck.

I worked most of my second day locating (and then about 19 seconds fixing) the place in the code where the word "persian" resulted in a pokeman image. I changed it to "pokemanpersian".

Welcome to facebook.