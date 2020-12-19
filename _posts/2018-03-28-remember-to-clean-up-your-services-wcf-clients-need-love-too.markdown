---
layout: post
title: Remember to clean up your services; WCF Clients need love too
date: '2018-03-28 13:38:15'
image: /images/posts/alina-grubnyak-334440-unsplash-1_bad07e5d9a46cb5a77c547006c2a2986.jpg
tags:
- development
---

All developers cringe when they start working on another person's code base; it is never in the state we would like it to be. Mostly that is because we developers are a picky bunch; everything has to be just perfect and nothing anyone else does ever is!
![profanity](/images/content/profanity.jpg)
Today I have been working on someone else's project, and the first thing that jumped out at me when I was doing some clean up was that none of the WCF Service calls (well most of them) had been closed. Whilst the program was being run by a single user in debug this wasn't really a problem, but add more users into the mix and it all goes pear-shaped.

## Remember to close your WCF Services
An open WCF Service consumes resources; memory, CPU, and anything it connects to (database readers etc). Especially if the developer of the service expected to dispose of their creations when the client was closed.

Picture this; you call a WCF Service method (let's call it GetMyStuff(int sessionId)). The GetMyStuff call hits a database to determine what stuff is yours, then to be nice and fast it spawns a bunch of threads to go and get all that stuff from other databases. You now have several connections to multiple databases open; all waiting to be closed when the service client is closed. But no one closes the client!

Normally a database will provide a few hundred possible connections to an application; when they are all open the application has to wait for more. If none of them is closed then the application will wait for a long time!

## How do you close a WCF Service Client?
<pre><code datalang="c">if(clientObject != null && clientObject.State == System.ServiceModel.CommunicationState.Opened){
    clientObject.Close();
}
</code></pre>

Just remember to run the above code somewhere after you are done with the client, if you are using the client in a 'using statement' just try this:
<pre><code datalang="c">using(var client = new ServiceClient()){
    ....
    ..
    .
    client.close();
}
</code></pre>

Simples!

### Thanks to [Alina Grubnyak](https://unsplash.com/@alinnnaaaa) for providing the header image for this post on [https://unsplash.com](https://unsplash.com).