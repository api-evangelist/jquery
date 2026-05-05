---
title: "jQuery 3.7.0 Released: Staying in Order"
url: "https://blog.jquery.com/2023/05/11/jquery-3-7-0-released-staying-in-order/"
date: "Thu, 11 May 2023 18:38:17 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>jQuery 3.7.0 is now available! This release has it all: bug fixes, a new method, and a performance improvement! We even dropped our longtime selector engine: Sizzle. Or, I should say, we moved it into jQuery. jQuery no longer depends on Sizzle as a separate project, but has instead dropped its code directly into jQuery core. This helps us prepare for the major changes coming to selection in future jQuery versions. That doesn&#8217;t mean much right now, but jQuery did drop a few bytes because Sizzle supports even older browsers than jQuery. As an aside, we do plan on archiving Sizzle, but we&#8217;ll have more details on that in a future blog post.</p>



<p>As usual, the release is available on <a href="https://jquery.com/download/">our cdn</a> and the npm package manager. Other third party CDNs will probably have it soon as well, but remember that we don&#8217;t control their release schedules and they will need some time. Here are the highlights for jQuery 3.7.0.</p>



<h2 class="wp-block-heading">New method: <code>.uniqueSort()</code></h2>



<p>Some APIs, like <code>.prevAll()</code>, return elements in reverse order, which can result in some confusing behavior when used with wrapping methods. For example,</p>



<pre class="wp-block-preformatted">$elem.prevAll().wrapAll("&lt;p/&gt;")</pre>



<p>The above would wrap all of the elements as expected, but it would write those elements to the DOM in reverse order. To solve this in a way that prevented breaking existing code, we&#8217;ve documented that <code>.prevAll()</code> and similar methods return reverse-order collections, which is still desirable in many cases. But we&#8217;ve also added a new method to make things easier: a chainable <code>.uniqueSort()</code>, which does the equivalent of the existing but static <code>jQuery.uniqueSort()</code>.</p>



<p>So, our previous example would become:</p>



<pre class="wp-block-preformatted">$elem.prevAll().uniqueSort().wrapAll("&lt;p/&gt;")</pre>



<p id="block-b68ae8c6-b30e-493b-915d-c8d63a2485c1">and the element order in the DOM would remain the same.</p>
</div></div>



<h2 class="wp-block-heading">Added some unitless CSS properties</h2>



<p>jQuery 3.7.0 adds support for more CSS properties that should not automatically have &#8220;px&#8221; added to them when they are set without units. For instance, <code>.css('aspect-ratio', 5)</code> would result in the CSS <code>aspect-ratio: 5px;</code>.  All in all, we added seven more properties, and we got a little help with our list from <a href="https://github.com/facebook/react/blob/afea1d0c536e0336735b0ea5c74f635527b65785/packages/react-dom-bindings/src/shared/CSSProperty.js/#L8-L58">React</a>. Thanks, React!</p>



<p>It&#8217;s worth noting that jQuery 4.0 will change the way we handle unitless CSS properties. Rather than relying on a list of CSS properties to avoid adding <code>"px"</code>, we&#8217;ll instead have an list of properties to which we definitely want to add <code>"px"</code> when there are no units passed. That should be more future-proof.</p>



<h2 class="wp-block-heading">Performance improvement in manipulation</h2>



<p>jQuery 3.7.0 comes with a measurable performance improvement for some use cases when using manipulation methods like <code>.append()</code>. When we removed a support test for a browser we no longer support, it meant that checks against document changes no longer needed to run at all. Essentially, that resulted in a speedup anywhere between 0% and 100%. The most significant speedup will be for some rare cases where users frequently switch contexts between different documents, perhaps by running manipulations across multiple iframes.</p>



<h2 class="wp-block-heading">Negative margins in <code>outerHeight(true)</code></h2>



<p>Back in jQuery 3.3.0, we fixed an issue to include scroll gutters in the calculations for <code>.innerWidth()</code> and <code>.innerHeight()</code>. However, that fix didn&#8217;t take negative margins into account, which meant that <code>.outerWidth(true)</code> and <code>.outerHeight(true)</code> no longer respected negative margins. We&#8217;ve fixed that in 3.7.0 by separating the margin calculations from the scroll gutter adjustments.</p>



<h2 class="wp-block-heading">Using different native focus events in IE</h2>



<p>Focus and blur events are probably the most complicated events jQuery has to deal with across browsers. jQuery 3.4.0 introduced some minor regressions when it fixed an issue with the data passed through focus events. We were finally able to <a href="https://github.com/jquery/jquery/commit/59f7b55bf6dad71eee6434116566356d597f1d90">close all of those tickets</a> in jQuery 3.7.0!</p>



<p>But, we need to point out a possible breaking change in IE. In all versions of IE, <code>focus</code> &amp; <code>blur</code> events are fired asynchronously. In all other browsers, those events are fired synchronously. The asynchronous behavior in IE <a href="https://github.com/jquery/jquery/issues/4856">caused</a> <a href="https://github.com/jquery/jquery/issues/4859">issues</a>. The fix was to change which events we used natively. Fortunately, <code>focusin</code> &amp; <code>focusout</code> are run synchronously in IE, and so we now simulate <code>focus</code> via <code>focusin</code> and <code>blur</code> via <code>focusout</code> in IE. That one change allowed us to rely on synchronous focus events in IE, which solved a lot of issues (see the changelog for the full list).</p>



<p>If you&#8217;re curious, support for IE will be dropped in jQuery 5.0 and many of those changes are already in a <a href="https://github.com/jquery/jquery/pull/5077">PR</a>.</p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Upgrading</h2>



<p>We do not expect compatibility issues when upgrading from a jQuery 3.0+ version. To upgrade, have a look at the new <a href="https://jquery.com/upgrade-guide/3.5/">3.5 Upgrade Guide</a>. If you haven’t yet upgraded to jQuery 3+, first have a look at the <a href="https://jquery.com/upgrade-guide/3.0/">3.0 Upgrade Guide</a>.</p>



<p>The <a href="https://github.com/jquery/jquery-migrate#migrate-older-jquery-code-to-jquery-30">jQuery Migrate plugin</a> will help you to identify compatibility issues in your code. Please try out this new release and <a href="https://github.com/jquery/jquery/issues">let us know about any issues you experienced</a>.</p>



<p>If you can&#8217;t yet upgrade to 3.5+, Daniel Ruf has kindly provided <a href="https://github.com/DanielRuf/snyk-js-jquery-565129">patches for previous jQuery versions</a>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-3.7.0.js">https://code.jquery.com/jquery-3.7.0.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.7.0.min.js">https://code.jquery.com/jquery-3.7.0.min.js</a></p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@3.7.0</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Along with the regular version of jQuery that includes the ajax and effects modules, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 6k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-3.7.0.slim.js">https://code.jquery.com/jquery-3.7.0.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.7.0.slim.min.js">https://code.jquery.com/jquery-3.7.0.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm and Bower. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/fecore1">fecore1</a>, <a href="https://github.com/mgol">Michal Golebiowski-Owczarek</a> and the whole jQuery team.</p>



<h2 class="wp-block-heading">We&#8217;re on Mastodon!</h2>



<p>jQuery now has its very own Mastodon account. We will be cross posting to both Twitter and Mastodon from now on. Also, you may be interested in following some of our team members that have Mastodon accounts.</p>
</div></div>



<p>jQuery: <a href="https://social.lfx.dev/@jquery">https://social.lfx.dev/@jquery</a></p>



<p>mgol: <a href="https://hachyderm.io/@mgol">https://hachyderm.io/@mgol</a></p>



<p>timmywil: <a href="https://hachyderm.io/@timmywil">https://hachyderm.io/@timmywil</a></p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/3.6.4...3.7.0">3.7.0</a></p>
</div></div>



<h3>Build</h3>
<ul>
<li>Only install Playwright dependencies when needed (<a href="https://github.com/jquery/jquery/commit/212b6a4fce06b7435bbe9d8494e470881badacc6">212b6a4f</a>)</li>
<li>Bump actions/setup-node from 3.5.1 to 3.6.0 (<a href="https://github.com/jquery/jquery/commit/582785e047ca1837ebffc8a87b2e51e03f727c0a">582785e0</a>)</li>
<li>Run GitHub Action browser tests on Playwright WebKit (<a href="https://github.com/jquery/jquery/commit/da7057e9b0d48afdf5666597279f0a24e9828bc8">da7057e9</a>)</li>
<li>Migrate middleware-mockserver to modern JS (<a href="https://github.com/jquery/jquery/commit/6b2abbdc46e9c4c37f515e838a7f820a4f2bb91a">6b2abbdc</a>)</li>
<li>remove stale Insight package from custom builds (<a href="https://github.com/jquery/jquery/commit/37b04d5aba732ce7f03dc73e524ef9096a613a4d">37b04d5a</a>)</li>
</ul>

<h3>CSS</h3>
<ul>
<li>Make `offsetHeight( true )`, etc. include negative margins (<a href="https://github.com/jquery/jquery/issues/3982">#3982</a>, <a href="https://github.com/jquery/jquery/commit/7bb48a0290a20594ea2a5a7b5772e0410a67164c">7bb48a02</a>)</li>
<li>Add missing jQuery.cssNumber entries (<a href="https://github.com/jquery/jquery/issues/5179">#5179</a>, <a href="https://github.com/jquery/jquery/commit/3eed28209ed02eca498095b597727bf1f98163aa">3eed2820</a>)</li>
</ul>

<h3>Deferred</h3>
<ul>
<li>Rename `getStackHook` to `getErrorHook` (3.x version) (<a href="https://github.com/jquery/jquery/issues/5201">#5201</a>, <a href="https://github.com/jquery/jquery/commit/cca7118658a074771fb3598145e78ca39b93c20d">cca71186</a>)</li>
</ul>

<h3>Docs</h3>
<ul>
<li>Remove stale badge from README (<a href="https://github.com/jquery/jquery/commit/e062f9cbc680998fe391e505a7e0e082a83d7150">e062f9cb</a>)</li>
<li>update irc to Libera and fix LAMP dead link (<a href="https://github.com/jquery/jquery/commit/e0c670e66d409b6d7a230c7d4d119a7447091b63">e0c670e6</a>)</li>
</ul>

<h3>Event</h3>
<ul>
<li>Simplify the check for saved data in leverageNative (<a href="https://github.com/jquery/jquery/commit/9ab26aa508c6cca6afa9c6247ee6d50eaed2da77">9ab26aa5</a>)</li>
<li>Make trigger(focus/blur/click) work with native handlers (<a href="https://github.com/jquery/jquery/issues/5015">#5015</a>, <a href="https://github.com/jquery/jquery/commit/754108fbbf449b8d9736c6259551be538055a60a">754108fb</a>)</li>
<li>Simulate focus/blur in IE via focusin/focusout (3.x version) (<a href="https://github.com/jquery/jquery/issues/4856">#4856</a>, <a href="https://github.com/jquery/jquery/issues/4859">#4859</a>, <a href="https://github.com/jquery/jquery/issues/4950">#4950</a>, <a href="https://github.com/jquery/jquery/commit/59f7b55bf6dad71eee6434116566356d597f1d90">59f7b55b</a>)</li>
</ul>

<h3>Release</h3>
<ul>
<li>add support for md5 sums in windows (<a href="https://github.com/jquery/jquery/commit/3b7bf19998b8373a402f8f2c933fbbe0c112f0ed">3b7bf199</a>)</li>
</ul>

<h3>Selector</h3>
<ul>
<li>Remove an obsolete comment (<a href="https://github.com/jquery/jquery/commit/14685b318ae056cf9011ba2dcc73c077c3ae5a2d">14685b31</a>)</li>
<li>Wrap activeElement access in try-catch (<a href="https://github.com/jquery/jquery/commit/3936cf3ef355a556d7990c77bbcacb69208fa4ed">3936cf3e</a>)</li>
<li>Stop relying on CSS.supports( &#8220;selector(&#8230;)&#8221; ) (<a href="https://github.com/jquery/jquery/issues/5194">#5194</a>, <a href="https://github.com/jquery/jquery/commit/63c3af481c7010920bca68518c434cd27ab22cb2">63c3af48</a>)</li>
<li>Rename rcombinators to rleadingCombinator (<a href="https://github.com/jquery/jquery/commit/ac1c59a354c1e333cbe3c40f3b3dc7f644d81f6b">ac1c59a3</a>)</li>
<li>Make selector lists work with `qSA` again (<a href="https://github.com/jquery/jquery/issues/5177">#5177</a>, <a href="https://github.com/jquery/jquery/commit/848de625425c6b08ec9d8ad9a4bcab7e913c2477">848de625</a>)</li>
<li>Implement the `uniqueSort` chainable method (<a href="https://github.com/jquery/jquery/issues/5166">#5166</a>, <a href="https://github.com/jquery/jquery/commit/0acbe6433c2689327a7fff94f64dbee42f801ff8">0acbe643</a>)</li>
<li>Inline Sizzle into the selector module: 3.x version (<a href="https://github.com/jquery/jquery/pull/5113">#5113</a>) (<a href="https://github.com/jquery/jquery/commit/6306ca499433c45b58a02f1cf3a76cbafbc4a391">6306ca49</a>)</li>
</ul>

<h3>Tests</h3>
<ul>
<li>Indicate Chrome 112 &#038; Safari 16.4 pass the cssHas support test (3.x version) (<a href="https://github.com/jquery/jquery/commit/1a4d87afa08a68d81c38172ca10941e25633c323">1a4d87af</a>)</li>
<li>Fix tests added in gh-5233 (<a href="https://github.com/jquery/jquery/commit/759232e5af0eeba3c3107b6e8d20ab79aaf6ca6e">759232e5</a>)</li>
<li>Add tests for arary data in ajax (<a href="https://github.com/jquery/jquery/commit/4837a95b367faa613105a03fa0cb8b8fc50c02d4">4837a95b</a>)</li>
<li>Skip jQuery.Deferred.exceptionHook tests in IE 9 (<a href="https://github.com/jquery/jquery/commit/98dd622a55e672ef972cdd0854e7cd2f2db4e8ca">98dd622a</a>)</li>
<li>Test AJAX deprecated event aliases properly (<a href="https://github.com/jquery/jquery/commit/18139213fffdc7d42e3aa802d1006848bb3f95df">18139213</a>)</li>
<li>Fix selector tests in Chrome (<a href="https://github.com/jquery/jquery/commit/732592c2a779fb2001f037cce2b0cb860aeffa19">732592c2</a>)</li>
<li>Skip the native :valid tests in IE 9 (<a href="https://github.com/jquery/jquery/commit/6b2094da797087b027b453b15efe28b947641e80">6b2094da</a>)</li>
</ul>
