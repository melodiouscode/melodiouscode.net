---
layout: post
title: Obtaining the meta data from a SQL Query
date: '2019-01-10 12:43:53'
image: /images/posts/dm_exec_descrive_first_result_set____example-min-1.png
tags:
- development
- sql
---

I recently had a need to find a way of obtaining just the column names returned by a SQL Server Query; the query in question is ad-hoc and entered into an application by the user (in this case my application is a WPF desktop application, and the query is Microsoft T-SQL).

One quick and simple way of obtaining the column names would be to execute the query; I will not go into the details of why executing arbitrary SQL statements pasted into a text box by your users is a bad idea. Suffice to say it is a very bad idea; especially if your application is run with higher privileges. In my case, these pasted queries are also persisted in the database if a user with low rights passed a dangerous query someone with higher rights could come across it in the future causing it to be executed.

I needed to find an alternative; I contemplated a couple of things:
+ A complicated Regular Expression (RegEx)
+ Wrapping the execution in a BEGIN TRANSACTION and ROLLBACK TRANSACTION.
+ Running the query under a low (db_reader only) privilege account

Whichever way I looked at it the options didn't seem great, and I thought there must be an alternative. It turns out there is!
<!--more-->
## Obtaining the SQL Query Meta Data (Columns) of a recordset without executing it!
From SQL Server 2012 a new Dynamic Management View (DMV) exists called sys.dm_exec_describe_first_result_set; this view allows you to obtain the metadata for the first possible result set in a T-SQL batch. Put simply it returns information about the columns returned from the first SELECT statement a query will hit (it is a little more complicated in that IF statements and the such can affect it, but basic queries work fine).
The command takes an NVARCHAR parameter which will be analysed (but not executed); a table of results is then provided in the normal way.
![dm_exec_descrive_first_result_set____example-min](/images/content/dm_exec_descrive_first_result_set____example-min.PNG)
In my use scenario I created a stored procedure which takes an NVARCHAR(MAX) string as a parameter and passes it to this command; returning to me a result set containing (amongst other things) all the column names in order.

It's easy once you know how! I urge anyone who is reading this to check out the [Microsoft Docs](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql?view=sql-server-2017) article on this command; as we all know you shouldn't just run the code you find on some guy's blog!