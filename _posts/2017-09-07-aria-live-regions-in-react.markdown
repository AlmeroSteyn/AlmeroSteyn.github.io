---
layout: post
title: ARIA live in React
description: "Easily add ARIA live regions to your React app"
date:   2017-09-07 16:10:21 -0100
categories: React Javascript A11y Accessibility ARIA aria-live
---

*This article is compatible with **React 15** and above.*

## TLDR;

Ever since my previous article on adding screen reader friendly transition notification to a **React** application using **React Router 4**,
I have been looking for was to simplify the solution. What bothered me most was that the solution depended on introducing **Redux** into
the application, which should not be a prerequisite for an ARIA live solution.

After getting some inspiration from the awesome folks at Deque and their <a href="https://github.com/dequelabs/ngA11y" target="_blank">react-aria-live</a> and
also conquering my fear of using the <a href="https://facebook.github.io/react/docs/context.html" target="_blank">React Context</a> api, I came
up with a solution that I felt was pretty good.

The functionality described in this article has been published as  <a href="https://www.npmjs.com/package/react-aria-live" target="_blank">react-aria-live</a>.

## Why do I need this?

Perhaps we should quickly revisit the reason for adding <a href="https://www.w3.org/TR/wai-aria/states_and_properties#attrs_liveregions" target="_blank">ARIA live regions</a>
to your applications.

In JavaScript applications, like those we create in React, we often find very important changes happening in the application which are completely ignored by
screen readers. This happens as we are manipulating the **HTML DOM** with JavasScript and screen readers are not built to look for these changes and to try
and figure out which ones to announce, but rather to read out the HTML the user is currently focusing on.

Examples of these changes are loading in new routed components and updating import parts of the interface after we have fetched data from the server. Visual users
can see this quite easily, but screen readers users need to be told by the screen reader software that something important has changed in the application.

To fix this, we can create **ARIA live regions** in our applications that, if found by a screen reader, will be monitored and any changes to the content
will be announced to the user.

These regions are simply HTML tags decorated with the ARIA property of `aria-live`. Here is an example of how we could configure such a region:

{% highlight javascript %}
<div aria-live="polite"
     aria-atomic="true"
     aria-relevant="additions">
        **Notification messages goes here**
</div>
{% endhighlight %}

The **aria-live** attribute tells screen readers that they should take note of this block. We normally use this with the **polite** setting as this
will be sufficient to notify users without being too invasive and override the screen reader's responses from their other actions.

The **aria-relevant** attribute
indicates to screen readers which changes in this **div** they should look for and in this case we want to look for the addition of nodes inside the **div**.

Finally the **aria-atomic** attribute is set to **true** to indicate to screen readers that they have to read out the
entire content of the wrapping **div** on every change.

The purpose of the article is not to teach about ARIA live regions, but rather on how to implement it in your React applications, so if you are
super confused at this stage, please backtrack and read the reference at the start of this section before proceeding.

## Making ARIA live regions play nice with React

One of the most important things to keep in mind when making use of an **ARIA live region** is that changes to the content will only be read out by
screen readers if the screen readers already know it exists and if, subsequently, there has been any changes.

This means I cannot render the live region in the DOM for the first time at the moment I want it to dispatch a message to the screen reader. No,
on the initial render in the DOM the inside text is typically ignored by screen readers.

And here comes the caveat in a React application; we need to ensure that the live region is already rendered when we send out first message and that it stays rendered
until we no longer require it.

In a React application it means that the live region needs to exist as high up in the component tree as possible.

{::nomarkdown}
<figure>
    <img src="/css/images/2017-09-07-aria-live-regions-in-react/componenttreeposition.png" alt="Showing a graphical representation of the React component tree from root to children with a lady indicating she pressed a button in the lost child and a man expressing surprise that the ARIA live region should go close to the root.">
</figure>
{:/}

As we can see in the above image, communicating from a child component far down in the tree to the top parent presents challenges in React. And for this reason I chose
**Redux** as solution in my previous article. But we can use the very same *api*  that the **react-redux** implementation uses to solve our problem and that
is the <a href="https://facebook.github.io/react/docs/context.html" target="_blank">React Context</a> api.

We quickly see that the documentation strongly discourages the use of this api and that is true, this is not something you want to implement for