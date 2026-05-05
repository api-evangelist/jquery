---
title: "Upgrading jQuery: Working Towards a Healthy Web"
url: "https://blog.jquery.com/2024/04/17/upgrading-jquery-working-towards-a-healthy-web/"
date: "Wed, 17 Apr 2024 17:00:00 +0000"
author: "Timmy Willison"
feed_url: "https://blog.jquery.com/feed/"
---
<p>jQuery&#8217;s influence on the web will always be evident. When it was first introduced in 2006, jQuery became a fundamental tool for web developers almost immediately. It simplified JavaScript programming, making it easier to manipulate HTML documents, handle events, perform animations, and much more. Since then, it has played and continues to play a major role in the evolution of web standards and browser capabilities.</p>



<p>With the rise of modern JavaScript frameworks, fewer developers may be choosing to use jQuery for new projects, but worldwide usage is still extremely high. After analyzing the results of a <a href="https://www.internetlivestats.com/total-number-of-websites/">survey conducted by IDC</a>, the OpenJS Foundation estimated that 90% of all websites use jQuery. And about a third of those use an outdated version.</p>



<p>The jQuery Team and OpenJS Foundation are working to fix that as part of the Healthy Web checkup campaign. This guide will explain why it is important to keep your jQuery version up to date and walk you through the process of upgrading jQuery.</p>



<h2 class="wp-block-heading">Why Is Upgrading jQuery Important for Security?</h2>



<p><strong>Security Vulnerabilities</strong>: Like any software, jQuery may contain security vulnerabilities in its codebase. These vulnerabilities can range from Cross-Site Scripting (XSS) vulnerabilities to more severe issues like Remote Code Execution (RCE). As vulnerabilities are discovered, the jQuery team releases patches and updates to address them. By upgrading to the latest version of jQuery, you ensure that your application benefits from these security fixes, reducing the risk of exploitation by attackers.</p>



<p><strong>Security Best Practices</strong>: Newer versions of jQuery often incorporate security best practices and enhancements to mitigate common security threats. These improvements may include stricter input validation, improved handling of user-generated content, and better protection against XSS attacks. By upgrading, you adopt these best practices and strengthen the security posture of your application.</p>



<p><strong>Compliance Requirements</strong>: Many industries and regulatory frameworks require organizations to maintain up-to-date software and address known security vulnerabilities promptly. Failure to upgrade jQuery and address security issues could lead to non-compliance with these requirements.</p>



<h2 class="wp-block-heading">What About Browser Support?</h2>



<p>jQuery 1.x, 2.x, and 3.x each have a different list of supported browsers. However, given current browser market usage, the <a href="https://jquery.com/browser-support/">browsers that jQuery 3.x supports</a>, which includes IE 9+, should be sufficient in almost all cases. jQuery 4.x will still support IE11, even though <a href="https://blogs.windows.com/windowsexperience/2022/06/15/internet-explorer-11-has-retired-and-is-officially-out-of-support-what-you-need-to-know/">Microsoft announced it is officially out of support</a>.</p>



<h2 class="wp-block-heading">How Do I Upgrade jQuery?</h2>



<p>The jQuery Team provides the <a href="https://github.com/jquery/jquery-migrate">jQuery Migrate plugin</a> to make upgrading jQuery as easy as possible. It is mainly meant as a development tool that generates warning messages in the browser console that can be used to identify and fix compatibility issues. It temporarily restores deprecated features and behaviors so that older code will still run on newer versions of jQuery while the compatibility issues are addressed.</p>



<p>There are two versions of jQuery Migrate: <a href="https://github.com/jquery/jquery-migrate/tree/1.x-stable">1.x</a> and <a href="https://github.com/jquery/jquery-migrate">3.x</a> (there is no Migrate 2.x). Only one version should be used at a time, but you may need to use both in succession if upgrading from a jQuery version that predates jQuery 1.9.</p>



<p>For example, if your current jQuery version is 1.4.4, first use jQuery Migrate 1.x to upgrade to jQuery 1.12.4 and then use jQuery Migrate 3.x to upgrade to the latest jQuery (3.7.1, as of this writing). If your current version is 2.2.4, you only need to use jQuery Migrate 3.x to upgrade to the latest jQuery.</p>



<h2 class="wp-block-heading">Using jQuery Migrate</h2>



<p>First, add jQuery Migrate to your page *after* loading jQuery.</p>



<pre class="wp-block-preformatted">&lt;script src="https://code.jquery.com/jquery-3.7.1.js">&lt;/script>
&lt;script src="https://code.jquery.com/jquery-migrate-3.4.1.js">&lt;/script></pre>



<p>Then, test your website or application. As different jQuery APIs are used, jQuery Migrate will log messages to the console warning about any deprecations or breaking changes. Address each warning one at a time.</p>



<p>Finally, when no more warnings are logged to the console and all breaking changes have been addressed, the jQuery Migrate can be removed and migration is complete!</p>



<p>See the <a href="https://github.com/jquery/jquery-migrate">jQuery Migrate README</a> for more details.</p>



<h2 class="wp-block-heading">jQuery Upgrade Guides</h2>



<p>The <a href="https://jquery.com/upgrade-guide/">jQuery Upgrade Guides</a> can be helpful when you&#8217;re looking for more details on a breaking change, or you just want to see the full list of breaking changes for each version. There are upgrade guides for jQuery <a href="https://jquery.com/upgrade-guide/1.9/">1.9</a>, <a href="https://jquery.com/upgrade-guide/3.0/">3.0</a> and <a href="https://jquery.com/upgrade-guide/3.5/">3.5</a> that list all of the breaking changes that happened in those releases. Most of the breaking changes listed will probably not apply to your code, but these guides add some context and explanation for each change.</p>



<h2 class="wp-block-heading">A Note on Future jQuery Versions</h2>



<p>With <a href="https://blog.jquery.com/2024/02/06/jquery-4-0-0-beta/">jQuery 4.0 on the horizon</a>, you may wonder what the process will be for upgrading to jQuery 4.x. The answer is that it will be the same as upgrading to jQuery 3.x and it can still be done in one step. In other words, there will be no need to upgrade to jQuery 3.x before upgrading to jQuery 4.x. You will be able to upgrade straight from 1.9+ to jQuery 4.x. We will also have an upgrade guide ready for jQuery 4.0.</p>



<h2 class="wp-block-heading">Conclusion</h2>



<p>Upgrading jQuery is essential for maintaining the security, performance, and compatibility of your web applications. By following the steps outlined in this guide, you can safely upgrade to the latest version of jQuery and take advantage of its new features and improvements while ensuring that your web application remains protected against any discovered vulnerabilities. Remember to regularly check for updates and stay informed about new releases to keep your codebase up to date.</p>
