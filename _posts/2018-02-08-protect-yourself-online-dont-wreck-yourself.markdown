---
layout: post
title: Protect yourself online, don’t wreck yourself
image: /images/posts/hacker-2883635_640.jpg
date: '2018-02-08 09:48:00'
---

I have been watching a lot of the TV show [Criminal Minds](http://www.cbs.com/shows/criminal_minds/) recently (blame my wife); in the show there is a technical wizard known as Penelope. She is the teams super hacker and data manipulation extraordinaire.  In some of the episodes Garcia (her surname, it’s an American show they all call each other by their surnames because its more dramatic) delves deep into an unsub’s (Unknown Subject, the bad guy serial killer crazy person they are trying to catch) digital life and comes up with all the answers

Very little effort seems to be put in to the hacking, she just gets into their social media accounts, or their emails and finds out the address of their secret death dungeon thanks to an invoice from the power company stored under “Super Secret Death Documents” in their gmail folders. This got me thinking (the security bit, not the super-secret-death-dungeon bit) about how easy some forms of “hacking” are, and how you can protect yourself online.

It isn’t hard to work out the basics about a person these days; there is so much Open Source Intelligence (OSINT) available to the casual social engineer (for more information about OSINT and Social Engineering check out one of Troy Hunt’s courses on [Plural Sight](https://app.pluralsight.com/courses/ethical-hacking-social-engineering) or his [blog](https://www.troyhunt.com/its-time-that-you-vulnerable-human/)). Facebook, LinkedIn, and twitter are generally a good starting point to find out all sorts of information about your “target”.

Last time you signed up for an email account (or similar) do you remember those questions about your first pet, or your mothers maiden name? Those tiny bits of knowledge can be used to reset the password to your email account; once you are in there (as Garcia was) you can access almost everything a person has online (resetting passwords via their inbox as you go). From my generation on-wards (and more so for younger generations) you will almost certainly find someones mother on their Facebook wall (liking everything they post as mine does), and then from their profile you may find their maiden name (or even their parents posting on their wall!). How many people list their dog on Facebook, posts about how nice it looks in its Christmas jumper, that’s another tick box covered!

One source of data that I haven’t seen Criminal Minds use yet is the data breach; why bother hacking someones account when the password they use for everything is in a leaked data-set? Surely Garcia must have them all downloaded so she can search for the unsub’s passwords? Coincidentally if you haven’t already go and check out [haveibeenpwned](https://haveibeenpwned.com/) and see if you have been breached (I bet you have). There seems to be a new data breach every few days so if you haven’t been “pwned” yet you will be!

## Protect yourself, don’t wreck yourself!
So what can you do to protect yourself online and your accounts against Garcia (or some script kiddo from a far flung country)? Well there are a few things, some simple, some more complex (but still worth doing).

### Stop using the same password
No seriously stop, just stop using the same passwords everywhere. All it takes is for that basic little website about how [much you like cats](http://www.catforum.com/) to get breached (rather likely considering they run as a vBulletin forum) and your password for Gmail/your bank/your government login/etc to be leaked (along with your email address as you used that to sign in). But “how can I remember hundreds of passwords” I hear you scream, simple just don’t!

### Use a password manager
In the past I would not have recommended a password manager; giving someone else all your passwords seemed like crazy talk. However that was before all the breaches started; companies were not storing user passwords securely so each breach leaked credentials (often in plain text). Remembering a unique and secure password for each system you use is unlikely to work; however learning one long, complex, and strong password is easy, using that password to secure a highly encrypted vault is even easier!
![haveibeenpwned](/images/content/haveibeenpwned.png)

There are many password managers out there, depending on your preference (offline or online) I suggest looking at [KeePass](https://keepass.info/) or [1password](https://1password.com/). Which ever password manager you choose please do you research first; I am not saying that the smaller firms are not trust worthy but the larger and more public a firm the more likely it is to be secure (password managers get a lot of attention from white and black hats alike) due to the coverage it receives.

### Look into Multi-Factor Authentication
Google [recently stated](https://www.theregister.co.uk/2018/01/17/no_one_uses_two_factor_authentication/) that over 90% of Gmail users still don’t use two factor authentication (also known as Multi-Factor) to secure their accounts. Two Factor Authentication (2FA) is just what it sounds like; your password is the first factor, a single use code (from a mobile device for example) acts as the second. Services which offer 2FA provide an enrolment code which an app on your mobile device can understand; allowing it to display random codes over time which the server can validate.

When you log in you have to provide both your password and the 2FA code; this means that if someone obtains your password (from a breach for example) they can not log into your account without having access to your 2FA device. It is a quick and simple way to improve your security substantially.

Some sites (such as twitter, amazon, and google) allow you to receive an SMS with the 2FA code; there is currently a debate around how secure the use of mobile for 2FA is. However it is important to note that any form of 2FA is more secure than no form; so unless you are securing your massive crypto-currency reserves (we all have those right?) mobile 2FA will be fine for now!

### Turn on Alerts
A well written system will allow a user to review audit logs; or obtain alerts of unusual activity (think about how your bank informs you of strange activity). Check out the security settings on the websites you use; many will likely allow you to receive an alert for login from new devices.

On top of these active alerts; don’t forget to subscribe to a service such as [HaveIBeenPwned](https://haveibeenpwned.com/) which does it’s best to inform you if and when your email accounts (or even entire domains if you own them) appear in data breaches online.

##tldr; How do you protect yourself online?
This post has grown longer than I intended it to; so here are a few quick action points you can use to protect yourself online:

1. Stop using the same passwords on different services; invest in a password manager such as [KeePass](https://keepass.info/) or [1password](https://1password.com/).
2. Enable 2FA/MFA protections on as many accounts as you can; check out [twofactorauth.org](https://twofactorauth.org/) for a list (and instructions) of many sites which support it.
3. Review security settings on the sites you use; enable alerts and check logs.
4. Sign up to [HaveIBeenPwned](https://haveibeenpwned.com/).