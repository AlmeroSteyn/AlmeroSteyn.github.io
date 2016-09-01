---
layout: post
title:  Still don't understand why you need Redux? Read this...
description: "Redux explain really really really simply"
date:   2016-08-29 16:10:21 -0100
categories: Redux React Javascript
---

So I started looking at **React** recently. This was an instant hit for me but it is rarely mentioned in a
sentence without **Redux**. And honestly, at the beginning I had no idea why I wanted to use that.

Yep, predictable JavaScript state container to keep your state in one place sounds nice, but I was pretty sure that I
kept my application state small and localised enough to not require yet another tool, right? *RIGHT?*

I plowed through many tutorials and blog articles, which were all very good, no doubt, but I needed it explained super
simply and for someone who did not really want to use it. I was driven more by my wanting to know why so many people
love **Redux** than by wanting to know **Redux**.

Then after a few days of thinking and reading the light finally came on and it was a pretty bright light!

So if you are like me and still do not know why you need **Redux** stick with me for a few minutes as I explain what I
learnt and why I currently think it is the coolest thing since sliced bread. I think it would be a great loss to
abandon **Redux** simply because the problem it is trying to solve is not immediately clear.

**The Problem**

It is generally accepted that in order to fix a problem you first have to admit that you have one. So let's look at
why many client side applications suffer from problems related to state.

More and more JavaScript frameworks and libraries are adopting components as the de-facto way if creating web applications
so we will also look at the problem from this perspective.

So meet Mr. Component:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/component-man.png" alt="Mr Component">
</figure>
{:/}

Mr. Component lives in *Web Town*. Web Town recently decided that it wanted a bright and shiny new beachfront and all citizens are working
very hard to realize this.

Web Town fully believes in the principal of a self organizing team and the telephone was deemed the only way of
communication required. If one of the citizens decided to make, say, a bench for the beachfront, he would do it, then
he may either install it himself or pass it onto someone to go and do it after making even more changes.

News of the changes to the beachfront trickles through the community through the grapevine.

Of course, left up to no form of coordination or proper communication and despite the best most enthusiastic efforts of the citizens, the communication
lines soon looked like this:

{::nomarkdown}
<figure>
    <img src="/css/images/2016-08-29-redux-explained-again/comms-lines.png" alt="Garbled communications lines between citizens">
</figure>
{:/}

Which of course meant that Web Town's beachfront soon came to look like this:

**TODO** Messy beach front

**The Redux Beachfront Manufacturing Store to the rescue**

Web Town was in trouble. Citizens were trying to make similar changes to the beach front, benches were being installed
where the merry-go-round should go. Money was being wasted and more than one punch-up ensued.

So after an emergency meeting of the town council it was decided to call in professional help. What Web Town needed was
some serious coordination. And so the *Redux Beachfront Manufacturing Store* was born.

**TODO** Image of the store.

*NOTE: Although the term **store** in Redux refers to storage, in this article we will also use the shop meaning of store,
as the Redux store also provides us with some services... It also makes for more fun drawings!*

Web Town realised that in order to ensure that it built the beachfront it wanted, the construction had to be managed
in one place. And while the citizens were pretty good in creating the parts needed for the beachfront, the assembly
of the various parts into one whole needed to be handled by the experts.

And that is where the *Redux Beachfront Manufacturing Store* came in.

They had a few rules:

- Whenever someone made something to be incorporated in the beachfront, it had to be shipped to the store and not
directly installed. The store would handle installing the items in the correct location.

**TODO** Image of person shipping something to the store and the store installing it

- All communication were to be done via the store. Whilst Web Town still allowed casual chats and parties, all conversations
around the beach front needed to go through the store's communication department. This meant that every time a change
was made to the beachfront the communications department would contact every citizen and inform them that the beachfront
has changed.

**TODO** Image of communication back to the people

- All conversations were to be recorded.

**TODO** Show timetravelling

- And finally, as the CEO of the store was a student at *Hogwarts* university, he introduced a but of magic. Instead of
only changing the actual beachfront every time a change was made, a magical copy was made of the beachfront before the
change so that they could very easily go back to any version in time should it appear that things were not going the way as planned.

**TODO** Image of dude making copies

The rules meant that:

- By having the store doing the actual installations it meant no more problems with some citizens trying to install
the same thing twice or installing two things in the same place.
- With the store handling the communications, it meant that all instructions to make a change to the beachfront went through
one central location and in sequence and that all citizens were informed every time the progress changed so they could
all adjust their own plans instantly and cut out problems later.
- Because all calls were recorded and magical copies were made of all changes it meant that, should anything go wrong,
the store could instantly go back to any version of the beachfront and apply all changes but the faulty one to it.

For Web Town, the outcome was a resounding success! The new store not only ensure the creation of a lovely beachfront,
it also saved time and money for each and every citizen!

**Your application state**

Just like Web Town, your application also has something that many bits of code will use and update. And that is your
application state. And just like Web Town, leaving this update work to each bit of code means that the code will need
to get more complex. Also, it means that each bit of code will need to try and work with the changes all other bits of code
in the system is trying to make to the state.

In small applications this does not seem like an issue, but every large enterprise application suffers from complexity
surrounding this issue.

**Redux** provides a solution to this issue but ensuring that:

- Your state is wrapped in a store which handles all updates and notifies all code that subscribes to the store of updates
to the state.
- All changes are made sequentially to ensure a predictable end result free from unexpected results and race conditions.
- The state is immutable, meaning that every change in state results in a totally new version of the state, enabling us
to go look at any previous version of the state through the **Redux developer tooling**.

Like with Web Town, introducing this into your application will result in you having to write less code. And that is always
a result worth investing in!

**React**

When I first looked at using **Redux** in **React** I did not immediately see that there is a great **Redux wrapper
application** called **React Redux** (*big surprise there*), which handles a surprising amount of the code required to
make **Redux** work for you!

**So how do I implement it then**

I hope that this article has made a strong case for using **Redux**. And whether or not you are using **React**, you can
benefit from this great tool and pattern in your application. So head onto the following links to see how you can use
it:

**TODO** Ambramov Redux tut
**TODO** Wes Bos tut
**TODO** Other?







