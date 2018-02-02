---
layout: slide
title: Breaking the silence
description: Screen readers and React apps
theme: ramst
highlight: tomorrow
transition: none
---

<section class="main" data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<img src="/css/images/2018-01-25-breaking-the-silence/QDelft_logo.svg" alt="Log of QDelft" style="max-width: 40%; box-shadow: none; background-color: transparent; "/>
<h1>Breaking the silence</h1>
<h2>Screen readers and React apps</h2>
<hr>
<ul>
    <li style="font-size: 47px; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 30px; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
    <li style="font-size: large; margin-top: 20px;">Custom images: Kalina Hristova</li>
</ul>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>React a11y docs</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/reactdocs.png" alt="Screenshot of the React accessibility docs" style="max-width: 85%;"/>
<a href="https://reactjs.org/docs/accessibility.html">reactjs.org/docs/accessibility.html</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithoutAriaAndFocus.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>Routing is a11y silent</h1>
<pre><code class="javascript" data-trim>
const AppMain = () =>
  <main>
    &lt;Switch>
      <Route path="/todos" component={Todos} />
      <Route path="/todo" component={Todo} />
      <Route path="/contact" component={Contact} />
      &lt;Redirect to="/todos" />
    &lt;/Switch>
  </main>;
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithoutAriaWithFocus.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>ARIA live</h1>
<pre><code class="javascript" data-trim data-noescape>
const Announcer = ({ message }) =>
  &lt;div aria-live="polite"
       aria-atomic="true"
       aria-relevant="additions">
    {message}
  &lt;/div>;
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>ARIA live and the component tree</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/arialive.png" alt="Illustrates that the aria live region is more stable when rendered in the root component."/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>ARIA live announcer</h1>
<pre><code class="javascript" data-trim>
//...
import { LiveAnnouncer, LiveMessage } from 'react-aria-live';
//...
render() {
return (
  &lt;LiveAnnouncer>
    &lt;LiveMessage message={this.state.a11yMessage}
                 aria-live="polite" />
    {this.props.children}
  &lt;/LiveAnnouncer>
  );
}
//..
</code></pre>
<a href="https://github.com/AlmeroSteyn/react-aria-live">github.com/AlmeroSteyn/react-aria-live</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithAria.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>

<section class="main" data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroom.jpg">
<h1>Questions</h1>
<hr>
<p>Presentation online at:</p>
<a href="http://almerosteyn.com/slides/">almerosteyn.com/slides/</a>
<hr>
<ul>
    <li style="font-size: 47px; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 30px; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
    <li style="font-size: large; margin-top: 20px;">Custom images: Kalina Hristova</li>
</ul>
</section>
