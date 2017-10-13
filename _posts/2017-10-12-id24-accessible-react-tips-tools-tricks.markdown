---
layout: slide
title: Tips, tricks and tools for building accessible React web apps
description: Inclusive Design 24 Presentation
theme: id24
highlight: tomorrow
transition: none
---

<section class="main">
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/QLogo.png" alt="Log of QDelft" style="max-width: 20%"/>
<h1>Tips, tricks and tools for building accessible React web apps</h1>
<hr>
<ul>
    <li>Almero Steyn</li>
    <li>QDelft B.V.</li>
    <li>almerosteyn.com</li>
    <li>twitter.com/kryptos_rsa</li>
</ul>
</section>
<section>
<h1>React</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/react-logo.svg" alt="React logo" style="max-width: 20%"/>
<blockquote>
"A JavaScript library for building user interfaces." - React docs
</blockquote>
</section>
<section>
<h1>Who uses React?</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/facebook.png" alt="Facebook logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/Netflix.jpg" alt="Netflix logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/airbnb.png" alt="Airbnb logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/instagram.jpg" alt="Instagram logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/whatsapp.png" alt="Whatsapp logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/tenon.png" alt="Tenon logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/wehkamp.jpg" alt="Wehkamp logo" style="max-width: 20%"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/bbc.png" alt="BBC logo" style="max-width: 20%"/>
</section>
<section>
<h1>How accessible are they?</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/goodbadugly.jpg" alt="Movie poster of The Good, the Bad and the Ugly"/>
</section>
<section>
<h1>The Good-a11y</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/good.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/tenoncap.png" alt="Image capture and Axe scan of tenon.io"/>
</section>
<section>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/airbnbcap.png" alt="Image capture and Axe scan of airbnb"/>
</section>
<section>
<h1>The other two</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/bad.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/ugly.png" alt="The Good from the movie the Good, the Bad and the Ugly"/>
</section>
<section>
<h1>WebAIM Alexa Top 100 scan </h1>
<blockquote>
"The number of errors found has increased 60% over the last 5 years – from an average of 25 errors in 2011 to 40 errors in 2017." - WebAIM
</blockquote>
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
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/shock.jpg" alt="Image of koala expressing shock at React being all JavaScript" style="max-width:40%"/>
</section>
<section>
<h1>JS-Zilla destroys a11y!!</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/godzilla.jpg" alt="Image depicting JavaScript as a destructive monster"/>
</section>
<section>
<h1>But why?</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/grumpy-confused-cat.png" alt="Cat confused about the accessible state of React websites"/>
</section>
<section>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/divtobutton.jpg" alt="Image of Harry Potter turning a div into a button"/>
    <pre><code class="html" data-trim>
        <div className="looks-like-a-button"
             onClick={this.onClickHandler}>
               Press me please
        </div>
    </code></pre>
</section>
<section>
<h1>It can be a friendly monster...</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/friendly-monster2.jpg" alt="Image depicting JavaScript as cute monster"/>
<aside class="notes">
<ul>
<li>BREATHE!!!!!!</li>
</ul>
</aside>
</section>
<section>
<h1>Example application</h1>
<a href="https://github.com/AlmeroSteyn/react-a11y-patterns">https://github.com/AlmeroSteyn/react-a11y-patterns</a>
</section>
<section>
<h1>React component tree</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/react-components.png" alt="Depicts the React virtual DOM and how it relates to the real DOM"/>
</section>
<section>
<h1>React component class</h1>
<pre><code class="javascript" data-trim data-noescape>
import React, { Component } from 'react';

class Demo extends Component {
    render() {
        <mark class="transparent">return ( &lt;span>{this.props.displayText}&lt;/span> );</mark>
    }
}

export default Demo;

</code></pre>
</section>
<section>
<h1>React component class</h1>
<pre><code class="javascript" data-trim data-noescape>
import React, { Component } from 'react';

class Demo extends Component {
    render() {
        <mark>return ( &lt;span>{this.props.displayText}&lt;/span> );</mark>
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
<pre><code class="javascript" data-trim data-noescape>
import React from 'react';
<mark>import Demo from './Demo';</mark>

const Root = () => (
     <mark>&lt;Demo displayText="Show this text"/></mark>
);

export default Root;
</code></pre>
</section>
<section>
<h1>React virtual DOM + Reconciler</h1>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/reactdom.png" alt="Depicts the React virtual DOM and how it relates to the real DOM"/>
</section>
<section>
<h1>React virtual DOM in browser</h1>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/reactdominbrowser.png" alt="A debug view of the React DOM in React dev tools"/>
</section>
<section>
<h1>React actual DOM in browser</h1>
<img class="nomax"  src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/realdominbrowser.png" alt="A debug view of the DOM to compare to that of the React DOM of the previous slide"/>
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
<h1>Good HTML makes good JSX</h1>
<pre><code class="html" data-trim data-noescape>
const AppNavigation = () =>
  <mark class="transparent">&lt;aside></mark>
    &lt;nav>
      <mark class="transparent">&lt;ul className="nav"></mark>
        &lt;li>
          <mark class="transparent"><NavLink</mark>
            to={pathname}
            activeClassName="active">
            Contact
          <mark class="transparent"></NavLink></mark>
        &lt;/li>
      <mark class="transparent">&lt;/ul></mark>
    &lt;/nav>
  <mark class="transparent">&lt;/aside></mark>;
</code></pre>
</section>
<section>
<h1>Good HTML makes good JSX</h1>
<pre><code class="html" data-trim data-noescape>
const AppNavigation = () =>
  <mark>&lt;aside></mark>
    &lt;nav>
      <mark>&lt;ul className="nav"></mark>
        &lt;li>
          <mark class="transparent"><NavLink</mark>
            to={pathname}
            activeClassName="active">
            Contact
          <mark class="transparent"></NavLink></mark>
        &lt;/li>
      <mark>&lt;/ul></mark>
    &lt;/nav>
  <mark>&lt;/aside></mark>;
</code></pre>
</section>
<section>
<h1>Good HTML makes good JSX</h1>
<pre><code class="html" data-trim data-noescape>
const AppNavigation = () =>
  <mark>&lt;aside></mark>
    &lt;nav>
      <mark>&lt;ul className="nav"></mark>
        &lt;li>
          <mark><NavLink</mark>
            to={pathname}
            activeClassName="active">
            Contact
          <mark></NavLink></mark>
        &lt;/li>
      <mark>&lt;/ul></mark>
    &lt;/nav>
  <mark>&lt;/aside></mark>;
</code></pre>
</section>
<section>
<h1>First rule of ARIA</h1>
    <p>Bad idea:</p>
     <pre><code class="html" data-trim>
       <div className="looks-like-button"
            onClick={this.onClickHandler}>
         Press me
       </div>
     </code></pre>
    <p>Good idea:</p>
     <pre><code class="html" data-trim>
         <button onClick={this.onClickHandler}>
            Press
         </button>
     </code></pre>
</section>
<section>
    <h1>JSX and ARIA</h1>
    <p>All ARIA attributes are valid JSX props!</p>
    <pre><code class="html" data-trim>
            <input id={nameId} aria-label={accessibleLabel} type="text" />
    </code></pre>
    <p>IntelliSense in supported IDEs.</p>
    <img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/IDE-intellisense.png" alt="ARIA attribute IntelliSense in JSX with WebStorm"/>
<aside class="notes">
<ul>
<li>JSX supports ARIA in the same way as HTML</li>
<li>Added ability to change aria-props programmatically</li>
<li>Allows for IDE support</li>
</ul>
</aside>
</section>
<section>
<h1>Intact header symantics</h1>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/headers.png" alt="Diagram of HTML headers"/>
<pre><code class="html" data-trim>
const HeaderWithLevel = ({ headerText, level }) => {
  const HeaderLevel = `h${level}`;
  return &lt;HeaderLevel>{headerText}&lt;/HeaderLevel>;
};
</code></pre>
</section>
<section>
<h1>Components and unique id's</h1>
 <pre><code class="html" data-trim data-noescape>
 import uuid from 'uuid';
 //...
 <mark>this.inputId = uuid.v4();</mark>
 //...
 render() {
    //...
    <label <mark>htmlFor={this.inputId}</mark>>
      {labelText}
    </label>
    <input <mark>id={this.inputId}</mark>
      onChange={this.onChangeHandler}
      value={value}
    />
    //...
 }
 </code></pre>
 <a href="https://github.com/kelektiv/node-uuid">https://github.com/kelektiv/node-uuid</a>
</section>
<section>
<h1>Routing is a11y silent</h1>
<pre><code class="html" data-trim>
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
<section>
<h1>Set focus after navigation</h1>
<pre><code class="html" data-trim data-noescape>
class PageFocusSection extends Component {
  componentDidMount() {
    <mark>this.header.focus()</mark>;
  }
  render() {
    const { children, headingText } = this.props;
    return (&lt;section>
        <h2 tabIndex="-1"
            <mark>ref={header => (this.header = header)}</mark>>
          {headingText}
        </h2>
        {children}
      &lt;/section>);
  }
}
</code></pre>
</section>
<section>
<h1>Changing the document title</h1>
<pre><code class="html" data-trim>
//...
import DocumentTitle from 'react-document-title';
//...
const SetDocTitle = ({ docTitle, children }) =>
  <DocumentTitle title={docTitle}>
    {children}
  </DocumentTitle>;
</code></pre>
<a href="https://github.com/gaearon/react-document-title">https://github.com/gaearon/react-document-title</a>
</section>
<section>
<h1>ARIA live announcer</h1>
<pre><code class="html" data-trim>
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
<a href="https://github.com/AlmeroSteyn/react-aria-live">https://github.com/AlmeroSteyn/react-aria-live</a>
</section>
<section>
 <video controls class="stretch" src="/css/videos/2017-10-12-id24-accessible-react-tips-tools-tricks/a11yappwalkthrough.mp4" type="video/mp4">
        Your browser does not support the video tag.
</video>
</section>
<section>
<h1>React a11y docs</h1>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/reactdocs.png" alt="Screenshot of the React accessibility docs"/>
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
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/jsxa11y.png" alt="Image of some rules in the eslint-jsx-a11y plugin"/>
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
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/jsxa11ywebpack.png" alt="Shows eslint-jsx-a11y error feedback in create-react-app build"/>
<aside class="notes">
<ul>
<li>Can be hooked into WebPack build like in create-react-app</li>
</ul>
</aside>
</section>
<section>
<h1 class="no-capitalize">eslint-plugin-jsx-a11y</h1>
<p>IDE integration.</p>
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/jsxa11yIDE.png" alt="Shows eslint-jsx-a11y error feedback in an IDE"/>
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
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/axe-core.png" alt="React-axe uses axe-core. Shows axe-core logo." style="max-width: 50%;"/>
<br/>
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
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/reactaxeconsole.png" alt="Shows the react-axe console feedback for accessibility errors in Chrome"/>
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
<img class="nomax" src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/consolesummary.png" alt="Summary of console errors for React, aslint-jsx-a11y and react-axe"/>
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
<h1>Lazy loading components</h1>
<pre><code class="javascript" data-trim>
class App extends Component {
    state = { LazyBlock: null };

    async componentDidMount() {
        const { default: LazyBlock } =
                    await import('./LazyBlock');
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
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/codesplitting.png" alt="JavaScript code bundles after webpack async-await import and build"/>
<aside class="notes">
<ul>
<li>Files are chunked and loaded when required</li>
</ul>
</aside>
</section>
<section>
<img src="/css/images/2017-10-12-id24-accessible-react-tips-tools-tricks/its-logical.jpg" alt="Image of captain kirk showing thumbs up to Spock. Accessibility is logical."/>
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
