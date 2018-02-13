---
layout: slide
title: Breaking the silence
description: Screen readers and React apps
theme: ramst
highlight: tomorrow
transition: none
---

<section class="main" data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<img src="/css/images/2018-01-25-breaking-the-silence/QDelft_logo.svg" alt="Log of QDelft" style="max-width: 40%; box-shadow: none; background-color: transparent; "/>
<h1>Breaking the silence</h1>
<h2>Screen readers and React apps</h2>
<hr>
<ul>
    <li style="font-size: 47px; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 30px; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
</ul>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>Inclusive Design</h1>
<blockquote>The design of mainstream products and/or services that are accessible to, and usable by, as many people as reasonably possible... - British Standards Institute</blockquote>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>React a11y docs</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/reactdocs.png" alt="Screenshot of the React accessibility docs" style="max-width: 85%;"/>
<a href="https://reactjs.org/docs/accessibility.html">reactjs.org/docs/accessibility.html</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>The screen reader</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/JAWS.png" alt="JAWS logo" style="max-height: 100px;"/><br/>
<a href="http://www.freedomscientific.com/Products/Blindness/JAWS" style="font-size:24px;">www.freedomscientific.com/Products/Blindness/JAWS</a><br/>
<img src="/css/images/2018-01-25-breaking-the-silence/nvda.png" alt="NVDA logo" style="max-height: 100px;"/><br/>
<a href="https://www.nvaccess.org/" style="font-size:24px;">www.nvaccess.org</a><br/>
<img src="/css/images/2018-01-25-breaking-the-silence/VoiceOver.png" alt="VoiceOver logo" style="max-height: 100px;"/><br/>
<a href="https://www.apple.com/lae/accessibility/mac/vision/" style="font-size:24px;">www.apple.com/lae/accessibility/mac/vision</a><br/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>The dark room</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/torch.jpg" alt="Screenshot of the React accessibility docs" style="max-width: 85%;"/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>App with accessible HTML</h1>
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithoutAriaAndFocus.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>Well, that's still unusable!</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/confused.jpg" alt="Jacky Chan very shocked about how unusable this is" style="max-width: 85%;"/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>Routing is silent</h1>
<pre><code class="javascript" data-trim>
const AppMain = () =>
  <main>
    &lt;Switch>
      <Route path="/tasks" component={Tasks} />
      <Route path="/task" component={Task} />
      <Route path="/contact" component={Contact} />
      &lt;Redirect to="/tasks" />
    &lt;/Switch>
  </main>;
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>So are other important updates and messages...</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/errors.png" alt="Application input errors are not read out" style="max-width: 85%;"/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomwide.jpg">
<h1>Dearest user, you're not welcome!</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/unwelcome.jpg" alt="Unwelcome looking gate in arid landscape with barbed wire saying keep gate closed and locked" style="max-width: 85%;"/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Set focus after navigation</h1>
<pre><code class="javascript" data-trim data-noescape>
class PageFocusSection extends Component {
  componentDidMount() {
    <mark>this.header.focus()</mark>;
  }
  render() {
    const { children, headingText } = this.props;
    return (&lt;section>
        <h2 tabIndex="-1"
            <mark>ref={header => {this.header = header;}}</mark>>
          {headingText}
        </h2>
        {children}
      &lt;/section>);
  }
}
</code></pre>
<a href="https://reactjs.org/docs/refs-and-the-dom.html">reactjs.org/docs/refs-and-the-dom.html</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Adding Focus Control</h1>
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithoutAriaWithFocus.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>ARIA live regions to the rescue!</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/important.jpg" alt="Person shouting an important message through a loudspeaker" style="max-width: 85%;"/>
<a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions" style="font-size:24px;">developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>ARIA live</h1>
<pre><code class="javascript" data-trim data-noescape>
const Announcer = ({ message }) =>
  &lt;div role="log" 
       aria-live="polite" 
       aria-relevant="additions" 
       aria-atomic="true"> 
    {message}
  &lt;/div>;
  
  //Possible values
  //role:          log | status | alert 
  //aria-live:     polite | assertive | off
  //aria-relevant: additions | removals | text | all
  //aria-atomic:   true | false
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Error announcer!</h1>
<pre><code class="html" data-trim data-noescape>
    <label htmlFor={inputId}>{labelText}</label>
    <input
      id={inputId}
      aria-invalid={showErrors}
      aria-describedby={showErrors ? describedById : null}
      onChange={onChangeHandler}
      value={value} />
    {showErrors ?
      &lt;div
        id={describedById}
        aria-live="polite"
        aria-atomic="true">
          {errorText}
      &lt;/div> 
     : null}
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Our live region in JAWS</h1>
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/ErrorAriaJAWS.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>So we are done right?</h1>
<h2>Right?!</h2>
<h3>Why are you building the tension??!!</h3>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Our live region in NVDA</h1>
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/ErrorAriaNVDA.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>Stable error announcer!</h1>
<pre><code class="html" data-trim data-noescape>
 <label htmlFor={inputId}>{labelText}</label>
 <input
   id={inputId}
   aria-invalid={!showErrors}
   aria-describedby={showErrors ? this.describedById : null}
   onChange={onChangeHandler}
   value={value} />
 &lt;div
   aria-live="polite"
   aria-atomic="true">
   {showErrors ? 
     <span id={describedById}>{errorText}</span> 
   : null}
 &lt;/div>
</code></pre>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/darkroomdoublewide.jpg">
<h1>ARIA live and the component tree</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/arialive.png" alt="Illustrates that the aria live region is more stable when rendered in the root component."/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/brightroom.jpg">
<h1 style="color: #15191C;">Let's light up that dark room!</h1>
<img src="/css/images/2018-01-25-breaking-the-silence/lightup.png" alt="Light bulb plugging itself in to give more light."/>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/brightroom.jpg">
<h1 style="color: #15191C;">ARIA live announcer</h1>
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
<a href="https://github.com/AlmeroSteyn/react-aria-live" style="color: #15191C;">github.com/AlmeroSteyn/react-aria-live</a>
</section>
<section data-background-image="/css/images/2018-01-25-breaking-the-silence/brightroom.jpg">
<h1 style="color: #15191C;">Full screen reader a11y!</h1>
 <video controls class="stretch" src="/css/videos/2018-01-25-breaking-the-silence/WithAria.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>

<section class="main" data-background-image="/css/images/2018-01-25-breaking-the-silence/brightroom.jpg" style=" background-color:rgba(0,0,0,0.8);">
<h1>Questions</h1>
<hr>
<p>Presentation online at:</p>
<a href="http://almerosteyn.com/slides/" >almerosteyn.com/slides/</a>
<p style="font-size: 24px; margin-bottom: -10px; margin-top: 40px;">Example app at:</p>
<a href="https://github.com/AlmeroSteyn/react-a11y-patterns/tree/react-amsterdam-talk" style="font-size: 24px;" >github.com/AlmeroSteyn/react-a11y-patterns/tree/react-amsterdam-talk</a>
<hr>
<ul>
    <li style="font-size: 47px; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 30px; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
</ul>
</section>
