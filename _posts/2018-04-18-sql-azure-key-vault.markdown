---
layout: post
title: Azure SQL Connector for the Azure Key Vault - Error 2058
date: '2018-04-18 19:45:04'
image: /images/posts/thomas-kvistholt-191153-unsplash-min.jpg
tags:
- development
- azure
- sql
---

I spent today in a session with our external SQL Advisor; we have been working on provisioning a set of SQL Servers in Microsoft Azure. These servers will be using SQL Server TDE, which is a total database encryption system. I will not go into details of how this works, or what the setup is; however I will explain a problem we had in the hope that someone else will read this article and not spend an entire day trying to work out the cause!

>Key with name 'SOME_KEY_NAME' does not exist in the provider or access is denied. Provider error code: 2058.  (Provider Error - No explanation is available, consult EKM Provider for details)

The above error message was presented to us when we tried to create the asymmetric key for the server. According to the [official set of error codes](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting?view=sql-server-2017), error 2058 does not exist! What really confused us is that we had three other servers connect without a problem; those servers were created last year. The fourth problem server was only created this month; can you see where I am going with this?

It turns out that there is a bug in the February 2018 release of the [SQL Server Connector for Microsoft Azure Key Vault](https://www.microsoft.com/en-us/download/details.aspx?id=45344) that was released that month (version 15.0.300.96). We had used a previous release of the installed on the first three servers.

## How to fix Error 2058
The Feb release contains a requirement for a new registrary key; nothing has the rights to create that key (SQL Engine, connector, or the DLLs). The, unfortunately, the workaround is to create the following registry key:

>In the HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft node create a key "SQL Server Cryptographic Provider"

Once you have created the key grant full permissions on the key to the account which runs the SQL Engine Service. You should now be able to access the key vaults and create your keys.

Or of course, you could do what we did, and use the old version of the installer (patching is a problem for future me).

<small>The header image for this post was provided on [unsplash.com](https://unsplash.com) by [Thomas Kvistholt](https://unsplash.com/@freeche), thank you Thomas!</small>