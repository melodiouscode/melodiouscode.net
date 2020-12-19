---
layout: post
title: Force refresh Microsoft Account Password in Windows 10
date: '2017-12-23 09:36:00'
image: /images/posts/photo-1515449634394-7f0f1d7d6543_166244a125d35adf00b773febca86df4.jpg
tags:
- passwords
- microsoft
---

Windows 10 allows you to sign-in using your Microsoft Account Password which can be great, especially if you use a lot of Microsoft’s products (think OneDrive, Azure, [Visual Studio](https://visualstudio.com/), and other developer tools). Less passwords to remember means that you can have stronger passwords overall (less things to remember makes remembering things easier, but that will be another post in the future).

The problem arises when you change your Microsoft Account Password on another device, or via the web (using the account manager pages); windows doesn’t refresh it’s cache unless you change the password locally. Nor does it seem to refresh on restart/etc. So you end up having to use the old password and the new password for what is basically the same account (very annoying if you use [password managers](https://melodiouscode.net/password-management/)).

## How to refresh your Microsoft Account Password
The quick and easy way to refresh your Microsoft Account Password is:

1. Log in as any user on the machine (even the one you want to refresh)
2. Search for command prompt (cmd)
3. Right click and “Open file Location”, this will open an explorer window and show you the shortcut to Command Prompt.
4. Right click on the Command Prompt shortcut whilst holding down the ALT key, and pick “Run as a different user”.
5. Enter the Microsoft Account (full email address) and new password that you wish to re-fresh.
6. Done!

![runas](/images/content/runas.png)
The use of the “Run as a different user” option appears to force windows to check with the Microsoft Account servers when you enter the password; this then refreshes the local password cache.