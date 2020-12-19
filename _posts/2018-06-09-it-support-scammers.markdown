---
layout: post
title: IT Support Scammers
date: '2018-06-09 06:42:14'
image: /images/posts/rawpixel-653764-unsplash-min.jpg
tags:
- security
- learn
---

No matter how strong your technical security is ([antivirus](https://en.wikipedia.org/wiki/Antivirus_software), [firewalls](https://en.wikipedia.org/wiki/Firewall_(computing)), security headers, well-written applications, etc) there is always one sure route to failure, [social engineering](https://en.wikipedia.org/wiki/Social_engineering_(security)). If a privileged user can be convinced to perform nefarious acts on a system that system is compromised. That being said most professionals are not going to fall for that (although I know one who did fall for a variant the old Nigerian finance scam to the tune of several thousand pounds); the less initiated are a different story and we as IT professionals have a duty to help them!

IT Support scams appear to be on the rise again; I am aware of at least ten people who have received calls claiming to be from Microsoft in the last year. Luckily for them (and me) most of them realised what was going on before it was too late, some were less savvy and their machines required a lot of my time.

## What is a support scam?

IT support scams almost always start off with an unsolicited phone call. The scammers have either acquired the victim's number on the black market (data breaches, stolen files, etc) or they are just simply dialling every number one at a time (read about [auto-dialers here](https://en.wikipedia.org/wiki/Auto_dialer)).

Once a scammer gets ahold of their intended victim they claim to be from a trustworthy firm, typically Microsoft (or Apple, Google, etc). The scammer uses the victim's trust in a well-known firm to build a conversation and start engineering their way into the victim's system.

How many of the uninitiated (think your grandparents or that little old lady who is a friend of your mothers) understand half of the notifications their laptop shows them? The scammer preys on this; telling them that "Microsoft has detected some problems with your machine", asking them if they spotted that "update alert" the other day. The odds are that windows update has popped up an alert (or perhaps some anti-virus software has) in the last week and the user has ignored it. The scammer will walk the victim through some screens on their machine claiming that common files are viruses or getting them to look at the system event log to see all the "critical system errors" it shows (we know that badly written applications like to error, your grandparents do not).

Eventually, when the scammer has convinced the victim that they are at risk they encourage them to install some remote access software, sometimes a custom remote access trojan (RAT)) other times just something simple like [TeamViewer](https://www.teamviewer.com/en/). With remote access the scammer can do as they please, stealing documents, leaving malicious payloads ([ransomware](https://en.wikipedia.org/wiki/Ransomware), [keyloggers](https://en.wikipedia.org/wiki/Keystroke_logging), etc), once they become embedded they often ask the victim to hand over their credit card details to pay for "a cleaning service" which they have no intention of providing.

## How can we stop the spread?
Simply put making the vulnerable users security as simple to understand as possible is the first step; if they know they are secure because someone they trust told them so (hopefully they trust you) and showed them how to know they are secure then they are less likely to be scared into acting by a scammer. Most importantly tell them about these scams, make sure they understand that anyone who calls them about their computer is almost certainly lying if they have any doubt they should hang up and call you for assistance!

### Make sure they have antivirus and firewall
For most standard users the built-in Windows 10 security software is more than enough, especially from a firewall perspective. If you want to go one step further and install one of the many free antivirus programs be careful which one you pick. All the freemium products try and force their paid for products on you with every update, our potential victims are just going to click past the update messages because they mention spending money. Pick an antivirus program which is not just free as a hook for the paid software; [Sophos](https://www.sophos.com) provide a good product which is less needy (thanks to their top line coming from corporate subscriptions and not one-off payments). Depending on who the user is (friend or family) you may be willing to install the good stuff, add them to your personal subscription (I use [ESET Nod](https://www.eset.com/uk/home/multi-device-security/) for security and it costs all of $5 a year to add another user) that way they will never get nagged about converting to a paid subscription.

### Keep them up to date
Provide a simple way for them to keep all the little bits of software (Adobe, Java, etc) up to date. The more up to date their software the more secure they will be, free programs such as Adobe Software and Java are often filled with security holes, keeping them updated is especially important. I use a product called [Ninite Pro](https://ninite.com/pro) to silently push updates to family machines, for the machines that I do not want to spend money on (think friends rather than family) I place a copy of the [Ninite Updater](https://ninite.com/) on their desktop named "UPDATE" and tell them to run it once a week, this ensures all those little programs are kept up to date without the user having to understand what they are!

## Educate!
Explain how to be secure online, what to do and what not do to (don't forget the dangers of oversharing on social media!). Antivirus is useless if they don't understand the popups, show them what they look like and explain the jargon (write it down for them).

But most of all, tell them to contact you if they are concerned! It may seem like an invite for countless support calls but one or two calls a year which can be dealt with over the phone are better than a week of extracting malicious software from their laptop (and them being scammed out of a few hundred pounds).

## TLDR;
* Educate your friends and family about IT support scams so they don't fall victim!
* We need to work together on this!

<small>The header image on this post was provided for free by [@rawpixel](https://unsplash.com/@rawpixel) via [unsplash.com](https://unsplash.com). I chose it because it looks like us all fist bumping when we agree to work together on this!</small>