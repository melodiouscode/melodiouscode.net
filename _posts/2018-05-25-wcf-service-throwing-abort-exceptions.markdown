---
layout: post
title: WCF Service aborted by the server
date: '2018-05-25 20:40:08'
image: /images/posts/maria-freyenbacher-258254-unsplash-min.jpg
tags:
- development
- wcf
- debug
---

An error occurred while receiving the HTTP response to [http://localhost:12345/SomeService.svc](http://localhost:12345/SomeService.svc). This could be due to the service endpoint binding not using the HTTP protocol. This could also be due to an HTTP request context being aborted by the server (possibly due to the service shutting down). See server logs for more details.

This evening I spent more time than I would care to admit working on a problem in a WCF Service I am building. The service has been working well for a number of weeks whilst it has all its functions ironed out; suddenly today after adding in one of those functions it stopped working in debug. I blame tiredness and a busy day in the office for me not realising the error faster, but for those who like me get tired here is the cause of the above error (or at least this version of the error).

<!--kg-card-begin: markdown-->

    [DataContract]
    public enum LoginResultFlag {
        [EnumMember]
        Success = 100,
    
        [EnumMember]
        Failure = 200,
    
        [EnumMember]
        PasswordChangeRequired = 300,
    
        [EnumMember]
        AccountLocked = 400,
    
        [EnumMember]
        RequiresChallenge = 500,
    
        [EnumMember]
        SetupChallengeResponse = 600
    }

<!--kg-card-end: markdown-->

Can you see the problem; it took me a little while of trial end error before I spotted it the moment I looked at the enum. Enums cannot be null, at their most basic they are integers and take the value 0. If you specify integer values as I have done here without adding a zero value then it cannot be serialized/deserialized through the web service boundary. All I had to do was add the following to the enum:

<!--kg-card-begin: markdown-->

    [EnumMember]
    NotSet = 0

<!--kg-card-end: markdown-->

Problem solved!

The header image on this post was provided by [Maria Freyenbacher](https://unsplash.com/@freyenbacher) on [unsplash.com](https://unsplash.com). Thank you Maria!

