---
layout: slide
title: Inclusive React
description: A survival guide
theme: adventure
highlight: tomorrow
transition: none
---

<section class="no-background" data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<img class="nomax" src="/css/images/2018-04-11-inclusive-react/titletext.svg" style="background-color:transparent; -webkit-transform: scale(1.2);transform: scale(1.2);" alt="Adventure style text saying Inclusive React a survival guide over a forest backdrop."/>
</section>
<section class="no-background" data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<img class="nomax" src="/css/images/2018-04-11-inclusive-react/nametextbanner.svg" style="background-color:transparent;" alt="Adventure style text saying Almero Steyn with a twitter handle of @Kryptos_RSA and his blog address of almerosteyn.com."/>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>Get your QR-code scanner apps ready!</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/qrscanner.jpg" alt="Telephone used as QR code scanner."/>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>Inaccessible things are out of reach</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/lockedgate.jpg" alt="Rusted old lock and chain in a wooden door so unused it has spider webs."/>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<div class="flex-grid">
<div class="flex-col" style="background: transparent;" >
<h1 style="text-align: center; margin: 0;">Inaccessible</h1>
</div>
<div class="flex-col" style="background: transparent;" >
<h1 style="text-align: center; margin: 0;">Accessible</h1>
</div>
</div>
<div class="flex-grid">
            <pre class="flex-col"><code class="css" data-trim>
:focus {
    outline: 0; //Or none
}
            </code></pre>
       <pre class="flex-col"><code class="css" data-trim>
       :focus {
          // Some visual style
       }
                   </code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<span>Name:</span>

<input type="text" />
</code></pre>
<pre class="flex-col"><code class="html" data-trim>
&lt;label htmlFor="nameInput">
    Name:
</label>

<input id="nameInput" type="text" />
</code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<button>
    &lt;i className="save-icon" />
</button>
</code></pre>
<pre class="flex-col"><code class="html" data-trim>
<button aria-label="Save">
    &lt;i className="save-icon"
       aria-hidden="true" />
</button>
</code></pre>
</div>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<div class="flex-grid">
<div class="flex-col" style="background: transparent;" >
<h1 style="text-align: center; margin: 0;">Inaccessible</h1>
</div>
<div class="flex-col" style="background: transparent;" >
<h1 style="text-align: center; margin: 0;">Accessible</h1>
</div>
</div>
<div class="flex-grid">
             <pre class="flex-col" ><code class="html" data-trim>
            <div className="looks-like-button"
                 onClick={onClickHandler}>
                 Press Me
            </div>
                   </code></pre>
        <pre class="flex-col" ><code class="html" data-trim>
        <button onClick={onClickHandler}>
             Press Me
        </button>
               </code></pre>
</div>
<div class="flex-grid">
<pre class="flex-col"><code class="html" data-trim>
<a onClick={onClickHandler}>
    Click me
</a>
</code></pre>
<pre class="flex-col"><code class="html" data-trim>
<a href="/some/application/url">
    Navigate somewhere
</a>
</code></pre>
</div>
<div class="flex-grid">
<div class="flex-col code-shadow" >
<img src="/css/images/2018-04-11-inclusive-react/badcontrastbutton.png" alt="A button with dark blue text on a darker blue background showing bad contrast." style="box-shadow: none;"/>
</div>
<div class="flex-col code-shadow" >
<img src="/css/images/2018-04-11-inclusive-react/goodcontrastbutton.png" alt="A button with dark blue text on a light blue background showing good contrast." style="box-shadow: none;"/>
</div>
</div>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>We need a Swiss Army Knife</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/knife.jpg" alt="Swift army knife with blades and tools open."/>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>The React Accessibility Doc</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/reactdocs.png" alt="Screen capture of the React accessibility docs page."/>
<img src="/css/images/2018-04-11-inclusive-react/a11ydocsqr.svg" alt="QR code for url reactjs.org/docs/accessibility.html" style="width:5em;height: 5em;"/>
<a href="https://reactjs.org/docs/accessibility.html">reactjs.org/docs/accessibility.html</a>
</section>
<section class="no-background" data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<div style="display:flex;">
<div style="flex:10;">
<img class="nomax " src="/css/images/2018-04-11-inclusive-react/wai.svg" style="background-color:transparent;" alt="Text image spelling WAI-ARIA."/>
</div>
<div style="flex:7;">
<img class="nomax " src="/css/images/2018-04-11-inclusive-react/a11y.svg" style="background-color:transparent; margin-top: 100px; transform: rotate(-20deg); " alt="Text image spelling A11Y."/>
</div>
</div>
<div style="display:flex;">
<div style="flex:12;">
<img class="nomax " src="/css/images/2018-04-11-inclusive-react/wcag.svg" style="background-color:transparent;  " alt="Text image spelling WCAG."/>
</div>
<div style="flex:8;">
<img class="nomax " src="/css/images/2018-04-11-inclusive-react/confused.png" style="background-color:transparent;" alt="Text image spelling WAI-ARIA."/>
</div>

</div>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>WCAG</h1>
<h2 style="font-size: 1.4em; margin: 15px;">Web Content Accessibility Guidelines</h2>
<blockquote style="font-size: 0.8em;">Defines how to make Web content more accessible to all people.</blockquote>
<img src="/css/images/2018-04-11-inclusive-react/webaimwcagqr.svg" alt="QR code for url webaim.org/standards/wcag/checklist" style="width:5em;height: 5em;"/>
<br />
<a href="https://webaim.org/standards/wcag/checklist">webaim.org/standards/wcag/checklist</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>WAI - ARIA</h1>
<h2 style="font-size: 1.4em; margin: 15px;">Web Accessibility Initiative – Accessible Rich Internet Applications</h2>
<blockquote style="font-size: 0.8em;">Specifies how to increase the accessibility of web applications.</blockquote>
<img src="/css/images/2018-04-11-inclusive-react/waiariaqr.svg" alt="QR code for url https://www.w3.org/TR/wai-aria-practices-1.1/" style="width:5em;height: 5em;"/>
<br />
<a href="https://www.w3.org/TR/wai-aria-practices-1.1/">www.w3.org/TR/wai-aria-practices-1.1/</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>Semantic JSX and HTML</h1>
<div class="flex-grid">
<pre class="flex-col">
<h2 style="font-family: Verdana; text-align: center; margin: 0; font-weight: bold; border-bottom-color: black; border-bottom-width: 2px; border-bottom-style: solid; padding-bottom: 10px;">Non-semantic</h2>
<code class="html" data-trim>
<div>
    &lt;Navigation />
</div>
<div>
    &lt;SideMenu />
</div>
<div>
    &lt;MainContent />
    <div className="like-button"
         onClick={onClickHandler}>
         Save selection
    </div>
</div>
</code></pre>
<pre class="flex-col">
<h2 style="font-family: Verdana; text-align: center; margin: 0; font-weight: bold; border-bottom-color: black; border-bottom-width: 2px; border-bottom-style: solid; padding-bottom: 10px;">Semantic</h2>
<code class="html" data-trim>
<nav>
    &lt;Navigation />
</nav>
<aside>
    &lt;SideMenu />
</aside>
<main>
    &lt;MainContent />
    <button type="button"
            onClick={onClickHandler}>
         Save selection
    </button>
</main>
</code></pre>
</div>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>HTML !== &lt;div></h1>
<img class="nomax" src="/css/images/2018-04-11-inclusive-react/chest.png" style="background-color:transparent; box-shadow: none; width: 50%;" alt="Treasure chest spilling gold."/>
<img src="/css/images/2018-04-11-inclusive-react/semanticqr.svg" alt="QR code for url https://developer.mozilla.org/en-US/docs/Web/HTML/Element" style="width:5em;height: 5em;"/>
<a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element" style="font-size: 0.8em;">developer.mozilla.org/en-US/docs/Web/HTML/Element</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>Test with your keyboard</h1>
<blockquote>Use TAB, SHIFT + TAB, ENTER and the arrow keys.</blockquote>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/keyboard.jpg" style="width:50%;" alt="Keyboard with blue backlighting."/>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>eslint-plugin-jsx-a11y</h1>
<img class="shadow nomax" src="/css/images/2018-04-11-inclusive-react/jsxa11yIDE.png" style="margin-left:15px" alt="Screen capture of eslint-plugin-jsx-a11y IDE integration."/>
<br />
<img src="/css/images/2018-04-11-inclusive-react/jsxa11yqr.svg" alt="QR code for url github.com/evcohen/eslint-plugin-jsx-a11y" style="width:5em;height: 5em; margin-left: 60px;"/>
<br />
<a href="https://github.com/evcohen/eslint-plugin-jsx-a11y">github.com/evcohen/eslint-plugin-jsx-a11y</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>aXe and axe-core</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/axe.png" style="width:50%;" alt="Screen capture of aXe audit in browser."/>
<img src="/css/images/2018-04-11-inclusive-react/axeqr.svg" alt="QR code for url www.deque.com/axe" style="width:5em;height: 5em; margin-left: 60px;"/>
<br />
<a href="https://www.deque.com/axe/">www.deque.com/axe</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>react-axe</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/react-axe.png" style="width:80%; margin-left: 20px;" alt="Screen capture of aXe audit in browser."/>
<img src="/css/images/2018-04-11-inclusive-react/react-axeqr.svg" alt="QR code for url github.com/dequelabs/react-axe" style="width:5em;height: 5em; margin-left: 15px;"/>
<br />
<a href="https://github.com/dequelabs/react-axe">github.com/dequelabs/react-axe</a>
</section>
<section data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<h1>Test with screen readers</h1>
<img class="shadow" src="/css/images/2018-04-11-inclusive-react/reader.jpg" style="width:80%; margin-left: 20px;" alt="Computer with headphones to listen to text speech."/>
<img src="/css/images/2018-04-11-inclusive-react/screenreaderqr.svg" alt="QR code for url reactjs.org/docs/accessibility.html#screen-readers" style="width:5em;height: 5em; margin-left: 15px;"/>
<br />
<a href="https://reactjs.org/docs/accessibility.html#screen-readers" style="font-size: 0.8em;">reactjs.org/docs/accessibility.html#screen-readers</a>
</section>
<section class="no-background" data-background-image="/css/images/2018-04-11-inclusive-react/backgroundcolor2.jpg">
<img class="nomax" src="/css/images/2018-04-11-inclusive-react/trailingtext.svg" style="background-color:transparent;" alt="Adventure style text saying Inclusive React a survival guide over a forest backdrop. Also has a QR code to url almerosteyn.com/slides"/>
<a href="http://almerosteyn.com/slides/" style="color:white;">almerosteyn.com/slides/</a>
<p style="color: white; font-size: 0.3em;">Images CC0 - Pixabay</p>
</section>