---
title: "Second Beta of jQuery 4.0.0"
url: "https://blog.jquery.com/2024/07/17/second-beta-of-jquery-4-0-0/"
date: "Wed, 17 Jul 2024 14:03:14 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<p>Last February, we <a href="https://blog.jquery.com/2024/02/06/jquery-4-0-0-beta/">released the first beta of jQuery 4.0.0</a>. We&#8217;re now ready to release a second, and we expect a release candidate to come soon<img alt="™" class="wp-smiley" src="https://s.w.org/images/core/emoji/17.0.2/72x72/2122.png" style="height: 1em;" />. This release comes with a <a href="https://github.com/jquery/jquery/pull/5418">major rewrite to jQuery&#8217;s testing infrastructure</a>, which removed all deprecated or under-supported dependencies. But the main change that warranted a second beta was a fix to the <a href="https://github.com/jquery/jquery/pull/5429">exports field for bundlers</a>. More on that and other changes below.</p>



<p>Many of the breaking changes in jQuery 4.0.0 are ones the team has wanted to make for years, but couldn&#8217;t in a patch or minor release. We&#8217;ve trimmed legacy code (including removing support for IE before version 11), removed some previously-deprecated APIs, removed some internal-only parameters to public functions that were never documented, and dropped support for some &#8220;magic&#8221; behaviors that were overly complicated.</p>



<p>We will publish a comprehensive upgrade guide before final release, to outline the removed code and how to migrate. The <a href="https://github.com/jquery/jquery-migrate">jQuery Migrate plugin</a> will also be ready to assist. For now, please try out this release and <a href="https://github.com/jquery/jquery/issues">let us know if you encounter any issues</a>.</p>



<p>As usual, the release is available on <a href="https://jquery.com/download/">our CDN</a> and the npm package manager. Third party CDNs will not be hosting this beta release, but will host the 4.0.0 final release later. Here are some highlights for jQuery 4.0.0 beta.2.</p>



<h2 class="wp-block-heading">CommonJS + ESM: Strange Bedfellows</h2>



<p>There are many different ways to include jQuery in a project. Supporting all of them can be difficult, especially when the environment supports both CommonJS and ESM modules. We wanted to support all of the ways jQuery might be included, whether using a named export or the default export. Also, we wanted to ensure jQuery was only ever included once, even when jQuery was both <code>import</code>ed using ESM and <code>require</code>d using CommonJS in the same environment or bundle. We think we&#8217;ve worked out a solution that supports Node.js and bundlers like rollup, webpack, and parcel. More details can be found in the <a href="https://github.com/jquery/jquery/pull/5429">PR</a>. Also, we created a <a href="https://github.com/jquery/jquery/wiki/jQuery-4-exports-explainer">wiki page</a> to explain how the <code>exports</code> property in jQuery&#8217;s <code>package.json</code> will work in 4.0.</p>



<h2 class="wp-block-heading">Boolean Attributes: To Be Or &#8230;</h2>



<p>The HTML spec defines boolean attributes that often correlate with boolean properties. If the attribute is missing, it correlates with the <code>false</code> property value, if it&#8217;s present &#8211; the true property value. The only valid values for boolean content attributes are empty string or the full attribute name (e.g. <code>checked="checked"</code>).</p>



<p>jQuery has historically tried to be helpful here and treated boolean attributes in a special way in the <code>.attr()</code> API:</p>



<ol class="wp-block-list">
<li>For the getter, as long as the attribute was present, it was returning the<br />attribute name lowercased, ignoring the value.</li>



<li>For the setter, it was removing the attribute when <code>false</code> was passed;<br />otherwise, it was ignoring the passed value and set the attribute &#8211;<br />interestingly, in jQuery &gt;=3 not lowercased anymore.</li>
</ol>



<p>The problem is the spec occasionally converts boolean attributes into ones with additional attribute values with special behavior &#8211; one such example is the new <a href="https://html.spec.whatwg.org/multipage/interaction.html#the-hidden-attribute"><code>"until-found"</code> value for the <code>hidden</code> attribute</a>. Our setter normalization meant passing those values was impossible with <code>.attr()</code> (<code>.prop()</code> was unaffected). Also, new boolean attributes were introduced occasionally and jQuery could not easily add them to the list without incurring breaking changes.</p>



<p>This patch removes any special handling of boolean attributes &#8211; the getter returns the value as-is and the setter sets the provided value, with one exception. To maintain backwards compatibility, this patch makes the <code>false</code> boolean value trigger attribute removal for ALL non-ARIA attributes. For example, <code>.attr( "checked", false )</code> will continue to remove the <code>checked</code> attribute, which is the only way the corresponding property will be set to <code>false</code>. ARIA attributes are exempt from the rule since many of them recognize the string <code>"false"</code> as a valid value with semantics different than the attribute missing. To remove an ARIA attribute, use <code>.removeAttr()</code> or pass <code>null</code> as the value to <code>.attr()</code>.</p>



<h2 class="wp-block-heading">Position of Elements In Tables</h2>



<p>jQuery 4.0.0-beta.2 also fixes some inconsistent behavior when finding the position of elements within tables. The offset parent on which the position was based could change depending on whether the element&#8217;s <code>position</code> style was <code>static</code> or <code>relative</code>.</p>



<pre class="wp-block-preformatted">&lt;div id="container" style="position: relative;"&gt;
    &lt;table&gt;
        &lt;tr&gt;
            &lt;td&gt;
                &lt;span id="static"&gt;&lt;/span&gt;
                &lt;span id="relative" style="position: relative;"&gt;&lt;/span&gt;
            &lt;/td&gt;
        &lt;/tr&gt;
    &lt;/table&gt;
&lt;/div&gt;</pre>



<p>Previously,&nbsp;<code>$('#static').position()</code>&nbsp;was returning the position relative to the containing&nbsp;<code>&lt;td&gt;</code>&nbsp;element, while&nbsp;<code>$('#relative').position()</code>&nbsp;was returning the position relative to&nbsp;<code>#container</code>.</p>



<p>Now, both elements return their position relative to <code>#container</code>.</p>



<h2 class="wp-block-heading">Download</h2>



<p>You can get the files from the jQuery CDN, or link to them directly:</p>



<p><a href="https://code.jquery.com/jquery-4.0.0-beta.2.js">https://code.jquery.com/jquery-4.0.0-beta.2.js</a></p>



<p><a href="https://code.jquery.com/jquery-4.0.0-beta.2.min.js">https://code.jquery.com/jquery-4.0.0-beta.2.min.js</a></p>



<p>You can also get this release from npm:</p>



<p><code>npm install jquery@4.0.0-beta.2</code></p>



<h3 class="wp-block-heading">Slim build</h3>



<p>Sometimes you don&#8217;t need ajax, or you prefer to use one of the many standalone libraries that focus on ajax requests. And often it is simpler to use a combination of CSS and class manipulation for web animations. Finally, all of jQuery&#8217;s supported browsers (except for IE11) now have support for native Promises across the board, so Deferreds and Callbacks are no longer needed in most cases. Along with the regular version of jQuery that includes everything, we&#8217;ve released a &#8220;slim&#8221; version that excludes these modules. The size of jQuery is very rarely a load performance concern these days, but the slim build is about 8k gzipped bytes smaller than the regular version. These files are also available in the npm package and on the CDN:</p>



<p><a href="https://code.jquery.com/jquery-4.0.0-beta.2.slim.js">https://code.jquery.com/jquery-4.0.0-beta.2.slim.js</a></p>



<p><a href="https://code.jquery.com/jquery-4.0.0-beta.2.slim.min.js">https://code.jquery.com/jquery-4.0.0-beta.2.slim.min.js</a></p>



<p>These updates are already available as the current versions on npm. Information on all the ways to get jQuery is available at <a href="https://jquery.com/download/">https://jquery.com/download/</a>. Public CDNs receive their copies today, please give them a few days to post the files. If you’re anxious to get a quick start, use the files on our CDN until they have a chance to update.</p>



<h2 class="wp-block-heading">Thanks</h2>



<p>Thank you to all of you who participated in this release by submitting patches, reporting bugs, or testing, including <a href="https://github.com/mgol">Michał Gołębiowski-Owczarek</a>, <a href="https://github.com/xwxtwd">J.Son</a>, <a href="https://github.com/Minimaximize">Liam James</a> and the whole jQuery team.</p>



<h2 class="wp-block-heading">We&#8217;re on Mastodon!</h2>



<p>jQuery has a Mastodon account! We now post releases and other updates to both X and Mastodon. Also, you may be interested in following some of our team members that have Mastodon accounts.</p>
</div></div>



<p>jQuery: <a href="https://social.lfx.dev/@jquery">https://social.lfx.dev/@jquery</a></p>



<p>mgol: <a href="https://hachyderm.io/@mgol">https://hachyderm.io/@mgol</a></p>



<p>timmywil: <a href="https://hachyderm.io/@timmywil">https://hachyderm.io/@timmywil</a></p>



<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">
<h2 class="wp-block-heading">Changelog</h2>



<p><strong>Full changelog: </strong><a href="https://github.com/jquery/jquery/compare/4.0.0-beta...4.0.0-beta.2">4.0.0-beta.2</a></p>
</div></div>



<h2>Attributes</h2>
<ul>
<li>Make <code>.attr( name, false )</code> remove for all non-ARIA attrs (<a href="https://github.com/jquery/jquery/issues/5388">#5388</a>, <a href="https://github.com/jquery/jquery/commit/063831b6378d518f9870ec5c4f1e7d5d16e04f36">063831b6</a>)</li>
</ul>
<h2>Build</h2>
<ul>
<li>Bump the github-actions group with 2 updates (<a href="https://github.com/jquery/jquery/commit/3a98ef91dfa0b4897df7562f40bfd1715f5fc30e">3a98ef91</a>)</li>
<li>upgrade dependencies; fix bundler tests on windows (<a href="https://github.com/jquery/jquery/commit/cb8ab6ccdb8a7b843301793d4b7138a5a3750d6b">cb8ab6cc</a>)</li>
<li>improve specificity of eslint config; add ecma versions (<a href="https://github.com/jquery/jquery/commit/74970524e5e164c72ec0415267b1e057280c9455">74970524</a>)</li>
<li>Bump the github-actions group with 2 updates (<a href="https://github.com/jquery/jquery/commit/46b9e4803ec3506e830ea6b49541ea29717ed460">46b9e480</a>)</li>
<li>Group dependabot PRs updating GitHub Actions (<a href="https://github.com/jquery/jquery/commit/3cac1465b4b5539bb679a517fbb52e5419c1866e">3cac1465</a>)</li>
<li>Bump actions/cache, actions/checkout &amp; github/codeql-action (<a href="https://github.com/jquery/jquery/commit/df1df9503afad78bec3ba5217f9a9efce49fe634">df1df950</a>)</li>
<li>Bump express from 4.18.3 to 4.19.2 (<a href="https://github.com/jquery/jquery/commit/691c0aeeded5dea1ca2a0c5474c7adfdb1dadffe">691c0aee</a>)</li>
<li>make compare size cache readable for manual edits (<a href="https://github.com/jquery/jquery/commit/783c9d6958fd20a6a9a199aeecad605a59686992">783c9d69</a>)</li>
<li>fix size comparison for slim files when the branch is dirty (<a href="https://github.com/jquery/jquery/commit/8a3a74c475f92148675af4ee3f77e3d1746e6e88">8a3a74c4</a>)</li>
<li>migrate more uses of fs.promises; use node: protocol (<a href="https://github.com/jquery/jquery/commit/ae7f6139cc8e21a7116e8de30d26ca38426bde0b">ae7f6139</a>)</li>
<li>Bump github/codeql-action from 3.24.0 to 3.24.6 (<a href="https://github.com/jquery/jquery/commit/ae67ace649fd2ac49eb74709c3d0a5952d0dc3bb">ae67ace6</a>)</li>
<li>Bump actions/cache from 4.0.0 to 4.0.1 (<a href="https://github.com/jquery/jquery/commit/68f772e003ee0f39cf0f755070fb4e9ec9e90973">68f772e0</a>)</li>
<li>drop support for Node 10 (<a href="https://github.com/jquery/jquery/commit/5aa7ed888ddf314fba3c4f8750b891cb6427c9c2">5aa7ed88</a>)</li>
<li>add GitHub Actions workflow to update Filestash (<a href="https://github.com/jquery/jquery/commit/0293d3e30dd68bfe92be1d6d29f9b9200d1ae917">0293d3e3</a>)</li>
<li>update jenkins script to only build (<a href="https://github.com/jquery/jquery/commit/c21c6f4ddf96a5928e03bdd2bf0da87899f2ec24">c21c6f4d</a>)</li>
<li>Bump actions/cache &amp; github/codeql-action (#5402) (<a href="https://github.com/jquery/jquery/commit/bf11739f6c6926bc9bc1b5a1460505d3b7ef8b01">bf11739f</a>)</li>
</ul>
<h2>CSS</h2>
<ul>
<li>Tests: Fix tests &amp; support tests under CSS Zoom (<a href="https://github.com/jquery/jquery/issues/5489">#5489</a>, <a href="https://github.com/jquery/jquery/commit/071f6dba6bd1d8db3f36ce4694aab5ff437b9e36">071f6dba</a>)</li>
</ul>
<h2>Core</h2>
<ul>
<li>Fix the exports setup to make bundlers work with ESM &amp; CommonJS (<a href="https://github.com/jquery/jquery/issues/5416">#5416</a>, <a href="https://github.com/jquery/jquery/commit/60f11b58bfeece6b6d0189d7d19b61a4e1e61139">60f11b58</a>)</li>
</ul>
<h2>Docs</h2>
<ul>
<li>Update remaining HTTP URLs to HTTPS (<a href="https://github.com/jquery/jquery/commit/7cdd8374234b77a3c70dd511a1b06066afb146bb">7cdd8374</a>)</li>
</ul>
<h2>Event</h2>
<ul>
<li>Increase robustness of an inner native event in leverageNative (<a href="https://github.com/jquery/jquery/issues/5459">#5459</a>, <a href="https://github.com/jquery/jquery/commit/527fb3dcf0dcde69302a741dfc61cbfa58e99eb0">527fb3dc</a>)</li>
</ul>
<h2>Offset</h2>
<ul>
<li>Increase search depth when finding the 'real' offset parent (<a href="https://github.com/jquery/jquery/commit/556eaf4a193287c306d163635cbb5f5c95a22a84">556eaf4a</a>)</li>
</ul>
<h2>Release</h2>
<ul>
<li>ensure builds have the proper version (<a href="https://github.com/jquery/jquery/commit/3e612aeeb3821c657989e67b43c9b715f5cd32e2">3e612aee</a>)</li>
<li>set preReleaseBase in config file (<a href="https://github.com/jquery/jquery/commit/1fa8df5dbd5d84cf55882a38eb6e571abd0aa938">1fa8df5d</a>)</li>
<li>fix running pre/post release scripts in windows (<a href="https://github.com/jquery/jquery/commit/5518b2da1816b379b573abc55ba92f02776a3486">5518b2da</a>)</li>
<li>update AUTHORS.txt (<a href="https://github.com/jquery/jquery/commit/862e7a1882f3f737db7dde1b5ecda9766d61694a">862e7a18</a>)</li>
<li>migrate release process to release-it (<a href="https://github.com/jquery/jquery-release/issues/114">jquery/jquery-release#114</a>, <a href="https://github.com/jquery/jquery/commit/2646a8b07fcc2cf7cf384724f622eb0c27f9166c">2646a8b0</a>)</li>
<li>add factory files to release distribution (<a href="https://github.com/jquery/jquery/issues/5411">#5411</a>, <a href="https://github.com/jquery/jquery/commit/1a324b0792ba8d032b89dd8bf78bbf5caa535367">1a324b07</a>)</li>
</ul>
<h2>Tests</h2>
<ul>
<li>remove unnecessary scroll feature test (<a href="https://github.com/jquery/jquery/commit/ea31e4d57c05a072df98a08df6532b2afb679d30">ea31e4d5</a>)</li>
<li>Align <code>:has</code> selector tests with <code>3.x-stable</code> (<a href="https://github.com/jquery/jquery/commit/f2d9fde5f34c83a098fa2074ed808311086d9d23">f2d9fde5</a>)</li>
<li>revert concurrency group change (<a href="https://github.com/jquery/jquery/commit/fa73e2f1b25304c93006dd45b6cba24f663e2ae7">fa73e2f1</a>)</li>
<li>include github ref in concurrency group (<a href="https://github.com/jquery/jquery/commit/5880e02707dcefc4ec527bd1c56f64b8b0eba391">5880e027</a>)</li>
<li>Make the beforeunload event tests work regardless of extensions (<a href="https://github.com/jquery/jquery/commit/399a78ee9fc5802509df462a2851aef1b60b7fbc">399a78ee</a>)</li>
<li>share queue/browser handling for all worker types (<a href="https://github.com/jquery/jquery/commit/284b082eb86602705519d6ca754c40f6d2f8fcc0">284b082e</a>)</li>
<li>improve diffing for values of different types (<a href="https://github.com/jquery/jquery/commit/b9d333acef65a68d68b169b6acbbf96965414728">b9d333ac</a>)</li>
<li>show any and all actual/expected values (<a href="https://github.com/jquery/jquery/commit/f80e78ef3e7ded1fc693465d02dfb07510ded0ab">f80e78ef</a>)</li>
<li>add diffing to test reporter (<a href="https://github.com/jquery/jquery/commit/44fb7fa220e2dc2780203b128df2181853b3300f">44fb7fa2</a>)</li>
<li>add actual and expected messages to test reporter (<a href="https://github.com/jquery/jquery/commit/1e84908baf13da63c33ee66c857e45c2f02eced7">1e84908b</a>)</li>
<li>fix worker restarts for failed browser acknowledgements (<a href="https://github.com/jquery/jquery/commit/fedffe7448b9e2328b43641158335be18eff5f69">fedffe74</a>)</li>
<li>add &#8211;hard-retries option to test runner (<a href="https://github.com/jquery/jquery/commit/822362e6efae90610d7289b46477c7fa22758141">822362e6</a>)</li>
<li>fix cleanup in cases where server doesn't stop (<a href="https://github.com/jquery/jquery/commit/0754d5966400ff12e216031d68cb25ea314eac55">0754d596</a>)</li>
<li>fix flakey message logs; ignore delete worker failures (<a href="https://github.com/jquery/jquery/commit/02d23478289e45af3d7f4673b9ffe84591c23472">02d23478</a>)</li>
<li>reuse browser workers in BrowserStack tests (#5428) (<a href="https://github.com/jquery/jquery/commit/95a4c94b8131b737d8f160c582a4acfe2b65e0f8">95a4c94b</a>)</li>
<li>Use allowlist instead of whitelist (<a href="https://github.com/jquery/jquery/commit/2b97b6bbcfc67c234b86d41451aac7cdd778e855">2b97b6bb</a>)</li>
<li>migrate testing infrastructure to minimal dependencies (<a href="https://github.com/jquery/jquery/commit/dfc693ea25fe85e5f29da23752b0c7c8d285fbf0">dfc693ea</a>)</li>
<li>Fix Karma tests on Node.js 20 (<a href="https://github.com/jquery/jquery/commit/d478a1c0226b7825a99718bf605ef9727ee4beca">d478a1c0</a>)</li>
</ul>
