---
layout: post
title: Developer Tools List 2018
featured: true
date: '2018-04-07 11:40:11'
image: /images/posts/garage-hanging-mechanic-162553-min.jpg
tags:
- development
- developer
---

Ask any developer who has worked in the industry for more than a month 'what tools do you use?' and they will reply with a nice long list of apps, IDEs, plugins, and random tools. I have often found myself googling 'best dev tools' when I am stuck on a project, or just need a brain break; there are many blog posts out there listing program after program. This time I have decided I will create my own list; and see if any discussion occurs (please use the comments section to talk about these tools, or any you think should be on the list).

Some background first; I am a .NET developer who largely works in c#. I also do a lot of work in SQL Server, both as a A-DBA (the first A stands for accidental, there is a blog post in that somewhere!) and a SQL Developer. I have written a bit of everything in my journey from Junior Developer to Senior Application Developer; ranging from simple console apps to detailed WPF Applications, classic ASP all the way to ASP.NET MVC Web API, front end, back end, fire and forget apps that run every minute for years. The whole stack; so my list of tools is going to be more .NET centric, sorry not sorry!

## Disclaimer
Everything on this list is written by someone else; I have never received a gift/bribe/etc from any of these firms. Other than a few stickers and a t-shirt from JetBrains when I won a giveaway they were running! If it is a paid for application I have either use my own money, or managed to convince the boss to buy a licence for me at work.

# Generic Developer Tools
* **Windows 10** - I write for the Microsoft Stack, which until recently has meant developing on a windows machine. I know several people who still like Windows 7 more (and yes Windows XP was the best), but Windows 10 is my OS of choice.

# Utilities
* [**Notepad++**](https://notepad-plus-plus.org/) - A text editor (on Windows) does not get much simpler than notepad; Notepad++ takes that simplicity and adds a lot of useful features without removing from the it's simple origins. Syntax Highlighting, RegEx based find and replace (in file and in folders), XML formatting, and much more. **FREE!**
* [**f.lux**](https://justgetflux.com/) - Hands up if you work stupid hours? We all know that looking at a screen for hours on end can cause eye-strain and headaches (I already suffer from a nasty headache condition, so why make it worse); f.lux is a free tool which slowly changes the colour and hue of your monitors as the day progresses based on your location. **FREE!**
* [**Fiddler**](https://www.telerik.com/fiddler) - Fiddler from Telerik is a free web debugging tool. It allows you to monitor, intercept, edit, and replay web traffic on your machine. It is great for watching traffic between your application and a remote service; or editing a request slightly before replaying it to see what changes. Very helpful when trying to debug a service you have no control over. **FREE!**
* [**Remote Desktop Connection Manager**](https://www.microsoft.com/en-gb/download/details.aspx?id=44989) - Written by the developers at Microsoft (rather than as a production product), RDC Manager allows you to keep a record of all the remote machines you access via the Remote Desktop Protocol. You can split connections up by groups and folders (think companies, production, staging, development, etc); the tool will securely remember your logins and settings across the hierarchy you have configured. No more remembering IP addresses; and it's **FREE!**
* [**1password**](https://1password.com/) - In a world of poorly hashed passwords (or plain text storage) and data breaches remembering lots of high strength passwords is a challenge. The 1password service is fantastic and secure, well worth a look!
* [**Paint.net**](https://www.getpaint.net/) - MS Paint on steroids, an open-source alternative to PhotoShop. It has many of the same features as PhotoShop but doesn't cost a penny.

# Development Environments and Plug-ins
* [**Visual Studio**](https://www.visualstudio.com/) - No list of .NET developer tools would be complete without the Visual Studio IDE. I spend 80% of my time in-front of Visual Studio, the rest is split between the application I am writing/debugging and SQL Management Studio. Visual Studio has been around for 11 years (launched in February 1997) and has matured into a very well rounded development environment. It supports everything the core languages can do, not surprisingly as it is written by the people who maintain (mostly anyway) those languages. You can acquire Visual Studio Community edition for free, so even a person looking to code for the first time can afford it; or you can purchase licences for the Professional and Enterprise versions of the software.
* [**SQL Server Management Studio**](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) - As a developer who started in the days of Query Analyser and Enterprise Manager (or Mangler as we called it), I have to like SSMS in comparison. A strong and clean IDE for managing SQL servers, and writing SQL queries. The intelisense can be a bit glitchy; but for a free tool you can't really complain. I have come across developers (or more often Systems Engineers) who insist on using some "free open-source alternative"; but as someone who has had to pick up the pieces when some unofficial tool borks a database, I have to ask why you would not use the official tool when it is so well rounded and **FREE!**?

# Visual Studio Plugins
* [**Jetbrains Resharper**](https://www.jetbrains.com/) - First of all resharper is not free, if you are paying for a tool out of your own pocket you might not like the price tag. That being said a few years ago they switched to a subscription model, so you can pay for it monthly if you feel like it. I have been using the resharper VS plug-in for around six years and it is the first thing I install when setting up a new Visual Studio instance. R# is a productivity and code analysis tool; it fills in all the little gaps in Visual Studios functionality. I don't like to say that a tool can make you a better developer (as you should know how to code anyway, a tool shouldn't have to tell you), but as we all know speed is sometimes important when a deadline is looming. R# helps you to see any potential pitfalls in the code you write (missing case statement options, potential null reference exceptions, over the top LINQ statements, etc). If you have not used R# before I urge you to download the free trial and see for your self.
* [**Layouts O Rama**](https://marketplace.visualstudio.com/items?itemName=LayoutsORama.LayoutsORama) - I switch between monitor layouts a lot; 3 widescreens and a laptop display at work, 2 widescreens and the laptop at home, or just the laptop display. Layouts O Rama allows you to save the displayed windows/snap-ins and their location in profiles; so when I switch to another location (or just un-dock for a meeting) I can just switch to a saved layout. The plug-in also understands the difference between debug and standard more; ensuring you always have the screens/snap-ins open that you required. I have also used this to switch up my interface when I move between working on desktop or web applications.
* [**Wix Toolset**](http://wixtoolset.org/) - The Wix toolset embeds the Windows Install XML process into visual studio making it easier to create MSIs (installers) for your applications. 

*I used to use a lot more VS plugins, but as both Visual Studio and resharper have matured many of them were made redundant or just become resource hogs.*

# SQL Management Studio Plugins
* [**SSMS Tools Pack**](https://www.ssmstoolspack.com/) - At only $30 this is a great extension of Sql Server Management Studio; it adds extended intelisense, code templates, safety checks (making sure you have a where clause, and no accidental truncates!), and code history. I find it's ability to keep a record of all the SQL I execute invaluable; being able to search for that bit of code you didn't think you needed to save is a great time saver!
* [**SQL Prompt**](https://www.red-gate.com/products/sql-development/sql-prompt/index) - SQL Prompt from Redgate is the next step up from SSMS Tools Pack; it performs many of the same functions but at a higher level. It's intelisense improvements are fantastic; but along with that level of function comes a higher price tag.

# Browser Plugins
*I generally use Chrome as my development browser as I find it's developer tools (F12) to be better than others. It also now integrates well into Visual Studio for javascript debug.*

* [**Edit This Cookie**](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=en) - A chrome plug-in that does just what it's name implies; allows you to see the cookies used by a page and edit or delete them. A great tool when working on your applications authentication and security processes.
* [**The Great Suspender**](https://chrome.google.com/webstore/detail/the-great-suspender/klbibkeccnjlkjkiokjodocebajanakg?hl=en) - Another chrome plug-in; this one suspends the processes of chrome tabs when you have not been using them for a while. Saving on system resources!
* [**1Password X**](https://blog.agilebits.com/2017/11/13/1password-x-a-look-at-the-future-of-1password-in-the-browser/) - A plug-in for Chrome (and other browsers) which embeds the 1password password manager into the browser. Providing quick fill-in of your secure passwords, and an easy way to create new logins.

# Team Tools
* [**Slack**](https://slack.com/) - Like it or loath it slack is a great communication tool for teams; their free offering is more than enough for small teams. Chat on desktop, web, and mobile. You can also integrate with their API to push notifications from other systems; I use it to notify the team when tickets are pushed onto 4th line support and give counts of any error notifications from disparate systems.
* [**Visual Studio Team Services**](https://www.visualstudio.com/team-services/) - The ultimate team tool for Visual Studio users; source control, backlog management, testing, automated builds and releases. The whole Projects, Development, and DevOps process. Plus you get five free accounts just for signing up; any Visual Studio subscribers also get a full account.
* [**Trello**](https://trello.com/) - At it's heart Trello is a simple kanban board system; keep track of project progress (or backlogs) in a clean UI. As with VSTS the free accounts are more than enough, until you want to fill your boards with plug-ins and external integration (just don't do that, kanban boards are best kept simple).

# Websites
* [**The Old Reader**](https://theoldreader.com/) - In my mind one of the biggest mistakes that Google ever made was shutting down the "google reader" system. The Old Reader is a re-spin of that platform that keeps much of the original layout and functionality using a more modern web platform. I use it at-least once a day to keep track of blogs and news sites.
* * [**Optimizilla**](http://optimizilla.com/) - An online tool for compressing images without loosing quality, great if you just want to compress a header image for your blog post (I use it on all the images for melodiouscode).