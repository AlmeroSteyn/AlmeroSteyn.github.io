---
layout: slide
title: The Forms Boss Battle... and how to avoid it
description: Creating accessible forms in HTML and React
theme: id24
highlight: tomorrow
transition: none
---

<section class="main">
<h1>The Forms Boss Battle</h1>
<p>... and how to avoid it</p>
<hr>
<div style="display: flex; flex-direction:column;">
<div style="text-align: center">
<img src="/css/images/2019-04-04-the-forms-boss-battle/BHLogo.png" alt="Logo of Binary Horizons" style="max-width: 20%; box-shadow: none; "/>
</div>
<ul>
    <li style="font-size: 1.5em; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 1em; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
</ul>
</div>
</section>
<section class="main">
<h1>1977</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/atari.jpg" alt="Atari gaming console" style="max-width: 70%; box-shadow: none; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Wikimedia Commons licensed under <a style="font-size: 1em;" href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a></figcaption>
</figure>
</section>
<section class="main">
<h1>2019</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/PS4.jpg" alt="Playstation 4 gaming console" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Released into the <a style="font-size: 1em;" href="https://en.wikipedia.org/wiki/Public_domain">Public Domain</a></figcaption>
</figure>
</section>
<section class="main">
<h1>The game boss</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/gameboss.jpg" alt="Screenshot of a console game with a large, scary game boss" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Wikimedia Commons licensed under <a style="font-size: 1em;" href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a></figcaption>
</figure>
</section>
<section class="main">
<h1>It's too difficult!!!</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/anger.jpg" alt="Woman being angry about a difficult game" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Licensed under the <a style="font-size: 1em;" href="https://pixabay.com/service/license/">Pixabay License</a></figcaption>
</figure>
</section>
<section>
<h1>Boss battles on the web</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/loginforminaccessible.jpg" alt="A basic login form with username, password and a login button" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
</section>
<section class="main">
<h1>An inaccessible login form</h1>
<iframe src="https://player.vimeo.com/video/329304374" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>How can something so simple be so broken?</h1>
<pre><code class="html" data-trim>
    <span>Username</span>
    <input />
    <span>Password</span>
    <input />
    <div class="button">
        Login
    </div>
</code></pre>
</section>
<section class="main">
<h1>That button</h1>
<p style="font-size:0.8em;">If it looks like a button and quacks like a button... what should it be?</p>
<pre><code class="html" data-trim>
    <div class="button">
        Login
    </div>
    
    <!-- Or -->
    
    <button>Login</button>
</code></pre>
</section>
<section class="main">
<h1 style="margin-bottom:2em;">Buttons should:</h1>
<div style="display:flex; justify-content: center;">
<ul style="text-align:left; list-style: disc">
<li>Tell everyone that it's a button</li>
<li>Be focusable</li>
<li>Active on mouse click</li>
<li>Active on Enter</li>
<li>Active on Spacebar</li>
</ul>
</div>

<p style="margin-top:2em;">But &lt;div> doesn't do that!</p>
</section>
<section class="main">
<h1>Form accessibility secrets are not shared enough</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/shawntweet.png" alt="Tweet by Shawn Wang stating that he was surprised to only recently learn about button types" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
</section>

<section class="main">
<h1>How about labels?</h1>
<pre><code class="html" data-trim>
    <span>Username</span>
    <input />
</code></pre>
<p style="font-size:0.8em;">The &lt;span> does NOT label the &lt;input>!</p>
<p style="font-size:0.6em;">In other words this &lt;input> has no accessible name</p>
</section>
<section class="main">
<h1>What is the accessible name?</h1>
<blockquote style="font-size: 0.6em; border-left: 3px solid grey; text-align:left; padding-left:1em;">The accessible name is the name of a user interface element. Each platform accessibility API provides the accessible name property. The value of the accessible name may be derived from a visible (e.g., the visible text on a button) or invisible (e.g., the text alternative that describes an icon) property of the user interface element. - <span style="font-weight:bold;">W3C</span></blockquote>
</section>
<section class="main">
<h1>How do i give an input an accessible name?</h1>
<pre><code class="html" data-trim>
<label>
    Username
    <input />
</label>

<label for="username">Username</label>
<input id="username" />

<input aria-label="Username" />

<span id="username">Username</span>
<input aria-labelledby="username" />   
</code></pre>
<p style="font-size:0.8em;">Implicit labelling, explicit labelling, aria-label and aria-labelledby</p>
</section>
<section class="main">
<h1>And the winner is...</h1>
<p style="font-size:0.8em;">Explicit labelling</p>
<pre><code class="html" data-trim>
<label for="username">Username</label>
<input id="username" />
</code></pre>
</section>
<section class="main">
<h1>An accessible login form</h1>
<iframe src="https://player.vimeo.com/video/329332491" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>The WebAIM Million</h1>
<p style="font-size:0.6em;">Accessibility evaluation of the top 1 000 000 home pages</p>
<blockquote style="font-size: 0.6em; border-left: 3px solid grey; text-align:left; padding-left:1em;"><span style="font-weight:bold;">59% of the 3.4 million form inputs identified were unlabeled</span> (either via &lt;label>, aria-label, or aria-labelledby). - <a style="font-weight:bold;" href="https://webaim.org/projects/million/">https://webaim.org/projects/million</a></blockquote>
</section>
<section class="main">
<h1>Don't combine names!</h1>
<p style="font-size:0.8em;">A control should have only one name.</p>
<pre><code class="html" data-trim>
<label for="username">Username</label>
<input id="username" aria-label="Enter a name for your user"/>
</code></pre>
<p style="font-size:0.5em; font-weight:bold;">aria-label overrides the visual label</p>
</section>
<section class="main">
<h1>Think about voice control</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/dragon.png" alt="Box packaging of the Dragon Naturally Speaking software" style="max-width: 30%; box-shadow: none; margin-bottom:0;"/>
<p style="font-size:0.6em;">The accessible name will be used to match commands</p>
</section>
<section class="main">
<h1>What about info texts?</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/infotexts.jpg" alt="A login form showing info text for the username field asking for only characters from the alphabet" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
</section>
<section class="main">
<h1>Meet aria-describedby</h1>
<pre><code class="html" data-trim>
<label for="username">Username</label>
<input id="username" aria-describedby="info"/>

<span id="info">Please use only characters from the alphabet</span>
</code></pre>
</section>
<section class="main">
<h1>Info text in action</h1>
<iframe src="https://player.vimeo.com/video/329794023" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>Client side validation</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/validation.jpg" alt="A login form showing required field validation messages" style="max-width: 80%; box-shadow: none; margin-bottom:0;"/>
</section>
<section class="main">
<h1>Aria-describedby to the rescue again!</h1>
<pre><code class="html" data-trim>
<label for="username">Username</label>
<input id="username" aria-describedby="info error"/>

<span id="info">Please use only characters from the alphabet</span>
<span id="error">A user name is required</span>
</code></pre>
</section>
<section class="main">
<h1>Validation in action</h1>
<iframe src="https://player.vimeo.com/video/329808301" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>This works for all single form elements</h1>
<p>That means also for &lt;textarea>,&lt;input type="checkbox"> and &lt;select></p>
</section>
<section class="main">
<h1>What is ARIA?</h1>
<p>Accessible Rich Internet Applications is a set of attributes that define ways to make web content and web applications (especially those developed with JavaScript) more accessible to people with disabilities.</p>
</section>
<section class="main">
<h1>So I can still have my div button?</h1>
<p>...well yes you can.</p>
<pre><code class="html" data-trim>
    <div class="button"
         role="button"
         tabIndex="0"
         onClick={onclickhandler}
         onKeyDown={onkeydownhandler} >
        Login
    </div>
</code></pre>
</section>
<section class="main">
<h1>There is this "First rule of ARIA"</h1>
<p>If you can use a native HTML element or attribute with the semantics and behavior you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.</p>
</section>
<section class="main">
<h1>Rebuilding things is harder than re-using things</h1>
<blockquote style="font-size: 0.6em; border-left: 3px solid grey; text-align:left; padding-left:1em;"><span>Home pages with ARIA present averaged 11.2 more detectable errors than pages without ARIA.</span> - <a style="font-weight:bold;" href="https://webaim.org/projects/million/">https://webaim.org/projects/million</a></blockquote>
</section>
<section class="main">
<h1>What about groups of controls?</h1>
<pre><code class="html" data-trim>
    <label>Choose your favourite time of day</label>
    
    <input id="rMorning" type="radio" name="favTime" value="morning" />
    <label for="rMorning">Morning</label>
    <input id="rNoon" type="radio" name="favTime" value="noon" />
    <label for="rNoon">Noon</label>
    <input id="rNight" type="radio" name="favTime" value="night" />
    <label for="rNight">Night</label>
</code></pre>
<p>Labels can only be linked to ONE control.</p>
</section>
<section class="main">
<h1>Introducing the fieldset</h1>
<p>Here we label with the &lt;legend> tag</p>
<pre><code class="html" data-trim>
<fieldset>
    <legend>Choose your favourite time of day</legend>
    
    <input id="rMorning" type="radio" name="favTime" value="morning" />
    <label for="rMorning">Morning</label>
    <input id="rNoon" type="radio" name="favTime" value="noon" />
    <label for="rNoon">Noon</label>
    <input id="rNight" type="radio" name="favTime" value="night" />
    <label for="rNight">Night</label>
</fieldset>    
</code></pre>
<p style="font-size:0.6em;">The &lt;legend> tag HAS to be immediately after the &lt;fieldset> tag!</p>
</section>
<section class="main">
<h1>But what about aria-describedby?</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/noariadescribed.jpg" alt="Road sign with multiple arrows in multiple directions all ending up at the word NO" style="max-width: 60%; box-shadow: none; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">CC0 Public Domain</figcaption>
</figure>
<p style="font-size:0.75em;">Attaching aria-describedby to &lt;fieldset> or &lt;legend> is not supported in many screen readers</p>  
</section>
<section class="main">
<h1>How do I validate groups then?</h1>
<pre><code class="html" data-trim>
<fieldset>
    <legend>
        <span>Choose your favourite time of day</span>
        <span>You have not chosen a favourite time</span>
    </legend>
    
    <input id="rMorning" type="radio" name="favTime" value="morning" />
    <label for="rMorning">Morning</label>
    <input id="rNoon" type="radio" name="favTime" value="noon" />
    <label for="rNoon">Noon</label>
</fieldset>    
</code></pre>
<p style="font-size:0.8em;">Add text to the legend.</p> 
<p style="font-size:0.7em;">This means it can also be used for info texts!</p>
</section>
<section class="main">
<h1>You don't want your error texts next to your labels?</h1>
<p style="font-size:0.8em;">Move with CSS... or:</p>
<pre><code class="html" data-trim>
<fieldset>
    <legend>
        <span>Choose your favourite time of day</span>
        <span class="visually-hidden">
            You have not chosen a favourite time
        </span>
    </legend>
    
    <input id="rMorning" type="radio" name="favTime" value="morning" />
    <label for="rMorning">Morning</label>
    //...
    <span aria-hidden="true">
        You have not chosen a favourite time
    </span>
</fieldset>    
</code></pre>
</section>
<section class="main">
<h1>Visually hiding things</h1>
<pre><code class="css" data-trim>
.visually-hidden:not(:focus):not(:active) {
  clip: rect(0 0 0 0); 
  clip-path: inset(100%);
  height: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap; 
  width: 1px;
}
</code></pre>
<a style="font-size:0.5em;" href="https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html">https://www.scottohara.me/blog/2017/04/14/inclusively-hidden.html</a>
</section>
<section class="main">
<h1>A fieldset in action</h1>
<iframe src="https://player.vimeo.com/video/333546508" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>Never lose the focus outline</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/focus.png" alt="Road sign with multiple arrows in multiple directions all ending up at the word NO" style="max-width: 60%; box-shadow: none; margin-bottom:0;"/>
<p style="font-size:0.6em;">Don't do this!</p>
<pre><code class="css" data-trim>
    outline: none;
    outline: 0;
</code></pre>
<p style="font-size:0.6em;">Unless you provide your own focus outline style in the CSS</p>
</section>



