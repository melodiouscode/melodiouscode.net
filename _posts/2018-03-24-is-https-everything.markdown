---
layout: post
title: Is HTTPS everything?
featured: true
date: '2018-03-24 09:51:43'
image: /images/posts/giulio-magnifico-78819-unsplash_resized_d4193c042c9e68a4f766f020242d46d3.jpg
tags:
- security
- https
- https-series
---

>This post is part of a [series on HTTPS and browser security](https://melodiouscode.net/tag/https-series/); it is partly to spread knowledge, but mostly to allow me to learn more about the subject by putting it 'down on paper'! Enjoy, and please comment, correct, and discuss.

If you are involved in designing, developing, testing, publishing, or managing a website then you have likely already heard about HTTPS. HTTPS has been discussed from start to finish several times in recent years; by some notable people ([Troy Hunt](https://www.troyhunt.com/about/), [Scott Helme](https://scotthelme.co.uk/), etc) and some less notable people ([Don't Take Security Advice from SEO Experts or Psychics](https://www.troyhunt.com/dont-take-security-advice-from-seo-experts-or-psychics-neil-patel/)). In the past the subject of website security was generally restricted to the purchasing of an SSL Certificate, that has changed! This series of blog posts is aimed at demystifying website security and expanding both my and your knowledge of both HTTPS and it's supporting protocols.

## Part 1: What is HTTPS?
### Background
>**Protocol** (computing) *noun*: 'a set of rules governing the exchange or transmission of data between devices.'
>
The internet runs over a protocol called the *Hypertext transfer protocol* (or HTTP for short). The *Hypertext transfer protocol* was originally created by the internet giant [Sir Tim Berners-Lee](https://en.wikipedia.org/wiki/Tim_Berners-Lee) at CERN in 1989; it allows the transfer of hypertext (HTML to you and me) over a distributed network of machines (the internet).

HTTP served us well for many years (and continues to do so), but it needed something more. The secure version of the protocol was born with the simple addition of the letter S; HTTPS. Even the most ill-informed of surfers know that the green padlock (or is it a handbag) means that their connection is secure (sort of, more on that later in the series); the HTTPS protocol is what gives us that padlock.

### How does HTTPS work?
At it's most basic HTTPS works by verifying the remote web server is who it claims to be. This is achieved by the use of a digital certificate that states they are who they say they are; think of it like a passport for a website. Taking that passport metaphor a step further; when someone shows you their British passport you know they are who they claim to be. Why, because Her Britannic Majesty’s Government has stated so, and you trust them right? 

![chain-of-trust](/images/content/chain-of-trust.png)

This 'chain of trust' for a passport applies directly to the 'certificate chain' used by HTTPS. When you purchased your computer/mobile/etc you indicated that you trusted the people who wrote it's software; a company like Microsoft, Google, or Apple. Installed on your device are a set of certificates known as *root certificates*, companies like Microsoft install these certificates because they have explicit trust in their owners (companies like Comodo, Go Daddy, and DigiCert). Not all *root certificates* are managed by the operating system; your chosen web browser also bundles some certificates and can choose to trust or distrust them itself (more on that later in the series).

Those *root certificates* are owned by companies known as *root certification authorities* or root CAs for short. They choose to sell certificates onto the people who create websites; or in some cases, they delegate that trust onto other firms who act as resellers (this has been known to go a bit wrong sometimes, search for [Trustico revoke](https://www.google.co.uk/search?q=trustico+revoke) if you want to know more!). So when you see an 'HTTPS Certificate' on this website you can trust I am who I claim to be because another firm that is trusted by the software maker you trust has said so! A chain of people, a chain of trust; simple.

### Is that it?
The certificate by itself does not make the connection secure; a transfer protocol that is known as [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) (previously SSL, which is an older now less secure encryption protocol) provides the security. When you access a secure website (over https) your browser sends some information to the web server stating which secure protocols it can support. The server then picks one and a key exchange takes place (known as a handshake); this creates a secure tunnel between your browser and the remote server. From then onwards the communication is secure. How this works is a bit in-depth for this simple article, so check back later in the series for a more detailed explanation of how it works (and the dangers when it doesn't).

### Want to know more?
Subscribe to my RSS feed and keep an eye out for future articles in the series; or if you cant wait, check out the [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) and [HTTPS](https://en.wikipedia.org/wiki/HTTPS) pages on Wikipedia.

#### The header image for this post came from [Giulio Magnifico](https://unsplash.com/@giuliomagnifico?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) via [unsplash.com](https://unsplash.com).