---
layout: post
title: HTTPS is just the tip of the sword
featured: true
date: '2018-03-30 19:03:19'
image: /images/posts/alex-martinez-62348-unsplash_resized.jpg
tags:
- security
- https
- https-series
---

>This post is part of a [series on HTTPS and browser security](https://melodiouscode.net/tag/https-series/); it is partly to spread knowledge, but mostly to allow me to learn more about the subject by putting it 'down on paper'! Enjoy, and please comment, correct, and discuss.

In the previous post in this series I wrote about the basics of HTTPS; what certificates are and how the chain of trust works. The use of an HTTP certificate isn't a magic pill that makes everything secure, there are several other security techniques which you should investigate. Not every website will require all of these protections, but in general, they are worth considering.

* [Strict Transport Security](https://melodiouscode.net/https-is-just-the-tip-of-the-sword/)
* [Content Security Policy](https://melodiouscode.net/content-security-policy/)
* X-Frame Options
* Anti XSS Protection
* X-Content Type Options
* Referrer Policy

The articles in this series will focus largely on the above browser security headers; each article will take an individual header and look into it in more detail.

After discussing HTTPS Certificates the sensible next step is to review *Strict Transport Security* and it's options. So what is HTTP Strict Transport Security, or HSTS for short?

## The Basics of HSTS
Communication with an HTTPS-enabled website is secure; the handshakes between the server and client ensure that data between them is encrypted in transit and can not be interfered with by another party. However, this only applies once the secure connection has been made; if a user directly accesses the non-secure (HTTP) address then the connection is at risk.

This insecure connection can happen if a user types in the address directly (or opens it from a bookmark, etc). For example, if a user were to type *somedomain.com* direct into the browser it would attempt to access *http://somedomain.com*. If *somedomain.com* supports HTTPS and they have done a good job of it then the user will be redirected to the secure side of the domain (HTTPS); in here the problem lies!

The short moment that the user is traversing from their browser to HTTP, and on to HTTPS is a risk. Imagine that somedomain.com is actually yourbank.com. Suddenly the potential gain from hijacking that connection has jumped; step into the connection before it is secured and you could steal the user's password and gain entry to their bank account. All the while passing back the real website over the HTTP connection they hijacked. This is called a *Man in the Middle Attack* or MITM Attack for short. To achieve a MITM Attack you do need to have exploited some part of the connection, but this has been shown to be rather easy on free wifi in coffee shops and the like (see [this article about the wifi-pineapple](https://www.troyhunt.com/the-beginners-guide-to-breaking-website/)).

How can we protect against this? HSTS is the first weapon in our anti MITM arsenal. By sending an HSTS Header a web-server can state that from that moment onwards it should only be connected to via HTTPS (for a configurable duration); gone is the chance for a MITM attack as the browser will now try and create a secure connection from the start (and alert when it fails to do so).

There is one small problem left; HSTS requires that the end user makes a single connection first (which might be over an insecure connection). This still presents a risk to future communication; all it takes is for the attacker to inject a malicious payload into the page to high-jack the users browser (and control future connections); I make it sound a bit simple there but it is possible!

## HSTS Pre-Load
The HSTS Pre-Load system has already ridden to our rescue. If you are using a modern browser (which has connected to the internet in recent months) it will be impossible for you to connect to melodiouscode.net in an insecure manner; even if you type in the URL with HTTP. This is thanks to the HSTS Pre-Load header.

The HSTS Pre-load list ([https://hstspreload.org/](https://hstspreload.org/)) is managed by the Chromium project (related to Google Chrome). Website owners can submit themselves to the list for pre-loading into browsers. Once pre-loaded a browser (or User Agent to give it the proper term) will only ever connect to a site using HTTPS, this closes the door to the MITM attacks I mentioned earlier.

There are several hoops to jump through to become HSTS Pre-loaded, and it isn't for the faint-hearted. If you become pre-loaded and then stop serving a valid HTTPS certificate for any reason, then your website may become inaccessible to everyone until their User Agent (UA) is updated to remove your site (which could take a very long time).

## How do you enable HSTS?
HSTS is simple to enable, and you don't have to pre-load. You can just indicate you wish a UA to use HTTPS for visits it makes over a period of time.

<pre><code datalang="c">Strict-Transport-Security: max-age=60</code></pre>
The above snippet is the HSTS header; it can be set in most web-server environments. It indicates that the server wishes to be communicated with securely for the next 60 seconds! Not overly useful; but you get the idea. You can set it for any period of time you wish: 10 minutes, a day, a week, the next six months, it is up to you.

<pre><code datalang="c">Strict-Transport-Security: max-age=60; includeSubDomains</code></pre>
The *includeSubDomains* flag instructs the browser to talk securely with any subdomain of your site (such as blog.mysits.com or shopping-cart.mysite.com).

<pre><code datalang="c">Strict-Transport-Security: max-age=600; includeSubDomains; preload</code></pre>
The *preload* flag indicates that the site wishes to be included in the HSTS Pre-load list. **REMEMBER** this can be dangerous if you don't always serve a valid HTTPS certificate; use with caution. In effect preloading is a one-time thing; once you are on the list that is it, being removed is not quick or easy and requires you to contact the chromium group manually.

## How do I pre-load?
To be pre-loaded you must ensure your website puts forward the HSTS header in a particular way and serves a few other instructions:
1. You must have a valid HTTPS certificate for the domain, and all sub-domains you wish to use (all of them, not just ones you wish to protect with HSTS).
2. All HTTP traffic must be automaticity redirected to HTTPS.
3. All subdomains, especially the www subdomain, must be served over HTTPS.
4. The HSTS header must be served with a max age of at least one year, include subdomains, and the preload flag.

When you have covered all of the above visit the pre-load project and submit your site for inclusion at [https://hstspreload.org/](https://hstspreload.org/). Remember, it is a one-way street.

### Want to know more?
Subscribe to my RSS feed and keep an eye out for future articles in the series, or if you can't wait to check out one of these:
* [Is HTTPS Everything?](https://melodiouscode.net/is-https-everything/) @ melodiouscode.net
* [HSTS on Wikipedia](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) @ wikipedia.org
* [The OWASP Cheat Sheet](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) @ owasp.org

## The Series
1. [Is HTTPS Everything?](https://melodiouscode.net/is-https-everything/)
2. [HTTPS is just the tip of the sword](https://melodiouscode.net/https-is-just-the-tip-of-the-sword)

#### The header image for this post comes from [Alex Martinex](https://unsplash.com/@estudisimple?utm_source=melodiouscode.net) via [unsplash.com](https://unsplash.com), cheers Alex!