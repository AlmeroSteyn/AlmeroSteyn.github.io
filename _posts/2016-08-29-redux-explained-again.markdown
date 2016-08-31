---
layout: post
title:  Still don't understand why you need Redux? Read this...
description: "Redux explain really really really simply"
date:   2016-08-29 16:10:21 -0100
categories: Redux React Javascript
---

So I started looking at **React** recently. And whilst this was an instant hit for me, it is rarely mentioned in a
sentence without **Redux**. And honestly, I had no idea why I wanted to use that.

Yep, predictable JavaScript state container to keep your state in one place but I always keep my state minimised and never have issues
with it requiring understanding another tool, right? *RIGHT?*

I plowed through many tutorials and blog articles, which were all very good, no doubt, but I needed it explained super
simply and for someone who did not really want to use it.

Then after a few days of thinking and reading the light finally came on and it was a pretty bright light!

So if you are like me and still do not know why you need **Redux** stick with me for a few minutes as I explain what I
learnt and why I currently think it is the coolest thing since sliced bread.

**The Problem**

It is generally accepted that in order to fix a problem you first have to admit that you have one. So let's look at
why most client side applications suffer from problems related to state.

It is getting to the point where it can almost be accepted that the JavaScript application we are writing involves the
creation, arranging and re-use of some form of components.

So meet Mr. Component:

**TODO** Component image


