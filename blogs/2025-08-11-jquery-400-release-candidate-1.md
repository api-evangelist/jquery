---
title: "jQuery 4.0.0 Release Candidate 1"
url: "https://blog.jquery.com/2025/08/11/jquery-4-0-0-release-candidate-1/"
date: "Mon, 11 Aug 2025 17:35:14 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>It&#8217;s here! Almost. jQuery 4.0.0-rc.1 is now available. It&#8217;s our way of saying, &#8220;we think this is ready; now poke it with many sticks&#8221;. If nothing is found that requires a second release candidate, jQuery 4.0.0 final will follow. Please try out this release and <a href="https://github.com/jquery/jquery/issues">let us know if you encounter any issues</a>.</p>



<p>A <a href="https://stage.jquery.com/upgrade-guide/4.0/">4.0 upgrade guide</a> and <a href="https://github.com/jquery/jquery-migrate/releases/tag/4.0.0-beta.1">jQuery Migrate release</a> are also now available, but both are subject to changes before the final jQuery Core release.</p>



<p>Many of the breaking changes in jQuery 4.0.0 are ones the team has wanted to make for years, but couldn&#8217;t in a patch or minor release. We&#8217;ve trimmed legacy code (including removing support for IE before version 11), removed some previously-deprecated APIs, removed some internal-only parameters to public functions that were never documented, and dropped support for some &#8220;magic&#8221; behaviors that were overly complicated.</p>



<p>As usual, the release is available on our CDN and the npm package manager. Third party CDNs will not be hosting this rc release, but will host the 4.0.0 final release later. Here are some highlights for jQuery 4.0.0 rc.1.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-4.0.0-rc.1.js">https://code.jquery.com/jquery-4.0.0-rc.1.js</a></p>



<p><a href="https://code.jquery.com/jquery-4.0.0-rc.1.min.js">https://code.jquery.com/jquery-4.0.0-rc.1.min.js</a></p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@4.0.0-rc.1</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Finally, all of jQuery&#8217;s supported browsers (except for IE11) now have support for native Promises across the board, so Deferreds and Callbacks are no longer needed in most cases. Along with the regular version of jQuery that includes everything, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 8k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-4.0.0-rc.1.slim.js">https://code.jquery.com/jquery-4.0.0-rc.1.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-4.0.0-rc.1.slim.min.js">https://code.jquery.com/jquery-4.0.0-rc.1.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/ac-mmi">ac-mmi</a>, <a href="https://github.com/mgol">Michał Gołębiowski-Owczarek</a>, <a href="https://github.com/neogy-akash">neogy-akash</a>, and the whole jQuery team.</p>



<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/4.0.0-beta.2...4.0.0-rc.1">4.0.0-rc.1</a></p>
</div></div>



<h2>CSS</h2>
<ul>
<li>Fix dimensions of table <code>&lt;col&gt;</code> elements (<a href="https://github.com/jquery/jquery/issues/5628">#5628</a>, <a href="https://github.com/jquery/jquery/commit/eca2a56457e1c40c071aeb3ac87efeb8bbb8013e">eca2a564</a>)</li>
<li>Drop the cache in finalPropName (<a href="https://github.com/jquery/jquery/commit/640d5825df5ff223560c5690f1a268681c32f9fa">640d5825</a>)</li>
</ul>
<h2>Core</h2>
<ul>
<li>Remove obsolete workarounds, update support comments (<a href="https://github.com/jquery/jquery/commit/e2fe97b7f15cf5ee2e44566b381f7bf214e491b1">e2fe97b7</a>)</li>
<li>Switch <code>$.parseHTML</code> from <code>document.implementation</code> to <code>DOMParser</code> (<a href="https://github.com/jquery/jquery/commit/0e123509d529456ddf130abb97e6266b53f62c50">0e123509</a>)</li>
</ul>
<h2>Docs</h2>
<ul>
<li>Align CONTRIBUTING.md with <code>3.x-stable</code> (<a href="https://github.com/jquery/jquery/commit/d92810614b53270a8f014db14022887ee3383fd5">d9281061</a>)</li>
<li>Update CONTRIBUTING.md (<a href="https://github.com/jquery/jquery/commit/4ef25b0de4a847f14ba2f88e309eaf759e035d78">4ef25b0d</a>)</li>
<li>add version support section to README (<a href="https://github.com/jquery/jquery/commit/cbc2bc1fd37bb6af5d2c60cf666265c4d438200f">cbc2bc1f</a>)</li>
</ul>
<h2>Event</h2>
<ul>
<li>Use <code>.preventDefault()</code> in beforeunload (<a href="https://github.com/jquery/jquery/commit/7c123dec4b96e7c3ce5f5a78e828c8aa335bea98">7c123dec</a>)</li>
</ul>
<h2>Manipulation</h2>
<ul>
<li>Make jQuery.cleanData not skip elements during cleanup (<a href="https://github.com/jquery/jquery/issues/5214">#5214</a>, <a href="https://github.com/jquery/jquery/commit/3cad5c435aa2333c39baa55a8bceb2b6bf1e2721">3cad5c43</a>)</li>
</ul>
<h2>Selector</h2>
<ul>
<li>Properly deprecate <code>jQuery.expr[ &quot;:&quot; ]</code>/<code>jQuery.expr.filters</code> (<a href="https://github.com/jquery/jquery/commit/329661fd538a07993a2fcfa2a75fdd7f5667f86c">329661fd</a>)</li>
</ul>



<p></p>
