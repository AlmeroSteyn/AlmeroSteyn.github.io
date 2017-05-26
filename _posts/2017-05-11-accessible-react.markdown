---
layout: slide
title: Accessibility in React
description: Building accessible React apps
theme: present
highlight: tomorrow
transition: fade
---

<section id="main">
<h1>Accessibility in React</h1>
<hr>
<h2>Creating accessible applications</h2>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>
<section>
<h1>JS-Zilla destroys a11y!!</h1>
<img src="/css/images/2017-05-11-accessible-react/godzilla.jpg" alt="Image depicting JavaScript as a destructive monster"/>
</section>
<section>
<h1>JS-Zilla destroys a11y!!</h1>
<img src="/css/images/2017-05-11-accessible-react/friendly-monster2.jpg" alt="Image depicting JavaScript as cute monster"/>
</section>
<section>
    <pre><code class="javascript" data-trim>
        if (process.env.NODE_ENV !== 'production') {
            const axe = require('react-axe');
            axe(React, ReactDOM, 1000);
        }
    </code></pre>
</section>