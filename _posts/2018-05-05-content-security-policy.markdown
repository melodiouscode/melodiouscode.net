---
layout: post
title: Content Security Policies
featured: true
date: '2018-05-05 15:55:04'
image: /images/posts/ilya-pavlov-87438-unsplash-min2.jpg
tags:
- security
- https-series
- csp
---


>This post is part of a [series on HTTPS and browser security](https://melodiouscode.net/tag/https-series/); it is partly to spread knowledge, but mostly to allow me to learn more about the subject by putting it 'down on paper'! Enjoy, and please comment, correct, and discuss.

In the last post of this series I wrote about [HSTS](https://melodiouscode.net/https-is-just-the-tip-of-the-sword/); like HSTS a Content Security Policy is a browser header (or a tag, but more on that later) which can be used to improve a websites security footing.

## What is a Content Security Policy?
The easiest way to explain a Content Security Policy (CSP) is with the idea of a whitelist; whitelists act as an allowed set of values for a system. You may have heard of a blacklist before; a list of things which are not allowed, you employer/school will almost certainly have a blacklist of websites you are not authorised to visit (naughty or dangerous ones). A whitelist is the opposite; to use the website blocking analogy a whitelist would contain only the websites you are allowed to access (a much more restrictive setting than a blacklist).

A CSP outlines the resources which a website may use; this whitelist prevents any unauthorised or unexpected resources from being used on a website. These resources may be something as simple as a CSS or JS file served from your server, but they could also be dangerous injected javascript or hijacked third-party resources. A CSP is the first step towards mitigating the risk of unauthorised or unexpected page resources.

## Whitelisting content sources
The CSP header is a simple list of resource types and the locations that are authorised to serve them. The most basic of CSPs would be:
<pre><code data-language="html">Content-Security-Policy: default-src 'self'</code></pre>

This policy states that the website should only load resources from its own URL path (in the case of this page that would be melodiouscode.net). Any resource outside of that path (nastyhacker.com, googleanalytics.com etc) would be blocked by the browser. Although effective this policy is very restrictive; few sites only use their own resources and serving everything yourself is not the most efficient mechanism anymore (think of CDNs, Cloudflare, etc).

The CSP definition contains a number of restriction types, or directives, which can be used to fine-tune your whitelist.
## Directives
There are a number of directives which can be used to tailor your websites whitelist the three obvious ones are:
+ **default-src**: The default directive defines the fallback list of sources; used in the event that you do not specify a specific directive.
+ **script-src**: The script source is perhaps the most obvious directive; it defines the list of sources which can load script files (javascript), including the use of inline scripts and the 'eval' command. By default inline scripts and 'eval' are disabled.
+ **style-src**: The style source defines which sources can load stylesheets (CSS files), including the use of inline style tags and style attributes. By default inline styles are disabled.

In addition to the above three directives there are also directives for images, fonts, connect sources, objects, frames, and several others.

CSPs do not just act as restrictions for resource sources; there are also a number of directives which can be used to upgrade or improve the security of a website such as:
+ **require-sri-for**: This attribute causes a browser to only load scripts/styles which have Sub Resource Integrity attributes set (more about them in a later module).
+ **upgrade-insecure-requests**: As you would expect this directive encourages the browser to switch any HTTP requests into HTTPS requests where possible.
For a full list of the directives and a playground for creating a CSP header, I suggest taking a look at the [CSP Builder](https://report-uri.com/home/generate) provided by [report-uri](https://report-uri.com). Report-uri.com is a fantastic resource for anyone using a CSP on their website; not only do they help you to get to grips with the policy but their services allows you to monitor how your policy is enforced.

## Testing for and reporting on policy violations
Setting a policy without testing it would be a mistake; you may end up breaking your website without realising (you would have to test every page in every potential scenario to be sure it was 100% sure). Luckily there are two easy ways to review your CSP:

1. The browser console; all web browsers contain a console which script/etc errors are logged to.  The console will list all the violations as they happen; a great way to test your policy on the fly. However not a great way to ensure your website works (other users will see a broken site whilst you are debugging it(.
2. The report-uri directive allows you to specify an endpoint to which the browser will send violation reports. The report-uri directive can be used in tandem with the Report-Only header which means that the browser will not actually enforce the policy; it will just report on the violations. It should not come as a surprise that Scott Helme's report-uri.com also hosts a reporting endpoint (he did well getting that domain name).

## Why use a Content Security Policy?
If your website only serves static HTML and uses no external elements then a CSP is unlikely to add much to your site. That being said it will also be easy to implement using the 'default self' rule!

However if your site uses external scripts over which you have no control then you should be using a CSP; or if your site allows users to enter information that is then displayed (comments, reviews, etc) you should also be utilising a CSP as an extra layer of defence against persistent XSS (cross-site scripting). If a user carefully crafts a comment to contain a piece of javascript and that comment is rendered back into the page a strongly controlled CSP will prevent the code from running (google 'CSP nonce' and 'CSP hash' for ways of dealing with inline javascript).

A well crafted and strict Content Security Policy, used in tandem with other best practices, will significantly reduce the risk of cross-site scripting (XSS) attacks.

## Using a meta tag
I mentioned at the top of this post that a CSP can also be a TAG; not everyone has the ability to edit their browser headers. On shared hosting platforms, you are rarely given the ability to directly control the web server; some platforms such as GhostPro do not allow you any control over the server side configuration. The use of an HTML meta tag can help you to implement a CSP without having to set the actual browser header. The CSP "code" is the same as that for a browser header; the only limitation is that you can not use the report-uri feature to send failure reports. You can, however, look at report-uri.com's JS which will perform the failure reporting for you!

## Summary
In summary, if you run a website which presents dynamic content (be it a large corporate system, or a simple blogging/commenting platform) then you should also be using a Content Security Policy. It should be restrictive and ensure only expected and authorised hosts can be referenced in by your site. You should also make use of the report-uri functions (either self-hosted or using [Scott Helem's](https://scotthelme.co.uk/) [report-uri.com](https://report-uri.com)) to ensure that you do not cause errors on your website.