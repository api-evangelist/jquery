---
title: "jQuery 3.6.3 Released: A Quick Selector Fix"
url: "https://blog.jquery.com/2022/12/20/jquery-3-6-3-released-a-quick-selector-fix/"
date: "Tue, 20 Dec 2022 21:35:36 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>Last week, we released jQuery 3.6.2. There were several changes in that release, but the most important one addressed an issue with some new selectors introduced in most browsers, like <code>:has()</code>. We wanted to release jQuery 3.6.3 quickly because an <a href="https://github.com/jquery/jquery/issues/5177">issue was reported</a> that revealed a problem with our original fix. More details on that below.</p>



<p>As usual, the release is available on <a href="https://code.jquery.com/jquery-3.6.3.js">our cdn</a> and the npm package manager. Other third party CDNs will probably have it soon as well, but remember that we don&#8217;t control their release schedules and they will need some time. Here are the highlights for jQuery 3.6.3.</p>



<h2 class="wp-block-heading">Using <code>CSS.supports</code> the right way</h2>



<p>After the <a href="https://github.com/jquery/jquery/issues/5098">issue with <code>:has</code></a> that was <a href="https://blog.jquery.com/2022/12/13/jquery-3-6-2-released/">fixed in jQuery 3.6.2</a>, we started using <code>CSS.supports( "selector(SELECTOR)")</code> to determine whether a selector would be valid if passed directly to <code>querySelectorAll</code>. When <code>CSS.supports</code> returned <code>false</code>, jQuery would then fall back to its own selector engine (Sizzle). Apparently, our implementation had a bug. In <code>CSS.supports( "selector(SELECTOR)")</code>, <a href="https://w3c.github.io/csswg-drafts/css-conditional-4/#at-supports-ext">SELECTOR</a> needed to be a <code><a href="https://w3c.github.io/csswg-drafts/selectors-4/#typedef-complex-selector">&lt;complex-selector></a></code> and not a <code><a href="https://w3c.github.io/csswg-drafts/selectors-4/#typedef-complex-selector-list">&lt;complex-selector-list></a></code>. For example:</p>



<pre class="wp-block-code"><code>CSS.supports("selector(div)"); // true
CSS.supports("selector(div, span)"); // false</code></pre>



<p>This meant that all complex selector lists were passed through Sizzle instead of <code>querySelectorAll</code>. That&#8217;s not necessarily a problem in most cases, but it does mean that some level 4 selectors that were supported in browsers but not in Sizzle, like <code>:valid</code>, no longer worked if it was part of a selector list (e.g. <code>"input:valid, div"</code>). It should be noted this currently only affects Firefox, but it will be true in all browsers as they roll out changes to <code>CSS.supports</code>.</p>



<p>This has now been fixed in jQuery 3.6.3 and it is the only functional change in this release.</p>
</div></div>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Upgrading</h2>



<p>We do not expect compatibility issues when upgrading from a jQuery 3.0+ version. To upgrade, have a look at the new <a href="https://jquery.com/upgrade-guide/3.5/">3.5 Upgrade Guide</a>. If you haven’t yet upgraded to jQuery 3+, first have a look at the <a href="https://jquery.com/upgrade-guide/3.0/">3.0 Upgrade Guide</a>.</p>



<p>The <a href="https://github.com/jquery/jquery-migrate#migrate-older-jquery-code-to-jquery-30">jQuery Migrate plugin</a> will help you to identify compatibility issues in your code. Please try out this new release and <a href="https://github.com/jquery/jquery/issues">let us know about any issues you experienced</a>. </p>



<p>If you can&#8217;t yet upgrade to 3.5+, Daniel Ruf has kindly provided <a href="https://github.com/DanielRuf/snyk-js-jquery-565129">patches for previous jQuery versions</a>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-3.6.3.js">https://code.jquery.com/jquery-3.6.3.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.3.min.js">https://code.jquery.com/jquery-3.6.3.min.js</a> </p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@3.6.3</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Along with the regular version of jQuery that includes the ajax and effects modules, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 6k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-3.6.3.slim.js">https://code.jquery.com/jquery-3.6.3.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.3.slim.min.js">https://code.jquery.com/jquery-3.6.3.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm and Bower. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/mgol">Michal Golebiowski-Owczarek</a> and the whole jQuery team.</p>



<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/3.6.2...3.6.3">3.6.3</a></p>
</div></div>



<h3>Build</h3>
<ul>
<li>remove stale Insight package from custom builds (<a href="https://github.com/jquery/jquery/commit/81d5bd17fd2f82779351c101de280f89c22948ac">81d5bd17</a>)</li>
<li>Updating the 3.x-stable version to 3.6.3-pre. (<a href="https://github.com/jquery/jquery/commit/2c5b47c4def78e447d2eb97a6f382e2b713165f8">2c5b47c4</a>)</li>
</ul>

<h3>Selector</h3>
<ul>
<li>Update Sizzle from 2.3.8 to 2.3.9 (<a href="https://github.com/jquery/jquery/issues/5177">#5177</a>, <a href="https://github.com/jquery/jquery/commit/8989500e6c695d10806400d20381da4d1ed34a7b">8989500e</a>)</li>
</ul>
