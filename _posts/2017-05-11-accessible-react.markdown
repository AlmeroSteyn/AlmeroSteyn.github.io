---
layout: slide
title: Accessibility in React
description: Building accessible React apps
theme: present
highlight: tomorrow
transition: fade
---

<section class="main">
<h1>React Accessibility</h1>
<hr>
<h2>Creating accessible applications with ease</h2>
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
"A JavaScript library for building user interfaces." - React docs
</blockquote>
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
<h1 class="no-capitalize">create-react-app</h1>
<pre><code class="javascript" data-trim>
yarn global add create-react-app
create-react-app my-react-app
cd my-react-app
yarn start
</code></pre>
<ul>
    <li>Webpack development and production build.</li>
    <li>ESLint with some a11y rules.</li>
    <li>Progressive app by default.</li>
    <li>Supports code splitting.</li>
    <li>Unit tests + coverage with JSDOM.</li>
</ul>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<blockquote>
"Static AST checker for a11y rules on JSX elements."
</blockquote>
<a href="https://github.com/evcohen/eslint-plugin-jsx-a11y">https://github.com/evcohen/eslint-plugin-jsx-a11y</a>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>More than 30 ESLINT a11y checks.</p>
<img class="nomax" src="/css/images/2017-05-11-accessible-react/jsxa11y.png" alt="Image of some rules in the eslint-jsx-a11y plugin"/>
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
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>A11y issues become build warnings.</p>
<img class="nomax" src="/css/images/2017-05-11-accessible-react/jsxa11ywebpack.png" alt="Shows eslint-jsx-a11y error feedback in create-react-app build"/>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>IDE integration.</p>
<img class="nomax" src="/css/images/2017-05-11-accessible-react/jsxa11yIDE.png" alt="Shows eslint-jsx-a11y error feedback in an IDE"/>
</section>
<section>
<h1 class="no-capitalize">react-axe</h1>
<blockquote>
"Accessibility auditing for React.js applications."
</blockquote>
<img class="nomax" src="/css/images/2017-05-11-accessible-react/axe-core.png" alt="React-axe uses axe-core. Shows axe-core logo." style="max-width: 50%;"/>
<a href="https://github.com/dequelabs/react-axe">https://github.com/dequelabs/react-axe</a>
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
</section>
<section>
<h1 class="no-capitalize">react-axe</h1>
<p>Browser console feedback.</p>
<img class="nomax" src="/css/images/2017-05-11-accessible-react/reactaxeconsole.png" alt="Shows the react-axe console feedback for accessibility errors in Chrome"/>
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
</section>
<section>
<h1>Focus control</h1>
<p>Setting focus with ReactDOM.</p>
<pre><code class="javascript" data-trim>
componentDidMount(){
    const componentNode = ReactDOM.findDOMNode(this);
    componentNode.querySelector('input').focus();
}

render(){
    return(
        <div>
            <label htmlFor="demoId">Name</label>
            <input id="demoId" type="text"/>
        </div>
    );
}
</code></pre>
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
</section>
<section>
<h1>Lazy loading components</h1>
<p>Splitting code files.</p>
<img src="/css/images/2017-05-11-accessible-react/codesplitting.png" alt="JavaScript code bundles after webpack async-await import and build"/>
</section>
<section class="main">
<h1>Questions</h1>
<hr>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>