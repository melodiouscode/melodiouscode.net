---
layout: post
title: Serving a single page with a Cloudflare Worker
date: '2019-03-02 16:29:42'
image: /images/posts/jamie-street-368704-unsplash-min.jpg
tags:
- azure
- cloudflare
---

Ok, so I may have gone overboard on the [dot dev](https://get.dev) domains, obviously, I purchased [melodious.dev](https://melodious.dev) and forwarded it to this website but I also purchased two random domains:

- [itworksonmymachine.dev](https://itworksonmymachine.dev)
- [i-am-a-great.dev](https://i-am-a-great.dev) (in response to spotting @CydeWeys buying i-am-a.dev whilst I was searching twitter for #dotdev)
<figure class="kg-card kg-embed-card"><blockquote class="twitter-tweet">
<p lang="en" dir="ltr">Look which <a href="https://twitter.com/hashtag/dotdev?src=hash&amp;ref_src=twsrc%5Etfw">#dotdev</a> domain I have grapped <a href="https://t.co/XUWQUS0iwK">https://t.co/XUWQUS0iwK</a> 😁</p>— Marvin C. (@marvincaspar) <a href="https://twitter.com/marvincaspar/status/1101186373921525762?ref_src=twsrc%5Etfw">February 28, 2019</a>
</blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</figure>

I could have just forwarded these domains to [melodiouscode.net](https://melodiouscode.net), but on my lunch break, I decided to chuck some single page sites at them for giggles. I, however, did not want to spend any more money than I already do on domain-related things. In steps [Cloudflare](https://cloudflare.com) [workers](https://www.cloudflare.com/en-gb/products/cloudflare-workers/).

For those that do not know about workers; they are small chunks of javascript that you can run on the "edge" of Cloudflare. This means that you can execute code at the moment that a page is requested from your site. In the case of my serverless approach, the code executes before the page request has the chance to realise there is no web server!

<figure class="kg-card kg-image-card"><img src="/images/content/worker.png" class="kg-image"></figure>

The above code binds to the "page fetch" event before the page request is processed the worker code jumps in and grabs a static piece of HTML from my Azure Blob storage and returns that instead!  
It is that simple, with just a few lines of javascript I can serve a simple web page without the need for a web server and at near-zero cost (seeing as I already pay for the workers and the blob storage cost is almost zero).

A quick post for a quick website! I may at some point put something more useful/meaningful/silly onto both of these domains, but for now, remember that you are [a great dev](https://i-am-a-great.dev) because it [works on your machine](https://itworksonmymachine.dev)!

### Update (15/03/2019)

Whilst monitoring a database migration this evening I decided to have a play with Cloudflare Workers again; i-am-a-great.dev is now purely served using a worker (no blob storage). On top of that, it also uses the Workers 'Key Value Pair' API to store a counter that is incremented each time the page is visited.

<!--kg-card-begin: markdown-->

    async function handleRequest(request) {
      let counter = await iamagreatdev.get("counter")
      let increment = parseInt(counter) + 1
    
      await iamagreatdev.put("counter",increment);
    
      let html = "...THE HTML FOR THE PAGE!..."
      
      html = html.replace("{{COUNTER}}", increment)
      
      let securityHeaders = {
         //...
         //various headers
         //...
      }
    
      return new Response(html, {
        status: 200,
        statusText: "OK",
        headers: securityHeaders
      })
    }
    
    addEventListener('fetch', event => {
      event.respondWith(handleRequest(event.request))
    })

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

<small>Thank you to <a href="https://unsplash.com/@jamie452">Jamie Street</a> on <a href="https://unsplash.com">Unsplash</a> for providing the header image for this post.</small>

<!--kg-card-end: markdown-->