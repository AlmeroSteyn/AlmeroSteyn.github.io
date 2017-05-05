---
layout: slide
title: Web Accessibility
description: Building websites for everyone.
theme: qdelft
transition: slide
---
<section data-markdown class="q-main-slide" data-background-color="#363F44">
{% highlight html%}
## Web Accessibility
{% endhighlight %}
___
Building websites for everyone
    <script type="text/template">
        <img class="q-image q-main-logo q-main-logo-pad" src="/css/images/2017-05-04-demo-presentation/QLogoInverted.png"/>
        <h2>Web accessibility</h2>
        <hr/>
        <p>
            <span>Building websites for everyone</span>
        </p>
        <div class="q-box q-col-50">
            <ul class="q-address">
                <li>Q Delft B.V.</li>
                <li>Mijnbouwplein 33</li>
                <li>2628 RT Delft</li>
                <li>+31 15 30 30 130</li>
                <li>www.qdelft.nl</li>
            </ul>
        </div>
        <div class="q-box q-col-50 q-col-50-right">
            <ul class="q-address">
                <li>Almero Steyn</li>
                <li>Twitter: @KryptosRSA</li>
                <li>almero.steyn@qdelft.nl</li>
                <li>almerosteyn.com</li>
            </ul>
        </div>
    </script>
</section>
<section data-markdown>
<script type="text/template">
     <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"What is web accessibility?"</h2>
                <p><i>The inclusive practice of removing barriers that prevent interaction with, or access to websites,
                    by
                    people with disabilities. When sites are correctly designed, developed and edited, all users have
                    equal
                    access to information and functionality.</i> - Wikipedia</p>
                <p style="font-size:27px;"><a href="https://en.wikipedia.org/wiki/Web_accessibility">https://en.wikipedia.org/wiki/Web_accessibility</a>
                </p>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"Who are the disabled?"</h2>
                <p><i>One in six people in the European Union (EU) has a disability
                    that ranges from mild to severe making around 80 million who are often prevented from taking part
                    fully in society
                    and the economy because of environmental and attitudinal barriers. For people with
                    disabilities the rate of poverty is 70% higher than the average partly due to limited access to
                    employment.</i> - European Commission</p>
                <p style="font-size:27px;"><a href="http://bit.ly/1LdRaml">http://bit.ly/1LdRaml</a></p>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>What types of disabilities are there?</h2>
                <img src="/css/images/2017-05-04-demo-presentation/types.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>What would your future self say?</h2>
                <img src="/css/images/2017-05-04-demo-presentation/future.png" class="stretch"/>
                <p><i>Over a third of people aged over 75 have disabilities that restrict them to some extent, and
                    over 20% are considerably restricted. Furthermore, these numbers are set to rise as the EU's
                    population ages.</i> - European Commission</p>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Did you know that accessible HTML is also better for search engines?</h2>
                <img src="/css/images/2017-05-04-demo-presentation/Google.png" class="stretch"/>
            </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
           <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"Accessibility is hard!!!"</h2>
                <img src="/css/images/2017-05-04-demo-presentation/a11yhard.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"Here you go. Support the WCAG!"</h2>
                <img src="/css/images/2017-05-04-demo-presentation/wcag.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"Accessibility was a nightmare on our previous project..."</h2>
                <img src="/css/images/2017-05-04-demo-presentation/hamster.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"The average user loves our website!!!"</h2>
                <img src="/css/images/2017-05-04-demo-presentation/average.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>"But my HTML works!"</h2>
                <divs>
                    <span style="font-size:24px;">Enter text here</span>
                    <input>
                </divs>
                <pre><code class="html" data-trim>
<divs>
<span>Enter text here</span></span>
    <input>
</divs>
</code></pre>
            </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>What if I told you that it's only perceived to be hard?</h2>
                <img src="/css/images/2017-05-04-demo-presentation/perception.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Who wouldn't be able to use this input screen?</h2>
                <img src="/css/images/2017-05-04-demo-presentation/faildetail.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Let's try it with a screen reader...</h2>
                <video controls class="stretch v3h2" data-src="/css/videos/2017-05-04-demo-presentation/FailDetail1.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <img data-src="/css/images/2017-05-04-demo-presentation/OMG.gif" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>It's a dumpster fire!</h2>
                <img src="/css/images/2017-05-04-demo-presentation/dumpster.gif" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Let's recap!</h2>
                <img src="/css/images/2017-05-04-demo-presentation/faildetailvirt.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Don't lose focus.</h2>
                <pre><code class="css">
                    /*The cardinal sin*/
                    :focus {
                    outline: 0;
                    }
                </code></pre>
                <img src="/css/images/2017-05-04-demo-presentation/focus.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Every time you neglect to label a control a fairy drops down dead.</h2>
                <pre><code class="html">
<!--Implicit labelling-->
<label>Name:
   <input type="text"/>
</label>
<!--Explicit labelling-->
<label for="nameInput">Name:</label>
<input id="nameInput" type="text"/>
<!--ARIA labelling-->
<input type="text" aria-label="Name"/>
                </code></pre>
                <aside class="notes">
                    <ul>
                        <li>Every form control needs a label.</li>
                        <li>We can use implicit labelling or explicit labelling.</li>
                        <li>For cases where the label is implied visually, we can use ARIA to still label for AT.</li>
                        <li>By properly labelling controls you can also select them by clicking the labels!</li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>If it walks like a duck and quacks like a duck it must be... urm... a button?</h2>
                <pre><code class="html">
<!--All the power of JavaScript and you make a DIV clickable?-->
<div class="btn btn-primary" onClick={...}>Press Me</div>
<!--How about just...-->
<button class="btn btn-primary" onClick={...}>Press Me</button>
                </code></pre>
                <aside class="notes">
                    <ul>
                        <li>Use native HTML elements when possible.</li>
                        <li>Every native HTML element is accessible for its role.</li>
                        <li>Mention a button with enter and space for activation.</li>
                        <li>One of the biggest secrets of a11y is using native HTML elements.</li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Your HTML is as strong as its weakest link.</h2>
                <pre><code class="html">
<!--Anchors are for navigation!-->
<a onClick={...}>Go to the company page.</a>
<a href="#" onClick={...}>Go to the company page.</a>
<!--Aaaaah that's better...-->
<a href="www.qdelft.nl">Go to the company page.</a>
                </code></pre>
                <aside class="notes">
                    <ul>
                        <li>An anchor is invalid without a proper href.</li>
                        <li>Omitting the href completely will render the anchor unclickable!</li>
                        <li>Let anchors navigate!</li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Button it! Link it!</h2>
                <pre><code class="html">
<!--Buttons are for actions-->
<button onClick={...}>Save changes.</button>
<!--Anchors are for navigation!-->
<a href="www.qdelft.nl">Go to the company details.</a>
                </code></pre>
                <img src="/css/images/2017-05-04-demo-presentation/buttonlink.png"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Don't leave people out of the picture.</h2>
                <pre><code class="html">
<img src="somepic4327628465784365.png" alt="Image of Albert Einstein"/>
                </code></pre>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Let's apply some of the new things we learnt.</h2>
                <video controls class="stretch v3h12" data-src="/css/videos/2017-05-04-demo-presentation/PassDetail.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Now we speak HTML!</h2>
                <img src="/css/images/2017-05-04-demo-presentation/speak.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>And ARIA is your second dialect...</h2>
                <a href="https://www.w3.org/WAI/intro/aria">https://www.w3.org/WAI/intro/aria</a>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>One more thing... Pokemon NO!</h2>
                <img src="/css/images/2017-05-04-demo-presentation/contrast.png" class="stretch"/>
            </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
   <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <p><i>Seeing it once is better than being told 100 times.</i> - Chinese proverb</p>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Plug out your mouse!</h2>
                <img src="/css/images/2017-05-04-demo-presentation/nomouse.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Chrome accessibility inspector.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/ChromeInspectorzoom.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Safari accessibility inspector.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/safari-inspectorzoom.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>The screen reader.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/screenbrowser.png" class="stretch"/>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>aXe your accessibility issues! </h2>
                <img src="/css/images/2017-05-04-demo-presentation/axe.png" style="width: 100px; float:right"/>
                <video controls class="stretch v4h5" data-src="/css/videos/2017-05-04-demo-presentation/axe.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>WAVE away your issues.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/wave.png" style="width: 200px; float:right"/>
                <video controls class="stretch v4h6" data-src="/css/videos/2017-05-04-demo-presentation/wave.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Visualising contrast.</h2>
                <p>Colour contrast analyser.</p>
                <video controls class="stretch v4h7" data-src="/css/videos/2017-05-04-demo-presentation/cca.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left"><h2>Simulate visual disabilities.</h2>
                <p>NoCoffee Vision Simulator</p>
                <video controls class="stretch v4h8" data-src="/css/videos/2017-05-04-demo-presentation/NoCoffee.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Do it right from the start.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/alllove.png" class="stretch"/>
                <aside class="notes">
                    <ul>
                        <li>Talk about how a11y is little extra work if it is thouight about from the start.</li>
                        <li>This is where a11y can become a lot of work later if everyone does not care about it.</li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>No man is an island.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/noisland.png" class="stretch"/>
                <aside class="notes">
                    <ul>
                        <li>Re-iterate the importance of everyone caring about a11y.</li>
                        <li>Re-iterate that a11y is only little work if it is important to everyone and from the
                            start.
                        </li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Inclusive design vs. good looking design.</h2>
                <img src="/css/images/2017-05-04-demo-presentation/chosen.png" class="stretch"/>
                <p>But I can't operate it at all with a keyboard! ¯\_(ツ)_/¯</p>
                <aside class="notes">
                    <ul>
                        <li>Don't just design for sighties. Design for function.</li>
                        <li>No matter how good something looks to you, there may be someone who gets completely blocked
                            from using it.
                        </li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Remember those internal websites!</h2>
                <p>The people in your company are... PEOPLE!</p>
                <aside class="notes">
                    <ul>
                        <li>Mention how we already have people with disabilities in our workplaces.</li>
                        <li>Mention that we are closing doors from desperate unemployed people by negating this.</li>
                    </ul>
                </aside>
            </section>
            <section data-background-image="/css/images/2017-05-04-demo-presentation/QLogoQOnlyPadded.png" data-background-size="100px"
                     data-background-position="bottom left">
                <h2>Helpful links</h2>
                <a href="http://a11yproject.com/">http://a11yproject.com/</a><br>
                <a href="http://webaim.org/">http://webaim.org/</a><br>
                <a href="https://www.w3.org/TR/wai-aria-practices-1.1/">https://www.w3.org/TR/wai-aria-practices-1.1/</a>
                <aside class="notes">
                    <ul>
                        <li>Explain what the links above are about.</li>
                    </ul>
                </aside>
            </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
 <section>
            <h2>Accessibility is easy!</h2>
            <img src="/css/images/2017-05-04-demo-presentation/a11yeasy.png" class="stretch"/>
            <aside class="notes">
                <ul>
                    <li>Stand still by how a11y can be very easy.</li>
                    <li>Mention the importance again vs the little extra time we need to skill up and build a11y
                        websites.
                    </li>
                    <li>Mention how we are now ready to build the inclusive websites of the future.</li>
                </ul>
            </aside>
        </section>
</script>
</section>
<section data-markdown>
<script type="text/template">
        <section class="q-main-slide " data-background-color="#363F44">
            <h2>Questions?</h2>
            <img class="q-image q-sub-logo" src="/css/images/2017-05-04-demo-presentation/QLogoQOnly.png"/>
            <div class="q-box q-col-50">
                <ul class="q-address">
                    <li>Q Delft B.V.</li>
                    <li>Mijnbouwplein 33</li>
                    <li>2628 RT Delft</li>
                    <li>+31 15 30 30 130</li>
                    <li>www.qdelft.nl</li>
                </ul>
            </div>
            <div class="q-box q-col-50 q-col-50-right">
                <ul class="q-address">
                    <li>Almero Steyn</li>
                    <li>Twitter: @KryptosRSA</li>
                    <li>almero.steyn@qdelft.nl</li>
                    <li>almerosteyn.com</li>
                </ul>
            </div>
        </section>
</script>
</section>