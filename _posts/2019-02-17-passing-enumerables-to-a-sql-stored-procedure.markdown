---
layout: post
title: Passing Enumerables to a SQL Stored Procedure
date: '2019-02-17 12:40:56'
image: /images/posts/kelly-sikkema-411622-unsplash-min.jpg
tags:
- c-sharp
- developer
---

I have been asked the question "Can you pass an enumerable to a procedure?" or "How do you pass a table to a stored procedure" several times in the past. The simple answer is "yes", the slightly more complex answer is "yes, and this is how"!

## How to pass an Enumerable to a SQL Stored Procedure in .NET

Although my example code here is in C# the same process applies to other .NET languages.  
You can indeed pass an enumerable object to your Stored Procedure by using a special type of SQL object called a "User Defined Table Type". UDTTs can be used to create tempory tables in a SQL Query without the need to fully write out the TABLE statement; in much the same way they can be used to pass a tempory table to a stored procedure. The only restriction is that the parameter passed into the query must be marked as read-only.  
An example SQL statement to create a User Defined Table Type is as follows:
<!--more-->
<figure class="kg-card kg-image-card"><img src="/images/content/udtt.png" class="kg-image"></figure>

An example of using that type in a procedure is also as follows:

<figure class="kg-card kg-image-card"><img src="/images/content/proc.png" class="kg-image"></figure>

Now the question is how to execute a procedure from a .NET application passing in your enumerable? The easiest way is to create a Data Table with a matching schema to the UDTT.

<figure class="kg-card kg-image-card"><img src="/images/content/definetable.png" class="kg-image"></figure>

You can then execute your stored procedure in the normal way, passing the table to the parameter on creation (or in your preferred way); just make sure you also set the TypeName of the parameter and set the type to Structured.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/images/content/ado.png" class="kg-image"><figcaption>I neglected to take a screenshot of this bit when mocking the above code, so this is from a project I am working on! Sorry for the differing paramter names, but @LookupList would be @Table, and [FSD].[DetailLookup] is [dbo].[MyTableType].</figcaption></figure>