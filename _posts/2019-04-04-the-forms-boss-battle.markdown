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
<img src="/css/images/2019-04-04-the-forms-boss-battle/BHLogo.png" alt="Logo of Binary Horizons" style="max-width: 12%; box-shadow: none; "/>
</div>
<ul>
    <li style="font-size: 1.5em; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 1em; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
</ul>
<div style="text-align: center">
<img src="/css/images/2019-04-04-the-forms-boss-battle/tenon-square-white.png" alt="Logo of Tenon.io" style="max-width: 40%; min-width: 100px; max-height:180px; box-shadow: none; "/>
</div>
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
<iframe src="https://player.vimeo.com/video/328650688" width="840" height="497" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
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
<h1>Buttons should:</h1>
<ul style="text-align:left; list-style: disc">
<li>Tell everyone that it's a button</li>
<li>Be focusable</li>
<li>Active on mouse click</li>
<li>Active on Enter</li>
<li>Active on Spacebar</li>
</ul>

<p>But &lt;div> does not!</p>
</section>