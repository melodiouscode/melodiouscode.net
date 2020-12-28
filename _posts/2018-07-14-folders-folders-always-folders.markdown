---
layout: post
title: Folders, Folders, always folders
date: '2018-07-14 09:59:14'
image: /images/posts/samuel-zeller-360588-unsplash-min.jpg
tags:
- development
---

Two of my employers' largest clients are law firms, and being law firms they regularly receive instructions from insurance firms for claims to be processed. This is where I come in, over the years I have created (or incremented) many instruction feeds that allow the insurance firms to electronically (normally via XML) instruct the law firms to investigate a claim.  These services get hit hard and often; in some cases receiving hundreds of fresh client instructions an hour, this creates a lot of data and transactional records. Storage of this data is the subject of this blog post.

Anyone who has been in a car crash and reported it to their insurer will know that it causes a lot of questions detailing every aspect of the incident. All these questions and answers (plus the schema data) can make for thousands of lines of XML (sometimes tens of thousands if the schema was badly designed!). Be it a good idea or not every service I have worked on has always had a project requirement to keep a copy of the XML in a place that is human accessable; this often ends up being the file system.

You guessed it, I am writing this quick article because I have just been bitten by a system which stored hundreds of thousands of little files in one big folder (it was not written by me).
<!--more-->
## The Problem
Windows has a limit on how many files should sit in a directory; depending on the level of resources available to the machine it can even crash explorer when you open a folder that contains a large number of files. You guessed it, this is where the 'folders, folders, always folders' subject comes in.
When you store a large number of files in a folder over a large time period (think several years), you need to break up the folder structure. Nothing is easier than simply placing files in a Year, Month, Day directory structure. 
> \\\SomeServer01\SomeShare\2018\07\14\Instruction001.xml

There are of course other options:
+ Store the files in the database
+ Store them in some sort of NoSQL store
+ etc

I used the word simple for a reason, and don't forget those project requirement documents!

## Why dates?
Humans understand dates, when a member of the helpdesk needs to locate an instruction file they can easily work out where it is based on the date it was processed/received/etc.

### Archiving
Any developer knows that systems often run out of storage space because the IT Systems Team were busy with something else and didn't notice, or the email alerts went to a folder rather than their inbox! Date formatted folders can easily be archived/zipped/etc.

### GDPR! 
In this new post GDPR world we should always think about how and for how long we store data, files stored in a date structured folder are very easy to locate and trim based on how old they are (not the only reason for deletion, but one of the many).

# Summary
To put it simply, don't forget how you store your data dumps. If you put a large number of files in a folder over a prolonged period of time, store them in a date formatted structure!
>\\\SomeServer01\SomeShare\2018\07\14\Instruction001.xml

<small>The header image for this post was provided for free on [unsplash.com](https://unsplash.com) by [Samuel Zeller](https://unsplash.com/@samuelzeller). Thanks Samuel!</small>