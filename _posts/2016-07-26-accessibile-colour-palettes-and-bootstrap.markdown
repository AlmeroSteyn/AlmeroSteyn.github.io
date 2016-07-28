---
layout: post
title:  "A11y: Create an accessible colour palette and use it in Bootstrap CSS"
description: "Colour contrast management made easy.."
date:   2016-07-26 16:10:21 -0100
categories: colorable bootstrap less color contrast colour accessibility a11y
---

One of the more subtle aspects of **Accessibility** is the need for good colour contrast when designing your web
applications. The **Web Content Accessibility Guideline (WCAG) Success Criterion 1.4.3** states the following:

>**Contrast (Minimum)**: The visual presentation of text and images of text has a contrast ratio of at least 4.5:1,
>except for the following: (Level AA)
>
>**Large Text**: Large-scale text and images of large-scale text have a contrast ratio of at least 3:1.
>
>**Incidental**: Text or images of text that are part of an inactive user interface component, that are pure decoration, that are not visible to anyone, or that are part of a picture that contains significant other visual content, have no contrast requirement.
>
>**Logotypes**: Text that is part of a logo or brand name has no minimum contrast requirement.

OK, English please!

Quite simply this means that any text on your website should really form a good contrast with the background it is written
on. And translated even more simply: Use a text colour that shoes off clearly on the colour of the background.

Why is this so important?

Well, many users face difficulties that hamper their vision. Whether it is an actual visual disability, like colour blindness,
or or simply sitting outside on a sunny day with your smart-phone, text of low contrast can be extremely difficult
to read for many users under different conditions.

Point is, your site is to be read to be understood.

**The colour contrast implementation challenge.**

Great, now we know why, but here is another little secret. Ensuring that every page you build conforms to these
contrast requirements can be a very difficult and lengthy process.

Then combine these challenges with using a complex CSS framework like **Bootstrap CSS** and you can quickly end up with
an unmanageable mess.

I have personally seen the following in many a project:

{% highlight html %}
  <link rel="stylesheet" href="bootstrap.css">
  <link rel="stylesheet" href="company-style.css">
  <link rel="stylesheet" href="project-style.css">
{% endhighlight %}

With this kind of hierarchy it quickly becomes a long winded process to properly implement the colour-contrast styles we
need, or any required style for that matter.

How can we make this easier?

The problem can be made far less challenging by doing two things:

- Pre-calculate your accessible colour combinations
- Use LESS or SASS

**Pre-calculate an accessible colour combinations matrix.**

Our goal here is to, even before we start, select a range of colours that we want to us in our project and then
calculate the colour pairs we can use as front- and background colours to conform to the minimum contrast specified by
the WCAG](https://www.w3.org/WAI/intro/wcag).

So take a set of, say seven colours, and go and calculate the colour contrast between all the other colours in the set
and make a list of those that pass. And if we change any colour, go and redo that calculation...

This sounds about as much fun as hitting your head against a wall, it only feels good when you stop.

Wouldn't it be nice if the computer could do it for us?