---
layout: post
title: Using Postman Securely
date: '2021-12-28 16:38:00'
image: /images/posts/mailbox-gce8e7f61a_1920-min.jpg
tags:
- developer
- api
- security
---
I will skip over any jokes about using a postman and go straight to the subject at hand, using Postman securely. 

## What is Postman?
[Postman](https://www.postman.com/){:target="_blank"} is a desktop and browser-based application that many developers use for calling or testing APIs; it also has additional features for testing and automating API workflows. However, this post is not to teach you about Postman but to teach you how to use it securely; if you want to learn more about Postman and how to use it, read the documentation on [postman.com](https://learning.postman.com/docs/getting-started/introduction/){:target=_blank}.

## The Postman Cloud
One of the key features of Postman is its ability to store your [API Collections in the cloud](https://www.postman.com/product/workspaces/){:target="_blank"}; you can access your collections from anywhere and share them with your team. However, this means that the collection, including sensitive information, is stored on Postman's servers. Depending on the sensitivity of your data and any rules at your organisation, you may be happy with this, or you may not (a question to ask your security team, not a question for my blog to answer!).
<!--more-->
## Initial and Current Variables
[Postman collections](https://learning.postman.com/docs/sending-requests/intro-to-collections/){:target="_blank"} can predefine variables used in multiple API Requests, such as usernames, passwords, and standard settings (like a base URL).

Variables have two modes; initial value and current value; all variables have an initial value stored with the collection (and synchronised to the Postman Cloud). When you change the value of a variable within a request (via tests, pre-request scripts, etc.), the new value is stored in the current value property. The current value is saved with the collection, but only on the local machine, and it is not uploaded to the cloud.

### Creating Variables
Variables are stored with your collection; select the 'variables tab' from the collections settings screen. 
![Postman Variables Screen](/images/content/postman-vars-min.png)

You can use a variable anywhere within a request by placing its name in curly braces.
![Postman Variables In Use](/images/content/postman-use-vars-min.png)

### Using Variables Securely
You can choose to set the initial value to an empty string (no characters) and allow that to be stored in the collection and uploaded to the cloud. Place any sensitive information inside the current value, such as the password in the example above.

Use these variables you have created within the requests in your collection; the variable's actual value is injected into the request when you execute it.

## Summary
Postman is a fantastic tool for developers working with APIs, but as with any tool (especially cloud-based tools), you need to be conscious of how much data you are sharing. Postman attest to the level of security, encryption, and privacy baked into their system; however, any firm is only one data breach away from finding out they are less secure than they thought! You can minimise your exposure by using the "current value" of variables rather than storing your secrets in the "initial value" that is then uploaded to the postman cloud (and included in any manual JSON exports from the postman client).