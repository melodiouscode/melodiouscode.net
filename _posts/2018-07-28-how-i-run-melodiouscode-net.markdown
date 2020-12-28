---
layout: post
title: How I run melodiouscode.net
date: '2018-07-28 14:53:15'
image: /images/posts/vadim-sherbakov-36-unsplash-min.jpg
tags:
- development
---

Partly for myself and partly for any interested readers I wanted to note down how melodiouscode.net works; what technologies and providers are used and for what purpose. This is not going to be a deep technical article but more of an overview and the basis for some more technical articles in the future.

Although this is a just a simple blog (for now anyway!) I have been using it to learn more about the systems that are out there to support and secure a larger website. Much of the work I have done is overkill for a small blog but I couldn't talk about security if I wasn't secure myself!

There are a number of components to melodiouscode.net the larger of which are listed here.
<!--more-->
## Componants

- The Ghost Blog engine
- Digital Ocean
- Cloudflare
- Cloudflare Workers
- Report URI
- Zapier
- Unsplash
- Grammarly

# The Ghost Blog Engine

Previous blog sites that I have run over the years have used the WordPress engine which has unfortunately become rife with questionable plugins and vulnerabilities, some of which have been rather nasty. On top of that, it requires so much maintenance and configuration that I never got around to writing any articles, instead spending my time upgrading, backing up, and tweaking appearances.

Shortly before I started up this new blog site (melodiouscode) I watched a talk called "[Hack your Career](https://www.youtube.com/watch?v=-MUhcgXBj_A)" &nbsp;by [Troy Hunt](https://troyhunt.com); in it, Troy recommends the Ghost Pro platform for anyone tempted to set up a semi-professional blog. I decided to take one step back from the Ghost Pro hosted offering and take a look at the Ghost Blog engine which is released as open source under the MIT licence.

Ghost is a simple and clean blogging engine aimed at writing articles, not creating some all singing all dancing website with integrations up the wazoo. Hopefully using a simple engine to run my blog will mean I write a few more articles!

# Digital Ocean

[Digital Ocean](https://m.do.co/c/8879a9740772) provides what they call droplets for you to run web-based systems on; at the basic end, they cost just $5 a month (the droplet I am running this site on is a $5 droplet). Droplets are effectively just virtual servers with a public IP address; Digital Ocean provides DNS features allowing you to map your domain name to their platform.  
Although using Digital Ocean does require me to update the software/operating-system on my droplet semi-regularly, this is easily automated (I use an Ubuntu Droplet so can set a cron job to run apt). They also have a quick one-click setup for Ghost allowing you to create a droplet pre-configured to use Ghost and LetsEncrypt.

You can help me out with my hosting costs by following this [referral link](https://m.do.co/c/8879a9740772) when checking out [Digital Ocean](https://m.do.co/c/8879a9740772).

# Cloudflare

This is where the fun begins, [Cloudflare](https://cloudflare.com)provides a number of services (many for free): enhanced security, caching, DDOS protection, application firewalls, and much more. All of this is available in a basic sense using their free website plan but for the purposes of learning and playing, I have chosen to use one of the paid plans as it grants access to some more features.  
Through Cloudflare, I am able to provide a secure connection to my site with little configuration, including HSTS Pre Loading, automatic HTTPS rewrites, and TLS 1.3. Along with the security enhancements they also provide an aggressive caching layer which keeps the site fast and removes the load from my origin Digital Ocean server.

# Cloudflare Workers

Along with the security and caching layers Cloudflare also provide a service called "Cloudflare Workers"; this allows me to run custom code on the edge of the Cloudflare estate moments before the webpage is sent to the client's browser. Following the advice of [Scott Helme](https://scotthelme.co.uk) I have taken his [Security Headers Cloudflare Worker](https://scotthelme.co.uk/security-headers-cloudflare-worker/) and modified it a little to serve my [CSP](https://melodiouscode.net/content-security-policy/)and other security headers without the need to modify my web server or Ghost installation.

# ReportURI

Created by Scott Helme, [ReportURI](https://report-uri.com)is a service which receives [CSP](https://melodiouscode.net/content-security-policy/)/etc reports when a site breaches the policy set in its security headers. Such as when an unexpected javascript resource is included in the page, or an iframe is injected into the view. Without a service like ReportURI I would not be able to tell if the [CSP](https://melodiouscode.net/content-security-policy/)I have set is functioning correctly; and ReportURI has a free basic tier which is more than enough to run a personal blog! If you intend to implement a CSP there is no reason not to pick up the free account on [ReportURI](https://report-uri.com), if you run a larger business site you should definitely look at their paid-for offerings.

# Zapier

Much like the service [IFTTT](https://ifttt.com/), [Zapier](https://zapier.com/)allows you to create simple logic flows to automate processes. I use it simply to tweet a link to a new article after I have posted it. I could do this myself, but why not have something do it for me! [Zapier](https://zapier.com/)is also free for basic "zaps" and ties in directly with Ghost.

# Unsplash

[Unsplash.com](https://unsplash.com) is a fantastic resource of high-quality royalty free images which you can use for any purpose. I use images from Unsplash for all the header pictures for each post and page on this site; you do not have to provide attribution when you use an unsplash image but it is good karma if you do (see the bottom of this post for an example).

# Grammarly

Write good, I often do not! [Grammarly](https://grammarly.com)is a program that provides spell checking, grammar reviewing, and sentence structure suggestions. The Grammarly system is slowly helping me to write better content. Improving upon my typically lax language and sentence structure.

# In Summary

Melodiouscode.net is made up of several parts, the basics of which are outlined above and will at some point form the parts of a more detailed write-up!

<!--kg-card-begin: html--><small>The header image for this post was provided for free on <a href="https://unsplash.com">unsplash.com</a> by <a href="https://unsplash.com/@madebyvadim">Vadim Sherbakov</a>. Thanks Vadim!</small><!--kg-card-end: html-->