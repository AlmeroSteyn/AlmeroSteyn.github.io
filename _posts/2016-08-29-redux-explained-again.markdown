---
layout: post
title:  Still don't understand why you need Redux? Read this...
description: "Redux explain really really really simply"
date:   2016-08-29 16:10:21 -0100
categories: Redux React Javascript
---

So I started looking at **React** recently. This was an instant hit for me, but it is rarely mentioned in a
sentence without **Redux** and honestly, at the beginning, I had no idea why I would want to use that.

*"A predictable JavaScript state container to keep your state in one place"* sounds nice, but I was pretty sure that I
kept my application state small and localised enough to not require yet another tool, right? *RIGHT?*

I plowed through many tutorials and blog articles, which were all very good, but I found it hard to see the problem **Redux**
solves and most importantly, that this problem was also present in my code. In fact, the only reason I invested the effort was because
I regard those who recommend it very highly.

Then after a few days of thinking and reading the light finally came on and it was a pretty bright light!

So I thought I would write this article for people like me. And this article will focus purely on illustrating the
problem **Redux** solves. You won't find a single line of getting started code here, for that there are brilliant resources out
there. My hope is that after reading this article you will be one step closer to figuring our why **Redux** is one of
the coolest things since sliced bread.

**The Problem**

It is generally accepted that in order to fix a problem you first have to admit that you have one. So let's look at
why many client side applications suffer from problems related to state.

Since more and more JavaScript frameworks and libraries are adopting components as the de-facto way if creating web applications,
we will also look at the problem from this perspective.

So meet Mr. and Mrs. Component:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/component-man.png" alt="Mr and mrs Component">
</figure>
{:/}

Mr. and Mrs. Component lives in *Web Town*. Web Town lies close to the sea and decided that it wanted a bright and
shiny new beachfront. All citizens were working very hard to make that happen.

Sadly, Web Town's council thought that great people and enough enthusiasm was enough to make this happen by itself without
any form of coordination.

People would make new benches or umbrellas or anything you would expect to find on a nice beachfront and just go and install it.
If you did not like the bar counter someone else installed, you could paint it blue yourself.

Meanwhile, news of the changes to the beachfront relied on the grapevine to reach all the citizens.

Of course, the efforts of the many citizens of Web Town soon started to look like this:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/comms-lines.png" alt="Garbled communications lines between citizens">
</figure>
{:/}

Crossed communication lines and very inefficient changes to the beachfront was at the order of the day and Web Town's beachfront
soon started to look like this:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/messy.png" alt="Messy beachfront with not planning in the arrangement">
</figure>
{:/}

**The Redux Beachfront Manufacturing Store to the rescue**

Web Town was in trouble. Many citizens were trying to make similar changes to the beach front, benches were being installed
where the merry-go-round should go, money was being wasted and more than one punch-up ensued.

Something had to be done. so after an emergency meeting of the town council it was decided to call in professional help. What Web Town needed was
some serious coordination. And that was how the *Redux Beachfront Manufacturing Store* was born.

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/store.png" alt="The redux store shown as a building">
</figure>
{:/}

*NOTE: Although the term **store** in Redux refers to storage, in this article we will also use the shop meaning of store,
as the Redux store also provides us with some services... It also makes for more fun drawings!*

The first issue that needed to be tackled was to ensure that all of the citizens' efforts would channeled through
the store alone.

To accomplish this the store set a few rules:

- Whenever someone made anything that was to be installed, they had to bring it to the store and not
install it directly. Here the item would be scheduled for installation and, at the appropriate moment, it would be
expertly installed.

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/store-install.png" alt="Showing a citizen bringing an addition to the beachfront to the store">
</figure>
{:/}

- All communication were to go via the store. All information about the progress of the beach front and the changes to be
made went to the store's communication department. Here it could be safely archived but more importantly, all changes to the
beachfront were instantly communicated to all citizens.

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/store-comms.png" alt="The store notifying all citizens that a change has been made">
</figure>
{:/}

- And finally, as the CEO of the store was a student at *Hogwarts* university, he introduced a bit of magic. To make sure
that they could easily recreate the beachfront at any point in time he would yell something like *"REDUXO!!"* and create a new copy
of the beachfront every time before they made the actual change.

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/magical-copies.png" alt="Magical copies of the beachfront being made with every addition">
</figure>
{:/}

The rules meant that:

- Changes to the beachfront would be made in the correct place and in the proper sequence.
- Changes could be made by a single store worker.
- Everyone always knew when a change was made to the beachfront and could immediately react to it.
- They could always go back to any version of the beachfront should something go wrong and they needed to find out what
happened.

This lead to a resounding success! The new store not only ensured the creation of a lovely beachfront,
it also saved time and money for each and every citizen!

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/final-result.png" alt="Final nice beachfront that was created">
</figure>
{:/}

**Your application state**

Just like Web Town, your application also has something that many bits of code (or components) will use and update. And that is your
application state. And just like Web Town, leaving the update work to each bit of code means that the code will need
to get more complex. Also, it means that each bit of code will need to try and work with the changes all other bits of code
in the system is trying to make to the state.

In small applications this does not seem like an issue, but every large enterprise application suffers from complexity
surrounding this issue. In fact after you have tried out **Redux** you will be surprised how soon you start seeing
a benefit from using it, even in applications where you think the state is minimal.

**Redux** provides a solution by ensuring that:

- Your state is wrapped in a store which handles all updates and notifies all code that subscribes to the store of updates
to the state. You don't need to pass state through an entire component tree anymore but can subscribe to these changes much closer
to where the information is needed.
- All changes are made sequentially to ensure a predictable end result free from unexpected effects and race conditions.
- The state is immutable, meaning that every change in state results in a totally new version of the state, enabling us
to write more predictable code or go and look at any previous version of the state through the **Redux developer tooling**.
This leads to an incredible debug experience.

Just like Web Town, introducing **Redux** into your application will result in you having to write and maintain less code and
less complicated code. And that is always a result worth investing in!

**React**

When I first looked at using **Redux** in **React** I did not immediately see that there is a great **Redux wrapper
application** called **React Redux** (*big surprise there*), which handles a surprising amount of the code required to
make **Redux** work for you!

**So how do I implement it then**

I hope that this article has made a strong case for using **Redux**. So head onto the following links to see how you can use it. These
links focus on using **Redux** with **React** but rest assured that it can be used in any JavaScript application and more often than
not you will find some wrappers already written for your technology of choice.

- [Redux](https://github.com/reactjs/redux)
- [Getting started with Redux by Dan Abramov](https://egghead.io/courses/getting-started-with-redux)
- [Learn Redux by Wes Bos](https://learnredux.com/)
- [React Redux](https://github.com/reactjs/react-redux)