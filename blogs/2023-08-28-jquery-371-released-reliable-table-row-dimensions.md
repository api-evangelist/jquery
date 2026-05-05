---
title: "jQuery 3.7.1 Released: Reliable Table Row Dimensions"
url: "https://blog.jquery.com/2023/08/28/jquery-3-7-1-released-reliable-table-row-dimensions/"
date: "Mon, 28 Aug 2023 13:40:07 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>jQuery 3.7.1 has been released! This release fixes a regression from jQuery 3.6.0 that resulted in rounded dimensions for <code>&lt;tr /&gt;</code> elements in Chrome and Safari. Also, a (mostly) internal Sizzle method, <code>jQuery.find.tokenize</code> that was on the jQuery object was accidentally removed when we <a href="https://blog.jquery.com/2023/05/11/jquery-3-7-0-released-staying-in-order/">removed Sizzle in jQuery 3.7.0</a>. That method has been restored.</p>



<p>As usual, the release is available on <a href="https://jquery.com/download/">our cdn</a> and the npm package manager. Other third party CDNs will probably have it soon as well, but remember that we don&#8217;t control their release schedules and they will need some time. Here are the highlights for jQuery 3.7.1.</p>



<h2 class="wp-block-heading">Support Test for Table Rows</h2>



<p>jQuery 3.6.0 introduced a change to a support test to account for a sudden failure from Firefox, which started including table borders in computed dimensions for <code>&lt;tr /&gt;</code> elements. That <a href="https://github.com/w3c/csswg-drafts/issues/4444">may be actually be correct</a>, but Firefox is the only browser doing it. However, that new support test didn&#8217;t account for pages with <code>* { box-sizing: border-box; }</code> in CSS. And so, the support test failed on those pages in all browsers. The result was a fallback to use <code>outerWidth</code> and <code>outerHeight</code>, which unfortunately doesn&#8217;t return fractional values. The support test has now been fixed and previous behavior has been restored for Chrome and Safari, but Firefox and IE will continue to return integers.</p>
</div></div>



<h2 class="wp-block-heading">Re-exposing Methods from Sizzle</h2>



<p>jQuery has <a href="https://blog.jquery.com/2023/05/11/jquery-3-7-0-released-staying-in-order/">inlined most of the code from Sizzle in jQuery 3.7.0</a> in preparation for larger changes coming to the jQuery selector engine in the future. For the most part, there were no functional changes, but we did accidentally privatize a method that used to be public. While <code>jQuery.find.tokenize</code> was not documented, some code relied on it being available. That method has now been restored.</p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Upgrading</h2>



<p>We do not expect compatibility issues when upgrading from a jQuery 3.0+ version. To upgrade, have a look at the new <a href="https://jquery.com/upgrade-guide/3.5/">3.5 Upgrade Guide</a>. If you haven’t yet upgraded to jQuery 3+, first have a look at the <a href="https://jquery.com/upgrade-guide/3.0/">3.0 Upgrade Guide</a>.</p>



<p>The <a href="https://github.com/jquery/jquery-migrate#migrate-older-jquery-code-to-jquery-30">jQuery Migrate plugin</a> will help you to identify compatibility issues in your code. Please try out this new release and <a href="https://github.com/jquery/jquery/issues">let us know about any issues you experienced</a>.</p>



<p>If you can&#8217;t yet upgrade to 3.5+, Daniel Ruf has kindly provided <a href="https://github.com/DanielRuf/snyk-js-jquery-565129">patches for previous jQuery versions</a>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-3.7.1.js">https://code.jquery.com/jquery-3.7.1.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.7.1.min.js">https://code.jquery.com/jquery-3.7.1.min.js</a></p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@3.7.1</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Along with the regular version of jQuery that includes the ajax and effects modules, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 6k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-3.7.1.slim.js">https://code.jquery.com/jquery-3.7.1.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.7.1.slim.min.js">https://code.jquery.com/jquery-3.7.1.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm and Bower. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/gabibguti">Gabriela Gutierrez</a>, <a href="https://github.com/mgol">Michal Golebiowski-Owczarek</a>, <a href="https://github.com/Krinkle">Timo Tijhof</a>, <a href="https://github.com/DimitriPapadopoulos">Dimitri Papadopoulos Orfanos</a> and the whole jQuery team.</p>



<h2 class="wp-block-heading">We&#8217;re on Mastodon!</h2>



<p>jQuery now has its very own Mastodon account. We will be cross posting to both Twitter and Mastodon from now on. Also, you may be interested in following some of our team members that have Mastodon accounts.</p>
</div></div>



<p>jQuery: <a href="https://social.lfx.dev/@jquery">https://social.lfx.dev/@jquery</a></p>



<p>mgol: <a href="https://hachyderm.io/@mgol">https://hachyderm.io/@mgol</a></p>



<p>timmywil: <a href="https://hachyderm.io/@timmywil">https://hachyderm.io/@timmywil</a></p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/3.7.0...3.7.1">3.7.1</a></p>
</div></div>



<h3>Build</h3>
<ul>
<li>Generate the slim build on `grunt` &#038; run `compare_size` on it (<a href="https://github.com/jquery/jquery/commit/763ade6dda092709b36d97491951bcae415d91d1">763ade6d</a>)</li>
<li>Make sure `*.cjs` &#038; `*.mjs` files use UNIX line endings as well (<a href="https://github.com/jquery/jquery/commit/3c18c1f33cfc69e1e1bd1410ab5176b2abc5fe3a">3c18c1f3</a>)</li>
<li>switch preferred email for timmywil (<a href="https://github.com/jquery/jquery/commit/72ae577c948f3577894bc7430a264ec27d9c2ba3">72ae577c</a>)</li>
<li>Build: Bump actions/checkout from 3.5.2 to 3.5.3 (<a href="https://github.com/jquery/jquery/commit/a370d7df4232c98f536bd97c049a0445d75c0f9e">a370d7df</a>)</li>
<li>Reference GitHub Actions by commit SHAs (<a href="https://github.com/jquery/jquery/issues/5266">#5266</a>, <a href="https://github.com/jquery/jquery/commit/0ea85dadaa054a0d05b3b015456c8fc67ddfec4a">0ea85dad</a>)</li>
<li>Test on Node.js 20, stop testing on Node.js 14 &#038; 19 (<a href="https://github.com/jquery/jquery/commit/b473729d0e6086b00ad72aa1e9f8f1d8ff159669">b473729d</a>)</li>
<li>Updating the 3.x-stable version to 3.7.1-pre. (<a href="https://github.com/jquery/jquery/commit/64460dac2ff6b9e4ed858928184cd119b6958b2b">64460dac</a>)</li>
</ul>

<h3>Core</h3>
<ul>
<li>Fix regression in jQuery.text() on HTMLDocument objects (<a href="https://github.com/jquery/jquery/issues/5264">#5264</a>, <a href="https://github.com/jquery/jquery/commit/44c56f87a31fbc1f43ac575cfd06a0df12073352">44c56f87</a>)</li>
</ul>

<h3>CSS</h3>
<ul>
<li>Make the reliableTrDimensions support test work with Bootstrap CSS (3.x version) (<a href="https://github.com/jquery/jquery/issues/5270">#5270</a>, <a href="https://github.com/jquery/jquery/commit/a288838c6f2ddd08c41e09b4672ad39a03822b04">a288838c</a>)</li>
</ul>

<h3>Deprecated</h3>
<ul>
<li>Define `.hover()` using non-deprecated methods (<a href="https://github.com/jquery/jquery/commit/7287894f1ac2aa25796008f1e39053969690c22f">7287894f</a>)</li>
</ul>

<h3>Docs</h3>
<ul>
<li>Fix typos found by codespell (<a href="https://github.com/jquery/jquery/commit/4a29888c759d0ca9a3ef7be90a2d7936cc48f5c8">4a29888c</a>)</li>
<li>remove stale gitter badge from readme (<a href="https://github.com/jquery/jquery/commit/141518e9c0382f6b384ad842c6349e518850ed2d">141518e9</a>)</li>
<li>Remove the &#8220;Grunt build&#8221; section from the PR template (<a href="https://github.com/jquery/jquery/commit/992a66538b535d24c9ba46c3a4492665943b40c7">992a6653</a>)</li>
</ul>

<h3>Release</h3>
<ul>
<li>revert change that broke release (<a href="https://github.com/jquery/jquery/commit/399b201bb3143a3952894cf3489b4848fc003967">399b201b</a>)</li>
<li>update authors (<a href="https://github.com/jquery/jquery/commit/f85d521cdeeb3c6d3f4563a06dba8be793e26ef0">f85d521c</a>)</li>
</ul>

<h3>Selector</h3>
<ul>
<li>Only attach the unload handler in IE &#038; Edge Legacy (<a href="https://github.com/jquery/jquery/issues/5281">#5281</a>, <a href="https://github.com/jquery/jquery/commit/87467a6f62b5fbd820ab387836e2a6fb186cbc1b">87467a6f</a>)</li>
<li>Re-expose jQuery.find.tokenize (3.x version) (<a href="https://github.com/jquery/jquery/issues/5259">#5259</a>, <a href="https://github.com/jquery/jquery/commit/13a870b60e2042cf2c5df45589ec160e19168531">13a870b6</a>)</li>
</ul>

<h3>Tests</h3>
<ul>
<li>Disable the &#8220;:lang respects escaped backslashes&#8221; test (<a href="https://github.com/jquery/jquery/issues/5271">#5271</a>, <a href="https://github.com/jquery/jquery/commit/5aa7d93acf61b165b12c4e4cc2440536a5fa94af">5aa7d93a</a>)</li>
<li>Skip a new `.text()` test in IE 9 (<a href="https://github.com/jquery/jquery/commit/b84146ce17cef7ec2ae2725ba62485368744de6c">b84146ce</a>)</li>
</ul>
