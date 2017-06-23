---
layout: slide
title: React Accessibility
description: Tooling and techniques
theme: present
highlight: tomorrow
transition: fade
---

<section class="main">
<img src="/css/images/2017-06-14-accessible-react/QLogo.png" alt="Log of QDelft" style="max-width: 20%"/>
<h1>React Accessibility</h1>
<hr>
<h2>Tooling and techniques</h2>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
<aside class="notes">
<ul>
<li>I'm Almero Steyn</li>
<li>South african - Netherlands for 5 years</li>
<li>Work at QDelft as Senior Developer</li>
<li>Projects for the government: Accessibility</li>
<li>R&D about web tech and accessibility in these techs</li>
</ul>
</aside>
</section>
<section>
<h1>React</h1>
<img src="/css/images/2017-06-14-accessible-react/react-logo.svg" alt="React logo" style="max-width: 20%"/>
<blockquote>
"A JavaScript library for building user interfaces." - React docs
</blockquote>
<aside class="notes">
<ul>
<li>Created by Jordan Walke at Facebook</li>
<li>Opensourced in 2013</li>
<li>A library instead of a framework</li>
<li>Build applications with components</li>
</ul>
</aside>
</section>
<section>
<h1>React syntax</h1>
<pre><code class="javascript" data-trim>
import React from 'react';
import Content from './Content';

const Root = ({headerText, onLogout}) => (
     <main>
        <h1>{ headerText }</h1>
        &lt;Content onLogout={ onLogout }/>
     </main>
);

export default Root;
</code></pre>
<aside class="notes">
<ul>
<li>React component are pure JavaScript</li>
<li>Returns view from JavaScript</li>
<li>Create a tree of components by passing properties and events</li>
<li>Renders to JavaScript enhanced HTML in the browser via the reconciler</li>
</ul>
</aside>
</section>
<section>
<h1>Everything in JavaScript?</h1>
<img src="/css/images/2017-06-14-accessible-react/shock.jpg" alt="Image of koala expressing shock at React being all JavaScript" style="max-width:40%"/>
</section>
<section>
<h1>JS-Zilla destroys a11y!!</h1>
<img src="/css/images/2017-06-14-accessible-react/godzilla.jpg" alt="Image depicting JavaScript as a destructive monster"/>
</section>
<section>
<h1>It can be a friendly monster...</h1>
<img src="/css/images/2017-06-14-accessible-react/friendly-monster2.jpg" alt="Image depicting JavaScript as cute monster"/>
<aside class="notes">
<ul>
<li>BREATHE!!!!!!</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">create-react-app</h1>
<pre><code class="javascript" data-trim>
yarn global add create-react-app
create-react-app my-react-app
cd my-react-app
yarn start
</code></pre>
<ol>
    <li>Webpack development and production build.</li>
    <li>ESLint with some a11y rules.</li>
    <li>Progressive app by default.</li>
    <li>Supports code splitting.</li>
    <li>Unit tests + coverage with JSDOM.</li>
</ol>
<aside class="notes">
<ul>
<li>I recommended this CLI maintained by React team members</li>
<li>Solid app development ecosystem ready for a11y</li>
<li>Contains some a11y linter rules by default</li>
</ul>
</aside>
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
<aside class="notes">
<ul>
<li>JSX is syntactic sugar</li>
<li>Only looks like HTML</li>
<li>Renders to clean HTML DOM without custom elements</li>
</ul>
</aside>
</section>
<section>
    <h1>JSX and ARIA</h1>
    <p>All ARIA attributes are valid JSX props!</p>
    <pre><code class="html" data-trim>
            <input id={nameId} aria-label={accessibleLabel} type="text" />
    </code></pre>
    <p>IntelliSense in supported IDEs.</p>
    <img src="/css/images/2017-06-14-accessible-react/IDE-intellisense.png" alt="ARIA attribute IntelliSense in JSX with WebStorm"/>
<aside class="notes">
<ul>
<li>JSX supports ARIA in the same way as HTML</li>
<li>Added ability to change aria-props programmatically</li>
<li>Allows for IDE support</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<blockquote>
"Static AST checker for a11y rules on JSX elements."
</blockquote>
<a href="https://github.com/evcohen/eslint-plugin-jsx-a11y">https://github.com/evcohen/eslint-plugin-jsx-a11y</a>
<aside class="notes">
<ul>
<li>Plugin for ESLINT</li>
<li>Checks JSX for a11y issues</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>More than 30 ESLINT a11y checks.</p>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/jsxa11y.png" alt="Image of some rules in the eslint-jsx-a11y plugin"/>
<aside class="notes">
<ul>
<li>More than 30 accessibility checks</li>
<li>Growing and evolving</li>
<li>Actively maintained</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>Rules are configurable.</p>
    <pre><code class="json" data-trim>
       {
         "rules": {
           "jsx-a11y/rule-name": "warn"
         }
       }
    </code></pre>
<p>Extending config in create-react-app.</p>
 <pre><code class="json" data-trim>
        {
          "extends": ["react-app", "plugin:jsx-a11y/recommended"],
          "plugins": ["jsx-a11y"]
        }
    </code></pre>
<aside class="notes">
<ul>
<li>Configurable both plugin and rule level</li>
<li>Create-react-app config can be extended by ejecting or to display in IDE</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>A11y issues become build warnings.</p>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/jsxa11ywebpack.png" alt="Shows eslint-jsx-a11y error feedback in create-react-app build"/>
<aside class="notes">
<ul>
<li>Can be hooked into WebPack build like in create-react-app</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>IDE integration.</p>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/jsxa11yIDE.png" alt="Shows eslint-jsx-a11y error feedback in an IDE"/>
<aside class="notes">
<ul>
<li>Can be integrated with IDE's to provide instant feedback</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">react-axe</h1>
<blockquote>
"Accessibility auditing for React.js applications."
</blockquote>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/axe-core.png" alt="React-axe uses axe-core. Shows axe-core logo." style="max-width: 50%;"/>
<a href="https://github.com/dequelabs/react-axe">https://github.com/dequelabs/react-axe</a>
<aside class="notes">
<ul>
<li>Brings axe-core to React at development time</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">react-axe</h1>
<p>Setting up react-axe.</p>
<pre><code class="javascript" data-trim>
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

if (process.env.NODE_ENV !== 'production') {
    const axe = require('react-axe');
    axe(React, ReactDOM, 1000);
}

ReactDOM.render(&lt;App />, document.getElementById('root'));
</code></pre>
<aside class="notes">
<ul>
<li>Hooks into ReactDOM</li>
<li>Run only in development</li>
<li>Note delay in execution</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">react-axe</h1>
<p>Browser console feedback.</p>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/reactaxeconsole.png" alt="Shows the react-axe console feedback for accessibility errors in Chrome"/>
<aside class="notes">
<ul>
<li>Display errors in browser console.</li>
<li>Errors indicate issue and related element</li>
<li>Can click through to actual DOM element</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">Combining the tools</h1>
<img class="nomax" src="/css/images/2017-06-14-accessible-react/consolesummary.png" alt="Summary of console errors for React, aslint-jsx-a11y and react-axe"/>
<aside class="notes">
<ul>
<li>Combining the tools are powerful</li>
<li>Error from React itself</li>
<li>Errors from ESLINT in create-react-app</li>
<li>Errors from react-axe</li>
</ul>
</aside>
</section>
<section>
<h1>Focus control</h1>
<p>Setting focus with refs.</p>
<pre><code class="javascript" data-trim>
componentDidMount(){
    this.nameInput.focus();
}

render(){
    return(
        <div>
            <label htmlFor="demoId">Name</label>
            <input id="demoId" type="text"
            ref={(input) => {this.nameInput = input;}}/>
        </div>
    );
}
</code></pre>
<aside class="notes">
<ul>
<li>Focus management important in JS frameworks/libraries</li>
<li>React changing HTML DOM can impact current keyboard focus</li>
<li>One way to set focus is with Refs</li>
<li>To be used judiciously</li>
</ul>
</aside>
</section>
<section>
<h1>Lazy loading components</h1>
<pre><code class="javascript" data-trim>
class App extends Component {
    state = { LazyBlock: null };

    async componentDidMount() {
        const { default: LazyBlock } = await import('./LazyBlock');
        this.setState({ LazyBlock: &lt;LazyBlock/> });
    }

    render() {
        return ( <main aria-busy={!this.state.LazyBlock}>
                    {this.state.LazyBlock || <p>Loading...</p>}
                 </main> );
    }
}
</code></pre>
<aside class="notes">
<ul>
<li>Way to support progressive enhancement</li>
<li>Start app as quickly as possible</li>
</ul>
</aside>
</section>
<section>
<h1>Lazy loading components</h1>
<p>Splitting code files.</p>
<img src="/css/images/2017-06-14-accessible-react/codesplitting.png" alt="JavaScript code bundles after webpack async-await import and build"/>
<aside class="notes">
<ul>
<li>Files are chunked and loaded when required</li>
</ul>
</aside>
</section>
<section>
<img src="/css/images/2017-06-14-accessible-react/its-logical.jpg" alt="Image of captain kirk showing thumbs up to Spock. Accessibility is logical."/>
</section>
<section class="main">
<h1>Questions</h1>
<hr>
<p>Presentation online at:</p>
<a href="http://almerosteyn.com/slides/">http://almerosteyn.com/slides/</a>
<hr>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>