---
title: "jQuery 3.6.4 Released: Selector Forgiveness"
url: "https://blog.jquery.com/2023/03/08/jquery-3-6-4-released-selector-forgiveness/"
date: "Wed, 08 Mar 2023 15:52:36 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>If you&#8217;ve been following along with recent jQuery releases, we have been working on how to address the recent addition of some new selectors in browsers, especially <code>:has</code>. <a href="https://blog.jquery.com/2022/12/20/jquery-3-6-3-released-a-quick-selector-fix/">jQuery 3.6.3</a> settled on the strategy of using native <code>CSS.supports</code> to determined whether a selector should be passed directly to <code>querySelectorAll</code> or instead go through jQuery&#8217;s selector engine, as might be the case when using jQuery selector extensions, complex <code>:not()</code>, or other selectors that are valid in jQuery but not in the browser. That all technically worked fine, but <a href="https://github.com/jquery/jquery/issues/5194">came with a downside</a>. Fortunately for us, the fix is <a href="https://github.com/w3c/csswg-drafts/issues/8378">no longer necessary</a> and we can go back to the old way. More on that below.</p>



<p>As usual, the release is available on <a href="https://code.jquery.com/jquery-3.6.3.js">our cdn</a> and the npm package manager. Other third party CDNs will probably have it soon as well, but remember that we don&#8217;t control their release schedules and they will need some time. Here are the highlights for jQuery 3.6.4.</p>



<h2 class="wp-block-heading">The Difference Between What Is Right and What Is Allowed</h2>



<p>Whenever you use a selector in CSS, or JS, there is more than one spec involved. There&#8217;s a spec to determine whether a selector is valid (i.e. <a href="https://drafts.csswg.org/selectors/">Selectors</a>) and there&#8217;s a spec to guide implementers in how a selector should be parsed (i.e. the <a href="https://drafts.csswg.org/css-syntax/#consume-simple-block">parser algorithm for consuming a simple block</a>). The parser implementation is more forgiving than the selector spec itself, to allow for things like attribute selectors missing the last <code>]</code> character.</p>



<p>When we <a href="https://blog.jquery.com/2022/12/13/jquery-3-6-2-released/">addressed an issue</a> with some selectors that were being added to modern browsers—specifically <code>:has</code>—we started making use of another API available in most of our supported browsers—<code>CSS.supports</code>—to determine whether a selector could safely be passed to native <code>querySelectorAll</code> or whether it needed to go through jQuery&#8217;s selector engine. Selectors may need to bypass <code>qSA</code> for multiple reasons. It may be a jQuery-only selector extension (<code>:contains</code>), a standard selector that jQuery supports in a more robust way (<code>:not(complex)</code>), or a selector we know to be buggy sometimes (<code>:enabled</code> or <code>:disabled</code>). Whatever the reason, the introduction of &#8220;forgiving parsing&#8221; in selectors like <code>:has</code> made our previous way of determining that an issue because the browser would no longer throw errors for some truly invalid selectors. For instance, <code>:has(:contains)</code> no longer threw an error when passed to <code>querySelectorAll</code>. Neither did <code>:has(:monkey)</code> for that matter. <code>CSS.supports</code> seemed to be the answer.</p>



<p>And yet, every solution can have a trade-off. The problem now was that selectors that were technically invalid according to the Selectors spec were throwing errors. But these same selectors used to work fine because the parsers were more, for lack of a better term, forgiving. Essentially, <code>CSS.supports</code> is not as forgiving as the parser.</p>
</div></div>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>Meanwhile, in our discussions with spec writers and vendors, it was agreed that we needed to prevent issues similar to the one with <code>:has</code> from happening again in the future. What does that mean? It means we can go back to the old way . . . <a href="https://github.com/jquery/jquery/pull/5206">mostly</a>. While the spec has been updated, browsers will need some time to update their implementations. And because of that, we still recommend upgrading jQuery to the latest version.</p>
</div></div>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Upgrading</h2>



<p>We do not expect compatibility issues when upgrading from a jQuery 3.0+ version. To upgrade, have a look at the new <a href="https://jquery.com/upgrade-guide/3.5/">3.5 Upgrade Guide</a>. If you haven’t yet upgraded to jQuery 3+, first have a look at the <a href="https://jquery.com/upgrade-guide/3.0/">3.0 Upgrade Guide</a>.</p>



<p>The <a href="https://github.com/jquery/jquery-migrate#migrate-older-jquery-code-to-jquery-30">jQuery Migrate plugin</a> will help you to identify compatibility issues in your code. Please try out this new release and <a href="https://github.com/jquery/jquery/issues">let us know about any issues you experienced</a>.</p>



<p>If you can&#8217;t yet upgrade to 3.5+, Daniel Ruf has kindly provided <a href="https://github.com/DanielRuf/snyk-js-jquery-565129">patches for previous jQuery versions</a>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-3.6.4.js">https://code.jquery.com/jquery-3.6.4.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.4.min.js">https://code.jquery.com/jquery-3.6.4.min.js</a></p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@3.6.4</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Along with the regular version of jQuery that includes the ajax and effects modules, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 6k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-3.6.4.slim.js">https://code.jquery.com/jquery-3.6.4.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-3.6.4.slim.min.js">https://code.jquery.com/jquery-3.6.4.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm and Bower. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/mgol">Michal Golebiowski-Owczarek</a> and the whole jQuery team.</p>



<h2 class="wp-block-heading">We&#8217;re on Mastodon!</h2>



<p>jQuery now has its very own Mastodon account. We will be cross posting to both Twitter and Mastodon from now on. Also, you may be interested in following some of our team members that have Mastodon accounts.</p>
</div></div>



<p>jQuery: <a href="https://social.lfx.dev/@jquery">https://social.lfx.dev/@jquery</a></p>



<p>mgol: <a href="https://hachyderm.io/@mgol">https://hachyderm.io/@mgol</a></p>



<p>timmywil: <a href="https://hachyderm.io/@timmywil">https://hachyderm.io/@timmywil</a></p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/3.6.3...3.6.4">3.6.4</a></p>
</div></div>



<h3>Build</h3>
<ul>
<li>Update Sizzle from 2.3.9 to 2.3.10 (<a href="https://github.com/jquery/jquery/issues/5194">#5194</a>, <a href="https://github.com/jquery/jquery/commit/dbe09e39673fa77f7753c30fea783fc061d1230f">dbe09e39</a>)</li>
<li>Updating the 3.6-stable version to 3.6.4-pre. (<a href="https://github.com/jquery/jquery/commit/a0d68b8441ae899a37b8f61dc2c33dc7cf03d0af">a0d68b84</a>)</li>
</ul>
