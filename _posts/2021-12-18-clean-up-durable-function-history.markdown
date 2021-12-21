---
layout: post
title: Clean up your durable functions history
date: '2021-12-18 07:21:00'
image: /images/posts/the-creative-exchange-cpIgNaazQ6w-unsplash_1000-min.jpg
tags:
- azure
- c-sharp
- dotnet
- developer
- azure-functions
- durable-functions
- clean-code
---

Recently I have been working with Azure Durable Functions, which are an extension of the Azure Function platform. Durable Functions provide a way to define a workflow that maintains a state between executions or during asynchronous runs of each part of the workflow.

I intend to write several posts on Azure Functions in the coming months, but for now, I want to write about cleaning up after durable function workflows, as it took me some time to work out how to do it myself.

## Durable Function History
If you already understand how durable functions maintain their state and history, scroll down to the next section; otherwise, keep reading to learn how durable state works.

Every output of a durable activity (or the orchestrator itself) is stored as part of the orchestration history; one of the requirements of activity functions is that their return type can be serialised and deserialised, and stored in JSON format. This JSON data is then stored in Azure Storage (blobs, queues, and tables) to be retrieved when the function resumes (after waiting on an activity or external event).

What isn't immediately apparent to developers is that this history is stored forever, an ever-growing pile of JSON in your storage accounts.
<!--more-->
## Why is this bad?
Ignoring the ever-increasing cost of the storage (blobs are cheap), if your function workflows process confidential data (and even if they don't), this forms a data security risk. Any good developer or cloud architect ensures that their database and application storage are secured (and implementing data minimisation), but it is easy to overlook the storage container that backs an Azure Function. It usually only contains basic log information that gets deleted automatically. 

If you were processing incoming financial or medical records, perhaps performing a machine learning activity, these JSON files might contain highly confidential information that will just sit there (duplicated from where it is meant to be stored) forever. What happens when someone obtains the keys to that storage container; they could exfiltrate masses of information, including information you think you have deleted from the system (following GDPR requests, for example).

## How can I keep my functions clean?

There are three ways to keep the function history clean:

1. Delete the history as you go.
2. Store tracking information and delete based on a workflow.
3. Delete the history on a schedule.

The first option requires storing the execution payload each time an orchestrator is started as it contains the URL to call that purges the executions data. The application that initiates the workflow also needs to monitor the orchestrations progress and execute the purge correctly. A viable option if your orchestrations are heavily managed but not the easiest or most efficient route.

Option two requires persistent storage, such as a database, to keep track of your execution payloads and a workflow to trigger the purges when appropriate. The code to purge a single workflow entity is simple and can be performed with a standard HTTP Trigger.

<!--kg-card-begin: markdown-->

    // in some form of iteration, after loading the list of IDs to purge simply call the admin API.
    await orchestrationClient.PurgeInstanceHistoryAsync(idToPurge);

<!--kg-card-end: markdown-->

The third option, and in my opinion the better option, is to delete the history based on a time window. There is a negative to this option; if your functions app contains a very high number of executions (or an extensive range of orchestrations), then the storage load can be high whilst performing the purge. However, the more often you purge, the less this becomes a problem.

<!--kg-card-begin: markdown-->

    [FunctionName(nameof(OrchestrationHistoryPurgeTimer))]
    public async Task OrchestrationHistoryPurgeTimer (
        [TimerTrigger("%SomeAppSettingWithTheCronValue%")] TimerInfo timerInfo,
        [DurableClient] IDurableOrchestrationClient orchestrationClient,
        ILogger log)
    {
        // a value far enough into the history to support your workflows execution times.
        var from = DateTime.UtcNow.Subtract(TimeSpan.FromDays(365));
        
        // a value that indicates the end period to delete based on your data retention needs.
        var to = createdTimeFrom.AddDays(30);

        // the statuses to delete, perhaps you want to keep errors!?
        var status = new List<OrchestrationStatus>
        {
            OrchestrationStatus.Completed
        };

        await orchestrationClient.PurgeInstanceHistoryAsync(from, to, status);
    }

<!--kg-card-end: markdown-->

## In summary
You should always know what data your applications store, especially if it is out of sight in a non-standard data store. When working with Azure Durable Functions, you need to ensure a viable strategy to maintain your history and state.

A time-based purge is less efficient than storing your execution identifiers, but it is an easy route to take that requires no additional resources.


<small>Cover Photo by <a href="https://unsplash.com/@thecreative_exchange?utm_source=melodiouscode&amp;utm_medium=referral&amp;utm_content=creditCopyText">The Creative Exchange</a> on <a href="https://unsplash.com/photos/cpIgNaazQ6w?utm_source=melodiouscode&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></small>