---
layout: slide
title: The Forms Boss Battle... and how to avoid it
description: Creating accessible forms in HTML and React
theme: ncdt
highlight: tomorrow
transition: none
---

<section class="main">
<h1>The forms boss battle</h1>
<p>... and how to avoid it</p>
<hr>
<div style="display: flex; flex-direction:column;">
<div style="text-align: center">
<img src="/css/images/2019-04-04-the-forms-boss-battle/BHLogo.png" alt="Logo of Binary Horizons" style="max-width: 20%; box-shadow: none;"/>
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
<img src="/css/images/2019-04-04-the-forms-boss-battle/atari.jpg" alt="Atari gaming console" style="max-width: 70%; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Wikimedia Commons licensed under <a style="font-size: 1em;" href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a></figcaption>
</figure>
</section>
<section class="main">
<h1>2019</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/PS4.jpg" alt="Playstation 4 gaming console" style="max-width: 80%; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Released into the <a style="font-size: 1em;" href="https://en.wikipedia.org/wiki/Public_domain">Public Domain</a></figcaption>
</figure>
</section>
<section class="main">
<h1>The game boss</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/gameboss.jpg" alt="Screenshot of a console game with a large, scary game boss" style="max-width: 80%; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Wikimedia Commons licensed under <a style="font-size: 1em;" href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a></figcaption>
</figure>
</section>
<section class="main">
<h1>It's too difficult!!!</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/anger.jpg" alt="Woman being angry about a difficult game" style="max-width: 80%; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Licensed under the <a style="font-size: 1em;" href="https://pixabay.com/service/license/">Pixabay License</a></figcaption>
</figure>
</section>
<section>
<h1>Boss battles on the web</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/loginforminaccessible.jpg" alt="A basic login form with username, password and a login button" style="max-width: 80%; margin-bottom:0;"/>
</section>
<section class="main">
<h1>An inaccessible login form</h1>
<iframe src="https://player.vimeo.com/video/329304374" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>How can something so simple be so broken?</h1>
<pre style="margin-top: 3em;"><code class="html" data-trim>
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
<h1>About that "button"...</h1>
<p style="font-size:0.8em; margin-top: 2em;">If it looks like a button and quacks like a button... what should it be?</p>
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
<li>Activate on mouse click</li>
<li>Activate on Enter</li>
<li>Activate on Spacebar</li>
</ul>
</div>

<p style="margin-top:2em;">But &lt;div> doesn't do that!</p>
</section>
<section class="main">
<h1>Form accessibility secrets are not shared enough</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/shawntweet.png" alt="Tweet by Shawn Wang stating that he was surprised to only recently learn about button types" style="max-width: 80%; margin-bottom:0;"/>
</section>

<section class="main">
<h1>How about labels?</h1>
<pre style="margin-top: 3em; margin-bottom:3em;"><code class="html" data-trim>
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
&lt;input id="username" />

<input aria-label="Username" />

<span id="username">Username</span>
<input aria-labelledby="username" />   
</code></pre>
<p style="font-size:0.8em;">Implicit labelling, explicit labelling, aria-label and </p>
<p style="font-size:0.8em;">aria-labelledby</p>
</section>
<section class="main">
<h1>And the winner is...</h1>
<p style="font-size:0.8em;">Explicit labelling</p>
<pre style="margin-top:4em;"><code class="html" data-trim>
<label for="username">Username</label>
&lt;input id="username" />
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
<pre style="margin-top:3em; margin-bottom:3em;"><code class="html" data-trim>
<label for="username">Username</label>
&lt;input id="username" aria-label="Enter a name for your user"/>
</code></pre>
<p style="font-size:0.5em; font-weight:bold;">aria-label overrides the visual label</p>
</section>
<section class="main">
<h1>Think about voice control</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/dragon.png" alt="Box packaging of the Dragon Naturally Speaking software" style="max-width: 30%; margin-bottom:0; box-shadow: none;"/>
<p style="font-size:0.6em;">The accessible name will be used to match commands</p>
</section>
<section class="main">
<h1>What about info texts?</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/infotexts.jpg" alt="A login form showing info text for the username field asking for only characters from the alphabet" style="max-width: 80%; margin-bottom:0;"/>
</section>
<section class="main">
<h1>Meet aria-describedby</h1>
<pre style="margin-top:4em;"><code class="html" data-trim>
<label for="username">Username</label>
&lt;input id="username" aria-describedby="info"/>

<span id="info">Please use only characters from the alphabet</span>
</code></pre>
</section>
<section class="main">
<h1>Info text in action</h1>
<iframe src="https://player.vimeo.com/video/329794023" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>Client side validation</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/validation.jpg" alt="A login form showing required field validation messages" style="max-width: 80%; margin-bottom:0;"/>
</section>
<section class="main">
<h1>Aria-describedby to the rescue again!</h1>
<pre style="margin-top:3em;"><code class="html" data-trim>
<label for="username">Username</label>
&lt;input id="username" aria-describedby="info error"/>

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
<p style="margin-top:3em;">That means also for &lt;textarea>,</p>
<p>&lt;input type="checkbox"> and &lt;select></p>
</section>
<section class="main">
<h1>What about groups of controls?</h1>
<pre style="margin-top:3em;"><code class="html" data-trim>
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
<pre style="margin-top:3em;"><code class="html" data-trim>
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
<img src="/css/images/2019-04-04-the-forms-boss-battle/noariadescribed.png" alt="Road sign with multiple arrows in multiple directions all ending up at the word NO" style="max-width: 60%; margin-bottom:0; border-radius: 0.4em;"/>
<figcaption style="font-size: 0.25em;">CC0 Public Domain</figcaption>
</figure>
<p style="font-size:0.75em;">Attaching aria-describedby to &lt;fieldset> or &lt;legend> is not supported in many screen readers</p>  
</section>
<section class="main">
<h1>How do I validate groups then?</h1>
<pre style="margin-top:3em;"><code class="html" data-trim>
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
<h1>You don't want your error texts next to your legends?</h1>
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
<pre style="margin-top:3em;"><code class="css" data-trim>
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
<img src="/css/images/2019-04-04-the-forms-boss-battle/focus.png" alt="Road sign with multiple arrows in multiple directions all ending up at the word NO" style="max-width: 60%; margin-bottom:0; margin-top: 2em;"/>
<p style="font-size:0.6em;">Don't do this! Unless you provide your own focus outline style in the CSS.</p>
<pre><code class="css" data-trim>
    outline: none;
    outline: 0;
</code></pre>
</section>
<section class="main">
<h1>Placeholders and titles</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/placeholdertitle.png" alt="Showing an input with a placeholder and a button with icon only and a title" style="max-width: 60%; margin-bottom:0; margin-top: 2em;"/>
<p style="font-size:0.6em;">Should be avoided in most cases!</p>
</section>
<section class="main">
<h1>Wasn't this talk supposed to be about React?</h1>
<img src="/css/images/2019-04-04-the-forms-boss-battle/React-icon.svg" alt="React logo" style="max-width: 60%; margin-bottom:0; box-shadow: none;"/>
<p style="font-size:0.6em;">All video example apps were built in React...</p>
</section>
<section class="main">
<h1>JSX has everything HTML has</h1>
<p style="font-size:0.7em;">A few differences:</p>
<div style="display:flex; justify-content: center;">
<ul style="text-align:left; list-style: disc; font-weight: normal;">
<li>Tags should always be closed</li>
<li>Non-ARIA properties are in camelCase</li>
<li>for becomes htmlFor</li>
<li>class becomes className</li>
</ul>
</div>
<p style="font-size:0.6em;">To build accessible React applications you HAVE to know HTML.</p>
</section>
<section class="main">
<h1>Some form JSX</h1>
<pre style="margin-top: 3em;"><code class="jsx" data-trim>
<form novalidate={true} onSubmit={onSubmitHandler}>

<label htmlFor="username">Username</label>
&lt;input id="username" aria-describedby="info error"/>

<span id="info">Please use only characters from the alphabet</span>
<span id="error">A user name is required</span>

&lt;button className="save-button" type="submit">Submit</button>

</form>
</code></pre>
</section>
<section class="main">
<h1>React hooks</h1>
<figure>
<img src="/css/images/2019-04-04-the-forms-boss-battle/boxinghook.jpg" alt="Boxer performing a hook" style="max-width: 60%; margin-bottom:0;"/>
<figcaption style="font-size: 0.25em;">Licensed under the <a style="font-size: 1em;" href="https://pixabay.com/service/license/">Pixabay License</a></figcaption>
</figure>
</section>
<section class="main">
<h1>Preventing form submission</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
const FormComponent = () => {

  const onSubmitHandler = e => {
    e.preventDefault();
    //Rest of the handler code
  };
  
  return (
      <form onSubmit={onSubmitHandler}>
        {/* Form JSX */}
      </form>
  );
  
};
</code></pre>
</section>
<section class="main">
<h1>Setting focus on things</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const buttonRef = React.useRef(null);
  
  const onSubmitHandler = e => {
    //Set focus when required
    buttonRef.current.focus();
  };
  
  return (
      <form onSubmit={onSubmitHandler}>
        {/* Some JSX */}
        <button type="submit" ref={buttonRef} />
        {/* Some more JSX */}
      </form>
  );
</code></pre>
</section>
<section class="main">
<h1>Controlled form elements</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const [inputValue, setInputValue] = React.useState('');  
  
  onChangeHandler = e => {
      setInputValue(e.target.value)
  }
  
  return (
    &lt;React.Fragment>
         <label htmlFor="petname">Your pet's name</label>
         &lt;input id="petName" 
            onChange={onChangeHandler}
            value={inputValue} />
    &lt;/React.Fragment>    
  );
</code></pre>
</section>
<section class="main">
<h1>Keeping id values unique</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const inputId = React.useRef(generateUniqueId());
  const [inputValue, setInputValue] = React.useState('');  
  
  onChangeHandler = e => {
      setInputValue(e.target.value)
  }
  
  return (
    &lt;React.Fragment>
         <label htmlFor={inputId.current}>Your pet's name</label>
         &lt;input id={inputId.current} onChange={onChangeHandler} 
            value={inputValue} />
    &lt;/React.Fragment>    
  );
</code></pre>
</section>
<section class="main">
<h1>Conditional rendering</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const inputId = React.createRef(generateUniqueId());
  const errorId = React.createRef(generateUniqueId());
  
  //More code
  
  return (
    &lt;React.Fragment>
         <label htmlFor={inputId.current}>Your pet's name</label>
         &lt;input id={inputId.current}
            aria-describedby={hasError ? errorId : null} 
            onChange={onChangeHandler} 
            value={inputValue} />
         {hasError && <span id={errorId}>Please enter a name</span>}   
    &lt;/React.Fragment>    
  );
</code></pre>
</section>
<section class="main">
<h1>Re-using stuff with hooks</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const useInput = () => {
    const inputId = React.createRef(generateUniqueId());
    const [inputValue, setInputValue] = React.useState('');  
      
    onChangeHandler = e => {
        setInputValue(e.target.value)
    }
    
    return {
        id: inputId,
        value: inputValue
        onChange: onChangeHandler
    }
  }
</code></pre>
</section>
<section class="main">
<h1>Now apply the custom hook</h1>
<pre style="margin-top: 3em;"><code class="javascript" data-trim>
  const inputProps = useInput();
  
  return (
    &lt;React.Fragment>
         <label htmlFor={inputProps.id}>Your pet's name</label>
         &lt;input {...inputProps} />
    &lt;/React.Fragment>    
  );
</code></pre>
</section>
<section class="main">
<h1>Applying it all</h1>
<iframe src="https://player.vimeo.com/video/334265221" width="840" height="497" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
</section>
<section class="main">
<h1>The Forms Boss Battle</h1>
<p>... and how to avoid it</p>
<hr>
<div style="display: flex; flex-direction:column;">
<div style="text-align: center">
<img src="/css/images/2019-04-04-the-forms-boss-battle/BHLogo.png" alt="Logo of Binary Horizons" style="max-width: 20%; box-shadow: none;"/>
</div>
<ul>
    <li style="font-size: 1.5em; margin-bottom: 25px;">Almero Steyn</li>
    <li><a href="http://almerosteyn.com/" style="font-size: 1em; font-weight: 100;">almerosteyn.com</a></li>
    <li><span style="font-size: 30px; font-weight: 100;">@kryptos_rsa</span></li>
</ul>
</div>
</section>



