---
layout: post
title: Password Management
date: '2017-08-05 09:19:00'
image: /images/posts/photo-1504203700686-f21e703e5f1c.jpg
tags:
- passwords
- security
---

In the years since I first sat in front of a computer the importance of a strong secure password has gone from a minor annoyance to a mission critical requirement. Now in the age of data breaches and the internet of things, the need for good password management is something that should be taught in school!

## Back to School
Cast your mind back to the early 90s; bleach blonde hair, a new friends episode every Thursday and big grey computers that only the nerds played with. The first computer I remember using was a simple grey box in a corner on the top floor of my primary school; there was no login screen, but considering it was only used to run educational programs and was completely air gaped it didn’t really need any security. The early internet as we know it had only just started to exist; [Sir Tim Berners-Lee](https://en.wikipedia.org/wiki/Tim_Berners-Lee) had published [WorldWideWeb](https://en.wikipedia.org/wiki/WorldWideWeb) (his first web browser) just a year or two before!

Soon came email accounts, forums, online banking and everything else. Passwords were just that, words used to pass through security. People generally had one and used it for everything, you felt oddly superior if it was a geeky word or a password you stole from a hacking movie (hack the gibson anyone?).

In the early 2000s what we now call data breaches started, old systems easily hacked by more modern systems. Everything was networked but not everyone knew how to do it securely. Hackers took swathes of user accounts with un-encrypted (or poorly hashed) passwords and shared them online; the size of these breaches grew and grew.

I could write a history of data breaches and bore you all half to death, I doubt anyone would read much further. If you do want a nice long list of breaches take a look at this [Wikipedia article](https://en.wikipedia.org/wiki/Data_breach).

What I will write about is the importance of good password, personal security and password hygiene.

## Passwords are like pants
There is a poster on the wall of my office that reads “Passwords are like underpants. Change them often, keep them private and never share them with anyone”; some bright spark has even added a note that says “password sniffing is a thing too”! It may sound like a joke but the poster isn’t wrong; changing your passwords once in a while is a simple way to protect yourself against the hacks (although it is not enough, something I will cover shortly).

You could come up with the most secure looking password in the world, and even remember it: asdfn03rAsdf$22@A}A4n2d. No one is going to remember that when they see you typing it in; and the chance of someone guessing it is slim to none. Sorted? I think not; it only takes one badly designed website (and trust me there are many) to leak its database with a plain text password field and you are done for. As soon as you find out you can change your password and re-learn it (and update it’s use everywhere); but finding out is the hard part.

Now is the moment to mention a fantastic service provided by Troy Hunt called [HaveIBeenPwned](https://haveibeenpwned.com/)? You can use his website to search for your email address (or username) in a large number of data breaches so see if your passwords have been “pwned” (released to the public). There is even a notification service that will inform you if you appear in a future breach (a sensible precaution to take).

## How can I protect myself?
The crazy strong password from earlier would be nearly impossible to remember and as we have seen doesn’t offer us much in the way of security. The solution is to use a different crazy password for each and every website; but how on earth would you remember them all? After all some of us have 100+ accounts to remember!

In comes a password manager; a simple application that keeps track of your credentials for you good ones even have password generators inside which will take care of creating your complex password. There are many people that would tell you a password manager is a bad idea (I used to be one of them); after all putting all your passwords (or eggs) in one basket and letting someone else hold on it it seems crazy. Our friend Troy Hunt has written a great article on why [password managers do not have to be perfect](https://www.troyhunt.com/password-managers-dont-have-to-be-perfect-they-just-have-to-be-better-than-not-having-one/) so I wont go into to much detail on the subject. Suffice to say a well controlled password manager will deal with 99.99% of your password problems; if you use a different password on each website then a breach will only affect that site!

## But which password manager?
Personally I use a system called KeePass; it is open source (so multiple people have verified it is safe and not evil) and free to use. The one requirement I had for a password manager was that it be under my control; I was not interested in giving my passwords to some service which could be breached. [KeePass](http://keepass.info/) creates an encrypted container which is secured using two of the best methods available (AES and TwoFish); as long as you have the container and know the passphrase (just one to remember now!) you can access all your passwords. There are options to use further keys such as an external token or even GPS coordinates (not really that useful!). I store my container in a place I can access it from anywhere (a secure place); that way I can use an app on my phone, desktop, chrome book, work laptop etc to get a hold of my passwords when ever I need them.

So should you use a password manager? If you feel secure in using one (and can cope with the change it entails) then yes, the more random and complex all your passwords are the better chance you have of surviving online.

I highly recommend that you read a few articles on subject of passwords and their management:

- [Password managers don’t have to be perfect](https://www.troyhunt.com/password-managers-dont-have-to-be-perfect-they-just-have-to-be-better-than-not-having-one/) by Troy Hunt
- [Passwords evolved](https://www.troyhunt.com/passwords-evolved-authentication-guidance-for-the-modern-era/) also by Troy Hunt
- [KeePass](http://keepass.info/) by KeePass!
- [HaveIBeenPwned?](https://haveibeenpwned.com/)