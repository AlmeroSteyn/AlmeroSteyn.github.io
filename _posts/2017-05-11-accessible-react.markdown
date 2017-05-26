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
<h1>React</h1>
<img src="/css/images/2017-05-11-accessible-react/react-logo.svg" alt="React logo" style="max-width: 20%"/>
<blockquote>
"A JavaScript library for building user interfaces" - React docs
</blockquote>
</section>
<section>
<h1>JS-Zilla destroys a11y!!</h1>
<img src="/css/images/2017-05-11-accessible-react/godzilla.jpg" alt="Image depicting JavaScript as a destructive monster"/>
</section>
<section>
<h1>It can be a friendly monster...</h1>
<img src="/css/images/2017-05-11-accessible-react/friendly-monster2.jpg" alt="Image depicting JavaScript as cute monster"/>
</section>
<section>
    <h1>JSX</h1>
    <p>HTML-like syntactic JavaScript sugar.</p>
    <pre><code class="html" data-trim>
        <label htmlFor={nameId}>{nameLabelText}</label>
        <input id={nameId} type="text" />
    </code></pre>
    Renders to HTML in the DOM.
    <pre><code class="html" data-trim>
         <label for="name">Darth Vader</label>
         <input id="name" type="text" />
    </code></pre>
</section>
<section>
    <h1>JSX and ARIA</h1>
    <p>All ARIA attributes are valid JSX props!</p>
    <pre><code class="html" data-trim>
            <input id={nameId} aria-label={accessibleLabel} type="text" />
    </code></pre>
    <p>IntelliSense in supported IDEs.</p>
    <img src="/css/images/2017-05-11-accessible-react/IDE-intellisense.png" alt="ARIA attribute IntelliSense in JSX with WebStorm"/>
</section>
<section>
<h1>React component class</h1>
<pre><code class="javascript" data-trim>
import React, { Component } from 'react';

class Demo extends Component {
    render() {
        return (
            <span>{this.props.displayText}</span>
        );
    }
}

export default Demo;

</code></pre>
</section>
<section>
<h1>React component function</h1>
<pre><code class="javascript" data-trim>
import React from 'react';

const Demo = ({ displayText }) => (
    <span>{displayText}</span>
);

export default Demo;
</code></pre>
</section>
<section>
<h1>Using a component</h1>
<pre><code class="javascript" data-trim>
import React from 'react';
import Demo from './Demo';

const Root = () => {(
     &lt;Demo displayText="Show this text"/>
)};

export default Root;
</code></pre>
</section>
<section>
<h1 class="no-capitalize">create-react-app</h1>
<pre><code class="javascript" data-trim>
yarn global add create-react-app
create-react-app my-react-app
cd my-react-app
yarn start
</code></pre>
<ul>
    <li>Webpack production build</li>
    <li>ESLint with some a11y rules</li>
    <li>Progressive app by default</li>
    <li>Supports code splitting</li>
    <li>Unit tests + coverage with JSDOM</li>
</ul>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<blockquote>
"Static AST checker for a11y rules on JSX elements."
</blockquote>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>
</section>
<section>
    <pre><code class="javascript" data-trim>
        if (process.env.NODE_ENV !== 'production') {
            const axe = require('react-axe');
            axe(React, ReactDOM, 1000);
        }
    </code></pre>
</section>