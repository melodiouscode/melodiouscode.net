---
layout: post
title: FontAwesome Spacing - The small things
date: '2019-04-30 12:35:31'
image: /images/posts/nasa-45076-unsplash-min.jpg
tags:
- development
- web
- css
---

It is often the small things which make a difference in an application; or at least in the end users opinion of the application. In this case, it is as small as a single space, just a bit of padding, room to breath!  
Although this article talks about FontAwesome the functionality used is nothing to do with it; it just becomes a bit more evident when using a web-based icon library such as FontAwesome.

<figure class="kg-card kg-image-card"><img src="/images/content/image.png" class="kg-image"></figure>

The icon in the above screenshot is a standard FontAwesome icon with no special treatment; it is a little to close to the text for my liking, it cluttered (it can also confuse a screen reader). However, the icon in the next screenshot is ever so slightly further away, but the code is the same.
<!--more-->
<figure class="kg-card kg-image-card"><img src="/images/content/image-1.png" class="kg-image"></figure><!--kg-card-begin: markdown-->

    <h5 class="modal-title" id="errorModalLabel"><i class="far fa-exclamation-square"></i>Error message</h5>

<!--kg-card-end: markdown-->

This has been achieved with a little known line of CSS wizardry; the 'after' attribute.

<!--kg-card-begin: markdown-->

    i:after{
    	content: " ";
    	white-space: pre;
    }

<!--kg-card-end: markdown-->

The above lines of CSS tell the browser to render a single space after and "i tag", this automatically gives us the extra bit of space without the need to add it to every icon we use. Magic!  
Once you realise the "after" attribute exists you can use it for all sorts of things, like adding a colon to the end of your labels rather than having to dirty the MVC attributes with them! The possibilities are endless (well not really, the attribute won't feed you or solve world peace).

<!--kg-card-begin: markdown-->

    label[for]:after {
    	content: ":";
    }

<!--kg-card-end: markdown--><!--kg-card-begin: markdown-->

<small>Thank you to <a href="https://unsplash.com/@nasa">NASA</a> for the header image on this post provided via <a href="https://unsplash.com">Unsplash</a>.</small>

<!--kg-card-end: markdown-->