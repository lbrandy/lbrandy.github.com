---
title: "Interviews, from every angle..."
date: '2011-01-03'
description:
categories:
tags: []

layout: post
type: draft
---
I've been ominously silent for several weeks now. The reason is simple: I've been interviewing.

I currently work at <a href="www.pittpatt.com">Pittsburgh Pattern Recognition</a> (note: we're hiring software engineers, if you are interested in a tiny startup-like company working on face recognition). My wife and I have decided to relocate from Pittsburgh for largely personal reasons. In the end, we decided to relocate to California, the Bay Area to be exact.

I spiffed up my resume and sent it out to a ton of places. I thought the economy was going to make it a tough time to find a job. Well, either my resume is truly spectacular, or the job market in Silicon Valley is really booming, because I received a pretty overwhelming response. I had 10+ phone calls and 6 on-site interviews. In the end, I had 5 offers.

And just in case you think I'm bragging, I'll go ahead and publish the most horrifying and ego-crushing news in detail: I got rejections from 2 companies as well. Both startups. One of them after an on-site interview, and one after a phone screen. Yes, I was phone screened. To be fair, though, I deserved it. It was, to be frank, a miserable performance on my part. And worst of all, he was a friend of a friend through which I was referred. How embarrassing.

Having spent a ton of time conducting and thinking about interviews over the last 5 years, and then to be put into the position of being interviewed (and being lucky enough to do so many back to back), I saw so many interesting things I feel like I could write a book (scratch that, I know I could write a book). Your perspective on interviewing changes quite a bit when you are giving the interviewer and it's really easy to be lured into a false sense of skillfulness. Having looked at from that angle, going back through the process as the interviewee was quite enlightening. Here's what I learned.

<strong>You will be false-positive'd. </strong> The "google-style" interview is both omnipresent and designed to minimize false-negatives (bad hires) in an expedient fashion. This necessitates an increase in false positives (rejecting good people). The industry is fairly cargo-cult about this. Google (et al.) can afford a false positive rate, and many firms try to imitate the google interview process -- even those who don't see the "resume flow" that Google does.

<strong>You will be false-positive'd. </strong> This is easier said than done, but: try to get multiple interviews and try not to put the ones you really care about early. Furthermore, when you crash and burn on one of those early interviews, please want to quit programming forever -- or at least keep the angst to a single day.

<strong>Interviewing (especially technical interviews) is absolutely, positively a skill</strong>. You must practice. The phone screen that I flunked was one of my first. By the end of the process, I would have crushed that exact same interview with ease.

<strong>There are only so many question "types". </strong>By the end of my process, between the previous interviews and my interview prep, virtually every question I heard was at least some variant of some other question I'd heard.

<strong>Know the time and space complexity of everything you do.</strong> I can't stress this enough. You have to feel big-O in your bones. If someone says your linear algorithm can be made logarithmic, you have to know what that means (practically, not theoretically) because it's usually a pretty big hint (note: it usually means you need to be able to look at one item and remove some fraction -- usually half -- of what's left).

<strong>Solve everything recursively and non-recursively. </strong>For any practice problem that can be done recursively, do both.

<strong>Always think about corner cases. </strong>What if one object is bad, or null. What if the node isn't in the tree. What if A is much larger than B.

Every question you don't know, write down. <strong>Keep a list. </strong>Revisit that list frequently.

<strong>Write, don't assume. </strong>This one is really important. Get out a piece of paper (or better: buy a whiteboard) and write down the answer to every single question or practice problem. Do it at least once. Trust me on this. You'll assume you know how to do something, and then when it comes time to do it on the whiteboard, you'll screw it up (or freeze). Reverse a linked list, yea yea, really easy. I bet if you haven't done it in 4 years (or ever), under interview conditions, it's much, much harder than you think.

Here's my study guide:
<ol>
	<li><a href="http://www.amazon.com/gp/product/047012167X?ie=UTF8&amp;tag=lbrandycom-20&amp;linkCode=as2&amp;camp=1789&amp;creative=390957&amp;creativeASIN=047012167X">Programming Interviews Exposed</a> -- Read it. Know everything in it. (note: this is baseline knowledge. This book alone isn't enough.)</li>
	<li>Fully implement: linked-list, binary search tree, hash-table (including validity checks)</li>
	<li>Lesser known but vital for interviews: Heap, Prefix tree</li>
	<li>Other cool data-structures to know of: skip-list, b-tree, bloom filter, avl/redblack/splay trees</li>
	<li>Quicksort, Mergesort, Linear sorting (postman, radix, bucket). Binary Search. Not just time but space complexity.</li>
	<li>Know big-O really well. Feel big-O in your bones.</li>
	<li>Dynamic Programming (see topcoder)</li>
	<li>Scour glassdoor.com for questions</li>
</ol>