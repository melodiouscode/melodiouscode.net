---
layout: post
title: Dependency Injection with Azure Functions
date: '2020-04-11 15:24:52'
image: /images/posts/sara-bakhshi-MfnX4XtGnvU-unsplash-min.jpg
tags:
- azure
- c
- dotnet
- developer
- microsoft
- net
---

I have been making good use of Azure Functions recently; their simple hosting style makes spinning up micro-services quick and easy whether they be HTTP, Blob, Table, or scheduled triggers. I have been making use of the schedule triggers recently to automate various processes for larger systems (they are substantially cheaper and easier to manage than Virtual Servers); to do so I have needed to make use of model/data layers within the rest of an application stack. Like most good code the other layers of these applications were designed to make use of IOC (Injection of Control) frameworks and DI (Dependency Injection; initially it seemed that IOC and DI were not possible with the Azure Functions platform. However, the addition of the support for Startup classes in Azure Functions v2 allows you to make use of the .NET Core Dependency Injection framework.
<!--more-->
### Include a Startup Class in your Function

Before you can make use of a Startup Class in your Azure Function you need to reference 'Microsoft.Azure.Functions.Extensions'; you can reference it via NuGet.  
Add a class file to the root of your project named Startup.cs; to ensure that the Functions Project makes use of the start-up code you need to add a few lines to the class file.

<!--kg-card-begin: markdown-->

    using DependencyInjectionFunctions;
    using Microsoft.Azure.Functions.Extensions.DependencyInjection;
    using Microsoft.Extensions.DependencyInjection;
    
    [assembly: FunctionsStartup(typeof(Startup))]
    namespace MyFunctionsApp {
    
       public class Startup : FunctionsStartup {
          public override void Configure(IFunctionsHostBuilder builder) {
             throw new System.NotImplementedException();
          }
       }
    }

<!--kg-card-end: markdown-->

By extending FunctionStartup (which in turn implements IWebJobStartup) you ensure that your code is part of the Functions initialisation process.

### Register your Dependencies

You can now use the configure method to register your applications dependency requirements using the IFunctionsHostBuilder provided in the Configuration method.

<!--kg-card-begin: markdown-->

    public class Startup : FunctionsStartup {
        public override void Configure(IFunctionsHostBuilder builder) {
           builder.Services.AddSingleton();
           // or one of the other life time options
           // builder.Services.AddTransient();
           // builder.Services.AddScoped();
        }
    }

<!--kg-card-end: markdown-->

You can now make use of Dependency Injection as you normally would by adding Interface parameters to your class constructors and registering them with the Services collection in your Startup.cs file.

Now that you know how to register dependencies in your Azure Functions Projects you can not go ahead and write better more maintainable micro-services.

<!--kg-card-begin: markdown-->

<small>Thank you to <a href="https://unsplash.com/@sarabakhshi" target="_blank">@sarabakhshi</a> on <a href="https://unsplash.com/photos/MfnX4XtGnvU" target="_blank">unsplash.com</a> for providing the header image used in this post for free.</small>

<!--kg-card-end: markdown-->