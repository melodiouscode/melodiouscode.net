---
layout: post
title: In the beginning there was 1.1.1.1
date: '2018-04-02 08:06:23'
image: /images/posts/maarten-van-den-heuvel-243707-unsplash-min.jpg
tags:
- internet
- cloudflare
- dns
- security
- privacy
---

>There is no place like 127.0.0.1
>**Dorothy (after she graduated from MIT)**

The old saying "there is no place like home" is often translated to "there is no place like 127.0.0.1" by us geeks. 127.0.0.1 is what is known as the "loopback address", every single computer device uses that IP address to reference its self. In effect 127.0.0.1 means home to the computer. Yesterday (yes April Fools Day, it was not a joke), [cloudflare](https://cloudflare.com) released a new DNS Resolver service by the name of [1.1.1.1](https://1.1.1.1) and it is exciting! 
![1111-1](/images/content/1111-1.png)
For those who do not know what DNS is, or how it works here is a quick and dirty breakdown.
## What is DNS and how does it work?
The internet is big and full of numbers; we call these IP Addresses which are a string of four sets of numbers (for now, but that will change in the future), at the time of writing the IP address behind melodiouscode.net is 104.25.29.109.

It is a lot easier to remember words than it is to remember numbers; that is why you type google.com rather than 216.58.208.174. This means that the internet needs a way to translate the words into the numbers; along comes DNS. The Domain Name System (DNS) is basically a giant phone book for the internet. Every name is in there (ignore the dark web for now) and its corresponding IP address is listed.

When you access a domain name (like google.com) your computer performs a "DNS Lookup" to resolve the name to an IP address. The "DNS Server" at the other end responds and tells your computer where to go.

If you want to read more about how DNS works check out the Wikipedia Page for the [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System).

## What is 1.1.1.1 and why is it amazing?
1.1.1.1 is the new "DNS Server" from [cloudflare](https://cloudflare.com); it does everything a DNS server is meant to do (be a secure and trustworthy phone-book).

Unfortunately, some DNS servers are not very trustworthy; some have been known to hijack sessions (directing you to the wrong website), others are known to record everything you do (track the websites you visit). Your Internet Service Provider (ISP) will provide you with a DNS address by default, my ISP (virgin media) hijack every invalid DNS record (when you make a typo or try to visit a site that does not exist) and serve you their own search results page. These typo-squatting DNS pages are often filled with tracking cookies, adverts, and sometimes malicious data.

The new "DNS Server" from Cloudflare is the complete opposite, they promise to never track you, and to delete their logs every day so that your browsing habits are kept private. That statement is easy to make, many providers have claimed that privacy is important to them, and many have lied. Cloudflare has promised that they will be audited once a year by KPMG who will release a report with their findings.

## How do I use 1.1.1.1?
I am not going to attempt to write a detailed set of instructions here, as one already exists. Just navigate to [https://1.1.1.1](https://1.1.1.1) and you will find Cloudflare's own explanation and instructions for using the 1.1.1.1 service. Enjoy!

## Why have they done it?
Oh, you're still here, cool. The DNS system is broken, it is not secure and can be tampered with. One of the larger tampering to hit the news recently occurred in Turkey. The government of Turkey blocked twitter at the root level of the countries internet system; the ISPs were forced to block the resolution of twitter.com to it's IP address in their "DNS Servers". The Turkish Government did this after some embarrassing videos about Government corruption were shared on Twitter; imagine what would happen in the UK if the government blocked twitter every time someone said that 'Theresa May stinks'!
![8888-min](/images/content/8888-min.jpg)
Some of the "geeks in the know" in Turkey resorted to spray painting 8.8.8.8 (Google's own DNS Server) onto walls in an attempt to help people bypass the block!

Cloudflare has designed it's new service from the ground up to be secure, private, and auditable. They have baked in two new technologies 'DNS over TLS' and 'DNS over HTTPS'; one of these will, in the end, form the backbone of future DNS, and 1.1.1.1 supports them both already (not that is future proofing). Cloudflare is also in a unique position to provide this system; considering they already provide access to a massive percentage of the web via their authoritative DNS provider they already know where everything is; making that phone book lookup lightning fast. Their server infrastructure is also worldwide (they opened a [new data centre](https://blog.cloudflare.com/tag/data-center/) every day during March 2018), so there is always a server near you.

### Why not just use Google's server?
True you can use Google's DNS Server (8.8.8.8, and 8.8.4.4); many people do not trust a company which makes its money on data to serve their DNS results. So a truly private (and openly audited) system like 1.1.1.1 (and 1.0.0.1) is a preferred alternative.

Also in a time when we are feeling about the about of data Facebook stores about us (and yes Google do the same) do we even want to think what the likes of [Virgin Media](https://www.virginmedia.com), [BT Internet](https://bt.com), [Sky Broadband](https://sky.com), and the like might be storing? The USA even made it legal for their ISPs to [sell the DNS data](https://arstechnica.com/information-technology/2017/03/how-isps-can-sell-your-web-history-and-how-to-stop-them/) about their customers! 

You can read more about Cloudflare's new service on their [blog](https://blog.cloudflare.com/announcing-1111/).

#### The header image for this post was taken by [Maarten van den Heuvel](https://unsplash.com/@mvdheuvel) and provided for free on [unsplash.com](https://unsplash.com). Thank you Maarten, it is a sad sign of the times when it is so hard to find a photo of a phone booth with a phone book still attached!