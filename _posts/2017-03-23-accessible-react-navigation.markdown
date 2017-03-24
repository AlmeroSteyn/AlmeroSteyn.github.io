---
layout: post
title:  Accessible React Router navigation.
description: "Make your router transitions visible to everyone"
date:   2017-03-23 16:10:21 -0100
categories: Redux React Javascript A11y Accessibility
---

*This article uses **React 15** with **React Router 4** and **Redux 3** and assumes knowledge of all three. However the concepts explained here
can be applied in any framework or library of your choice.*

Go to my Github profile for <a href="https://github.com/AlmeroSteyn/a11yrouter" target="_blank">a working accessibly routed example</a>. We
will explore this example app further in this article.

As a developer of *Single Page Applications* or *SPA's*, no one needs to tell you how important the **router** of the
application is. It translate the **browser address** into pages and also responds to user input to navigate to various
*pages* or *views* in our application. In a sense, the router can be seen as the heart of our applications.

But, did you know, that quite a few users out there can't see that a navigation from one page to another has taken place?

Surprised? I can't blame you, I mean what can be more clear change in an application than a navigation from one page to the next??!!

So let's look at a very basic routed application created in **React** with the latest current version of **React Router**, namely *v4.0*.

{::nomarkdown}
<figure>
    <img src="/css/images/2017-03-23-accessible-react-navigation/vanillaroutes.png" alt="A basic application with routes">
</figure>
{:/}

And before we dive into the code let's meet a group of users who will have a lot of trouble using this application. And those are
users with visual disabilities.

Users who cannot see well enough to use browsers the way the rest of us do, make use of **Assistive Technologies** called **Screen Readers**.
These are pieces of software that can read back what we normally see on the screen with synthesized voices. This large group of users
depend on the audible version of the websites we make to enjoy the same benefit that other users do.

**Screen readers** are clever enough to read a lot of information that the browser expose, but if no information exists to read out,
the screen reader will remain ominously silent, even if something very important has happened on screen.

Unfortunately, this is the case with many **routers** used in **SPA's** today. **Screen readers** are able to recognise actual
browser navigation very easily as the browser will tell the screen reader that it has navigated to another web page. In the case
of **SPA's**, like those built with **React** or **Angular** the **router** software will take over some of the navigation actions
from the browser in order to control the application without constantly reloading the host **HTML** page.

The result: A totally silent page transition leading to a very confusing experience for these users. Imagine trying to
navigate a web application if you could not even see that the navigation was successful!

You can try this yourself as screen reader software is readily and freely available. If you are viewing this page on a **Mac**,
you already have a screen reader called **VoiceOver** installed. Head over to *Deque University* to see
<a href="https://dequeuniversity.com/screenreaders/voiceover-keyboard-shortcuts" target="_blank">how to use the VoiceOver screen reader</a>.
For those on **Windows**, go grab <a href="https://www.nvaccess.org/" target="_blank">the NVDA screen reader</a> and then head over to *Deque University* to see
<a href="https://dequeuniversity.com/screenreaders/nvda-keyboard-shortcuts" target="_blank">how to use the NVDA screen reader</a>.

**The silence of the screen readers**

The **NVDA** screen reader has a neat *text to speech* mode which I will use to demonstrate what the screen reader would say if
I were to navigate our application above with a vanilla router implementation.

{::nomarkdown}
<figure>
    <img src="/css/images/2017-03-23-accessible-react-navigation/navigationnospeech.png" alt="Image of NVDA text to speech screen showing no mention of navigation in the application">
</figure>
{:/}

As we can see, the screen reader had no problems recognising our navigation links of **Overview**, **Orders** and **Contact**. It sees that
these are in fact HTML link elements and also that we have visited them before. However, the actual navigation actions did not
trigger any response from our screen reader.

This is nowhere near good enough. Not if we want everyone to be able to use our applications. We are looking for a solution that
will open the doors for millions more potential users to use our application. We are also looking for an easy solution, because
making websites for everyone is easier that you think!

We find our solution in the beautiful marriage between **React**, **Redux** and **React Router**.

{:.info}
*NOTE: This problem is not unique to using routing in **React** and as the solution comes from using HTML itself, it will also work in the
framework or library of your choice after adapting it.*

**Setting up our application**

Lets set up a React and Redux application with React Router 4:

{% highlight javascript %}
import React  from 'react';
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Header from './Header';
import Overview from './Overview';
import Contact from './Contact';
import Orders from './Orders';
import rootReducer from './reducers';
import  '../node_modules/bootstrap/dist/css/bootstrap.css';

//The Redux store is created as usual, but we add
//extra configuration to enable the use of the Redux browser dev tools.
//This extra configuration is entirely optional.
const store = createStore(rootReducer,
    window.__REDUX_DEVTOOLS_EXTENSION__ &&
    window.__REDUX_DEVTOOLS_EXTENSION__());

const App = () => (
    <Provider store={store}>
        <div>
            <Router>
                <div>
                    <Header/>
                    <main className="container">
                        <Route exact={true} path="/" component={Overview}/>
                        <Route path="/orders" component={Orders}/>
                        <Route path="/contact" component={Contact}/>
                    </main>
                </div>
            </Router>
        </div>
    </Provider>
);

export default App;
{% endhighlight %}

So, now we have an application that can navigate to three routes, is properly connected to **Redux** and
uses **Bootstrap CSS** for some style.

So, how can we get our application to tell screen readers when a new page has been loaded by the router. And as it turns out,
we find our solution in HTML.

**The magic of ARIA live regions**

As it turns out, making accessible web pages is far from new. Much thought has gone into it by the folks who write the specifications
and those who build the browsers we use. And therefore the **Web Accessibility Initiative - Accessible Rich Internet Applications** or
**WAI-ARIA** recommendation was created by the WC3. You can read about it on the
<a href="https://www.w3.org/TR/wai-aria/" target="_blank">WAI-ARIA recommendation page</a>. To go through the entire thing falls
way way WAY WAY WAY beyond the scope of this article. But we will make use of
<a href="https://www.w3.org/TR/wai-aria/states_and_properties#attrs_liveregions" target="_blank">ARIA live regions</a>.

Basically, these HTML attributes allow us to communicate directly with screen readers. Neat, hey?

An **ARIA live region** is a part of your HTML that will notify screen readers of changes in the content of the HTML.

**Giving the silent a voice**