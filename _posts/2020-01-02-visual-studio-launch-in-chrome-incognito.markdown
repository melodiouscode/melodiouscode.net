---
layout: post
title: 'Visual Studio: Launch in Chrome Incognito'
date: '2020-01-02 13:36:33'
image: /images/posts/braydon-anderson-wOHH-NUTvVc-unsplash-min.jpg
tags:
- debug
- developer
- visual-studio
- browser
---

By default Visual Studio creates an entry for each recognised web browser you have installed when you first launch the IDE. We all know that we should be testing our web applications in more than just our favorite browser (after all, our end users may be using any number of browsers).

Visual Studio supports the addition of other browsers; and using this feature you can add other browser modes such as incognito. Why I hear you ask; incognito mode is not just for naughty browsing habits. It also containerised your cookies, and history; so if you are debugging an application that uses an external authentication provider you won't inherit your existing sessions from other applications (my use case).

### How to add Chrome Incognito Mode to Visual Studio's Debug Button

1. Open the 'browse with' window from your menu bar (whilst a web application project is open). Strangely this requires your application to build before it will open!
<figure class="kg-card kg-image-card"><img src="/images/content/more-emulators-1.PNG" class="kg-image" alt="The 'browse with' menu option"></figure>

2. Click Add and enter the following values:

Program: C:\Program Files (x86)\Google\Chrome\Application\chrome.exe  
Arguments: --incognito  
Friendly Name: Chrome Incognito

Click OK.

3. If you want this to be your default, select the new list entry and click "set as default".

Now you can debug your web application as if you were a first time browser every time!

<!--kg-card-begin: html--><small>Thank you to <a href="https://unsplash.com/@braydona?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText" target="_blank" title="Unsplash">Braydon Anderson</a> for providing the image used in this post's header for free on <a href="https://unsplash.com" target="_blank" title="Unsplash.com">Unsplash.com</a>.</small><!--kg-card-end: html-->