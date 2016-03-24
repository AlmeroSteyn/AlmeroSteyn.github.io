---
layout: post
title:  "Angular2: Form validation salad."
description: "You know the basics, now see the power..."
date:   2016-03-23 16:10:21 -0100
categories: angular2 component form validation styles css content-projection transclude
---

One of the best things that ever happened to me in **AngularJS** was **ng-messages**. The projects I find myself on
are all very form intensive, and when **ng-messages** hit release it was, well, simply awesome. 

But I wanted more, I wanted a *transclude* directive that would wrap my input in some magical form-validation candy
without me having to write the boilerplate on every single form for every single form. And I did it. The *holy grail*
of form validation. 

If was pimped. No jokes. Adding custom validators in the HTML and controller code only, rendering the errors on the fly
and lots more.

So what better to try out in **Angulars** than to recreate one of the most complex **AngularJS** directives I ever wrote.

**SAY WHAT???!!**
In short, today we will be building an **Angular2** form validation component. And to see just how flexible it is,
we will be building the same component in three different ways. 

Before we come out the end of this blog post we will have used the following concepts in **Angular2** to see how they
fit into making a more complex functional component:

* Model forms
* 
