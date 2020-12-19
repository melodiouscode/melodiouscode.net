---
layout: post
title: Disqus and Cloudflare
date: '2018-04-05 18:51:56'
image: /images/posts/nasa-63029-unsplash-min.jpg
tags:
- cloudflare
---

The comments section of this site uses the third party Disqus system; it looks after the storage, moderation, management, and spam filtering of comments for me. The entire website is run through the Cloudflare system; providing the SSL Certificate, web application firewall, caching layer, edge node scripts, etc. Unfortunately, by default, these two systems do not play well together.
![rocketloader-min](/images/pages/rocketloader-min.png)

Rocket loader is one of Cloudflare's performance improvements; it decreases the window load time by optimizing any javascript contained within the page (bundling and reducing the number of external calls in the page load). Unfortunately, when Rocket Loader does its magic on the script used to load Disqus it breaks the script. The quick solution is to disable Rocket Loader on any site that uses Disqus, but there is another option.

When Cloudflare encounters a script tag containing the attribute 'data-cfasync="false"' it skips optimizing them. Place this into the Disqus loader on your site and you will find that Cloudflare and disqus start to play together well.
![script-min](/images/content/script-min.png)

### Thank you to [NASA](https://unsplash.com/@nasa) for providing the header image for this post on [unsplash.com](https://unsplash.com).