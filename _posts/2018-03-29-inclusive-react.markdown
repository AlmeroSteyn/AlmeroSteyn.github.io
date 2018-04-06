---
layout: slide
title: Inclusive React
description: A survival guide
theme: adventure
highlight: tomorrow
transition: none
---

<section class="no-background" data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<img class="nomax" src="/css/images/2018-03-29-inclusive-react/titletext.svg" style="background-color:transparent; -webkit-transform: scale(1.2);transform: scale(1.2);" alt="Adventure style text saying Inclusive React a survival guide over a forest backdrop."/>
</section>
<section class="no-background" data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<img class="nomax" src="/css/images/2018-03-29-inclusive-react/nametextbanner.svg" style="background-color:transparent;" alt="Adventure style text saying Almero Steyn with a twitter handle of @Kryptos_RSA and his blog address of almerosteyn.com."/>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>Get your QR-code scanner apps ready!</h1>
<img class="shadow" src="/css/images/2018-03-29-inclusive-react/qrscanner.jpg" alt="Telephone used as QR code scanner."/>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>Inaccessible things are out of reach</h1>
<img class="shadow" src="/css/images/2018-03-29-inclusive-react/lockedgate.jpg" alt="Rusted old lock and chain in a wooden door so unused it has spider webs."/>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>Blocking errors</h1>
<div class="flex-grid">
            <pre class="flex-col"><code class="css" data-trim>
:focus {
    outline: 0; //Or none
}
            </code></pre>
        <pre class="flex-col" ><code class="html" data-trim>
<div class="like-button"
     onClick={onClickHandler}>
     Press Me
</div>
       </code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<span>Name:</span>

<input type="text" />
</code></pre>
<pre class="flex-col"><code class="html" data-trim>
<a onClick={onClickHandler}>
    Click me
</a>
</code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<button>
    &lt;i class="save-icon"></i>
</button>
</code></pre>
<div class="flex-col code-shadow" >
<img src="/css/images/2018-03-29-inclusive-react/badcontrastbutton.png" alt="A button with dark blue text on a darker blue background showing bad contrast." style="box-shadow: none;"/>
</div>
</div>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>Blocking errors fixed!</h1>
<div class="flex-grid">
            <pre class="flex-col"><code class="css" data-trim>
:focus {
   // Some visual style
}
            </code></pre>
        <pre class="flex-col" ><code class="html" data-trim>
<button onClick={onClickHandler}>
     Press Me
</button>
       </code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
&lt;label htmlFor="nameInput">
    Name:
</label>

<input id="nameInput" type="text" />
</code></pre>
<pre class="flex-col"><code class="html" data-trim>
<a href="/some/application/url">
    Click me
</a>
</code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<button aria-label="Save">
    &lt;i class="save-icon"
       aria-hidden="true" />
</button>
</code></pre>
<div class="flex-col code-shadow" >
<img src="/css/images/2018-03-29-inclusive-react/goodcontrastbutton.png" alt="A button with dark blue text on a light blue background showing good contrast." style="box-shadow: none;"/>
</div>
</div>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>We need a Swiss Army Knife</h1>
<img class="shadow" src="/css/images/2018-03-29-inclusive-react/knife.jpg" alt="Swift army knife with blades and tools open."/>
</section>
<section data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<h1>The React Accessibility Doc</h1>
<img class="shadow" src="/css/images/2018-03-29-inclusive-react/reactdocs.png" alt="Screen capture of the React accessibility docs page."/>
<img src="/css/images/2018-03-29-inclusive-react/a11ydocsqr.svg" alt="QR code for url reactjs.org/docs/accessibility.html" style="width:5em;height: 5em;"/>
<a href="https://reactjs.org/docs/accessibility.html">reactjs.org/docs/accessibility.html</a>
</section>
<section class="no-background" data-background-image="/css/images/2018-03-29-inclusive-react/backgroundcolor2.jpg">
<div style="display:flex;">
<div style="flex:5;">
<img class="nomax fragment" src="/css/images/2018-03-29-inclusive-react/wcag.svg" style="background-color:transparent;  transform: rotate(20deg);" alt="Text image spelling WCAG."/>
</div>
<div style="flex:10;">
<img class="nomax fragment" src="/css/images/2018-03-29-inclusive-react/wai.svg" style="background-color:transparent; transform: rotate(-20deg);" alt="Text image spelling WAI-ARIA."/>
</div>
</div>
<img src="/css/images/2018-03-29-inclusive-react/a11y.svg" style="background-color:transparent; height: 20%; width: 20%" alt="Text image spelling A11Y"/>
<div style="display:flex;">
<div style="flex:12;">
<img class="nomax fragment" src="/css/images/2018-03-29-inclusive-react/focus.svg" style="background-color:transparent; transform: rotate(10deg);" alt="Text image spelling Focus Control."/>
</div>
<div style="flex:7;">
<img class="nomax fragment" src="/css/images/2018-03-29-inclusive-react/axe.svg" style="background-color:transparent; transform: rotate(-20deg);" alt="Text image spelling AXE."/>
</div>
</div>
</section>