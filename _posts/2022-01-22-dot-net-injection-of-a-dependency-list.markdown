---
layout: post
title: .NET Injection of a dependency list
date: '2022-01-22 08:00:00'
image: /images/posts/ivan-diaz-_ts3NfjvaXo-unsplash-min.jpg
tags:
- c-sharp
- dotnet
- developer
- dependency-injection
- clean-code
---

Whilst doom scrolling Twitter last night, I came across a tweet by a Norweigan software developer named <a href="https://twitter.com/KarlSolgard" target="_blank" title="Karlsolgrad on Twitter">KarlSolgard</a>; he tweeted about a feature of .NET Core Dependency Injection that I was unaware existed.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/dotnet?src=hash&amp;ref_src=twsrc%5Etfw">#dotnet</a> tip:<br>You can register services with same interface and inject them as a list in ctor <a href="https://t.co/pa8hhSGIsg">pic.twitter.com/pa8hhSGIsg</a></p>&mdash; Karl 🔥 (@KarlSolgard) <a href="https://twitter.com/KarlSolgard/status/1484527534742114306?ref_src=twsrc%5Etfw">January 21, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Injecting a class or a factory is something that every .NET developer has come to know; however, you can inject an IEnumerable of something. By registering multiple implementations of an interface, your classes can ask for an array of concrete implementations of that interface.
<!--more-->

<!--kg-card-begin: markdown-->

    var services = new ServiceCollection()
    .AddSingleton<IMessageHandler, EmailHandler>()
    .AddSingleton<IMessageHandler, SmsHandler>()
    .AddSingleton<IDataSource, FakeDataSource>()
    .AddSingleton<IMessageSender, MessageSender>()
    .BuildServiceProvider();

    var dataSource = services.GetService<IDataSource>();
    var messages = await dataSource!.GetPendingMessagesAsync();
    var sender = services.GetService<IMessageSender>();

    await sender!.SendMessagesAsync(messages);

<!--kg-card-end: markdown-->

I asked the tweet's author for an <a href="https://t.co/pknmCiX9nG" target="_blank" title="FizzBuzz4Champs">example</a>, and they replied with a way to tackle the traditional <a href="https://en.wikipedia.org/wiki/Fizz_buzz" target="_blank">FizzBuzz challenge</a>, but I wasn't satisfied and challenged myself to look for a more practical example.

Sending messages to different services based on some internal logic is often a pattern I have to write. So I went away and wrote a basic message sending system that doesn't contain any hardcoded logic to determine how to send different messages. 

The code in <a href="https://github.com/melodiouscode/demo-Multi_IOC_DI" target="_blank" title="My Demo Repository">my demo repository</a> isn't a complete example, and it may be a bit contrived, but it does show a practical implementation of the 'IEnumerable Injection' pattern.

<small>Cover Photo by <a href="https://unsplash.com/@ivvndiaz?utm_source=melodiouscode&amp;utm_medium=referral&amp;utm_content=creditCopyText">@ivvndiaz</a> on <a href="https://unsplash.com/photos/_ts3NfjvaXo?utm_source=melodiouscode&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></small>