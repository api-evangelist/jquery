---
title: "jQuery 3.6.2 Released!"
url: "https://blog.jquery.com/2022/12/13/jquery-3-6-2-released/"
date: "Tue, 13 Dec 2022 15:13:13 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>You probably weren&#8217;t expecting another release so soon, but jQuery 3.6.2 has arrived! The main impetus for this release was the introduction of some new selectors in Chrome. More on that below.</p>



<p>As usual, the release is available on <a href="https://code.jquery.com/jquery-3.6.2.js">our cdn</a> and the npm package manager. Other third party CDNs will probably have it soon as well, but remember that we don&#8217;t control their release schedules and they will need some time. Here are the highlights for jQuery 3.6.2.</p>



<h2 class="wp-block-heading">undefined and whitespace-only CSS variables</h2>



<p>jQuery 3.6.1 introduced a minor regression where attempting to retrieve a value for a custom CSS property that didn&#8217;t exist (i.e. <code>$elem.css("--custom")</code>) threw an error instead of returning undefined. This has been fixed in 3.6.2. Related to that, we also made sure that whitespace-only values return the same thing across all browsers. The spec requires that CSS variable values be trimmed, but browsers are inconsistent in their trimming. We <a href="https://github.com/jquery/jquery/commit/8bea1dec18da3f3a02751dc226d51b9d0546b49e">now return undefined for whitespace-only values</a> to make it consistent with older jQuery and across the different browsers.</p>



<h2 class="wp-block-heading"><strong>.contains() with &lt;template&gt;</strong></h2>



<p>An <a href="https://github.com/jquery/jquery/issues/5147">issue was recently reported</a> that showed that a <code>&lt;template&gt;</code>&#8216;s document had its <code>documentElement</code> property set to <code>null</code>, in compliance with the spec. While it made sense semantically for a template to not yet be tied to a document, it made for an unusual case, specifically in <code>jQuery.contains()</code> and any methods relying on it. That included manipulation and selector methods. Fortunately, <a href="https://github.com/jquery/jquery/pull/5159">the fix</a> was simple.</p>



<h2 class="wp-block-heading">It wasn&#8217;t Ralph that broke the internet</h2>



<p>The internet experienced a bit of a rumble when Chrome recently introduced some new selectors, the most pertinent of which being <code>:has()</code>. It was a welcome addition, and one celebrated by the jQuery team, but a change to the spec meant that <code>:has()</code> used what&#8217;s called &#8220;forgiving parsing&#8221;. Essentially, even if the arguments for <code>:has()</code> were invalid, the browser returned no results instead of throwing an error. That was problematic in cases where <code>:has()</code> contained another jQuery selector extension (e.g. <code>:has(:contains("Item"))</code>) or contained itself (<code>:has(div:has(a))</code>). Sizzle relied on errors like that to know when to trust native <code>querySelectorAll</code> and when to run the selector through Sizzle. Selectors that used to work were broken in all jQuery versions dating back to the earliest jQuery versions.</p>



<p>And yet, this little drama didn&#8217;t last long. The Chrome team <a href="https://bugs.chromium.org/p/chromium/issues/detail?id=1358953">quickly implemented a workaround</a> to fix previous jQuery versions in the vast majority of cases. Safari handled their implementation of <code>:has()</code> a little differently and <a href="https://bugs.webkit.org/show_bug.cgi?id=244708">didn&#8217;t have the same problem</a>. <s>But, there&#8217;s still <a href="https://github.com/w3c/csswg-drafts/issues/7676">an important issue</a> open to determine how to address this in the CSS spec itself.</s> The CSSWG has since <a href="https://github.com/w3c/csswg-drafts/issues/7676#issuecomment-1341347244">resolved the issue</a>.</p>



<p>jQuery has taken steps to ensure that <a href="https://github.com/jquery/jquery/pull/5107">any forgiving parsing doesn&#8217;t break future jQuery versions</a>, even if previous jQuery versions would still be affected.</p>



<h2 class="wp-block-heading">Upgrading</h2>



<p>We do not expect compatibility issues when upgrading from a jQuery 3.0+ version. To upgrade, have a look at the new <a href="https://jquery.com/upgrade-guide/3.5/">3.5 Upgrade Guide</a>. If you haven’t yet upgraded to jQuery 3+, first have a look at the <a href="https://jquery.com/upgrade-guide/3.0/">3.0 Upgrade Guide</a>.</p>



<p>The <a href="https://github.com/jquery/jquery-migrate#migrate-older-jquery-code-to-jquery-30">jQuery Migrate plugin</a> will help you to identify compatibility issues in your code. Please try out this new release and <a href="https://github.com/jquery/jquery/issues">let us know about any issues you experienced</a>. </p>



<p>If you can&#8217;t yet upgrade to 3.5+, Daniel Ruf has kindly provided <a href="https://github.com/DanielRuf/snyk-js-jquery-565129">patches for previous jQuery versions</a>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-3.6.2.js">https://code.jquery.com/jquery-3.6.2.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.2.min.js">https://code.jquery.com/jquery-3.6.2.min.js</a> </p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@3.6.2</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Along with the regular version of jQuery that includes the ajax and effects modules, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 6k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-3.6.2.slim.js">https://code.jquery.com/jquery-3.6.2.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.2.slim.min.js">https://code.jquery.com/jquery-3.6.2.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm and Bower. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/sashashura">sashashura</a>, <a href="https://github.com/andersk">Anders Kaseorg</a>, <a href="https://github.com/mgol">Michal Golebiowski-Owczarek</a>, and the whole jQuery team.</p>



<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/3.6.1...3.6.2">3.6.2</a></p>
</div></div>



<h3>CSS</h3>
<ul>
<li>Return <code>undefined</code> for whitespace-only CSS variable values (#5120) (<a href="https://github.com/jquery/jquery/commit/8bea1dec18da3f3a02751dc226d51b9d0546b49e">8bea1dec</a>)</li>
<li>Don’t trim whitespace of undefined custom property (<a href="https://github.com/jquery/jquery/issues/5105">#5105</a>, <a href="https://github.com/jquery/jquery/commit/c0db6d70320ad6fb29a6a89aae3811a81b5adedf">c0db6d70</a>)</li>
</ul>

<h3>Selector</h3>
<ul>
<li>Manipulation: Fix DOM manip within template contents (<a href="https://github.com/jquery/jquery/issues/5147">#5147</a>, <a href="https://github.com/jquery/jquery/commit/5318e3111afd4c307ad6851682620d7413824fc5">5318e311</a>)</li>
<li>Update Sizzle from 2.3.7 to 2.3.8 (<a href="https://github.com/jquery/jquery/issues/5147">#5147</a>, <a href="https://github.com/jquery/jquery/commit/a1b7ae3b3fb86b184bd50666c211f08bbc2ee686">a1b7ae3b</a>)</li>
<li>Update Sizzle from 2.3.6 to 2.3.7 (<a href="https://github.com/jquery/jquery/issues/5098">#5098</a>, <a href="https://github.com/jquery/jquery/commit/ee0fec052bc56cc1bf229260ea9edd4ed3af99ca">ee0fec05</a>)</li>
</ul>

<h3>Tests</h3>
<ul>
<li>Remove a workaround for a Firefox XML parsing issue (<a href="https://github.com/jquery/jquery/commit/965391ab9348c624b0fba42f79d3131652d9d494">965391ab</a>)</li>
<li>Make Ajax tests pass in iOS 9 (<a href="https://github.com/jquery/jquery/commit/d051e0e3a2aac3d5cf671b180fdf7b92d627a5bc">d051e0e3</a>)</li>
</ul>
