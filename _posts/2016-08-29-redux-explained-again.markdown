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

Mr. Component lives in *Web Town*. Web Town's wants a bright and shiny new beachfront and all citizens are working
together to realize this.

Web Town fully believes in the principal of a self organizing team and the telephone was deemed the only way of
communication required. If one of the citizens decided to make, say, a bench for the beachfront, he would do it, then
he may either install it himself or pass it onto someone to go and do it. He would then share the news with some
other citizens in the hopes that the entire town would come to hear that the bench was already made.

Of course, left up to no form of coordination, despite the best most enthusiastic efforts of the citizens the communication
lines soon looked like this:

**TODO** Squiggled line comms

Which of course means that Web Town's beachfront soon came to look like this:

**TODO** Messy beach front

By now, hopefully, it should be clear that the new beachfront being built represents our application state. Components
are continually reading from it and also making changes to it. With every component trying to alter te state to serve
its own needs it is no wonder that we soon have the spaghetti mess shown above.

Even if we are only talking about keeping tabs on an
**IsSaving** flag to show a spinner. No matter how small we try and keep the state, every enterprise application end
up a to a greater or lesser degree like Web Town, with serious crossed lines in communications.

**Redux to the rescue**

So how could we solve this?

Well, what Web Town needs is some serious coordination. And to that end they decided to set up the *Redux Beachfront Manufacturing Store*.

**TODO** Image of the store.

*NOTE: Although the term **store** in Redux refers to storage, in this article we will also use the shop meaning of store,
as the Redux store also provides us with some services...and its fun!*

Web Town realised that in order to ensure that it recieved the beachfront it wanted, the construction had to be managed
in one place. And while the citizens were pretty good in creating the parts needed for the beachfront, the assembly
of the various parts into one whole needed to be handled by the experts.

And that is where the *Redux Beachfront Manufacturing Store* came in.

They had a few rules:

- Whenever someone made something to be incorporated in the beachfront, it had to be shipped to the store and not
directly installed. The store would handle installing the items in the correct location.
- All communication were to be done via the store. Whilst Web Town still allowed casual chats and parties, all conversations
around the beach front needed to go through the store's communication department. This meant that every time a change
was made to the beachfront the communications department would contact every citizen and inform them that the beachfront
has changed.
- All conversations were to be recorded.
- And finally, as the CEO of the store was a student at *Hogwarts* university, he introduced a but of magic. Instead of
only changing the actual beachfront every time a change was made, a magical copy was made of the beachfront before the
change so that they could very easily go back to any version in time should it appear that things were not going the way as planned.

**TODO** Image of new flow

The rules meant that:

- By having the store doing the actual installations it meant no more problems with some citizens trying to install
the same thing twice or installing two things in the same place.
- With the store handling the communications, it meant that all instructions to make a change to the beachfront went through
one central location and in sequence and that all citizens were informed every time the progress changed so they could
all adjust their own plans instantly and cut out problems later.
- Because all calls were recorded and magical copies were made of all changes it meant that, should anything go wrong,
the store could instantly go back to any version of the beachfront and apply all changes but the faulty one to it.







