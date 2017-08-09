+++
title = "Degraded Performance for APIs"
severity = "degraded-performance"
affectedsystems = [
  "Files API",
  "Images API",
  "Relay API",
  "Simple API",
  "System API",
  "Console",
  "Simple Subscriptions API"
]
resolved = true
date = "2017-08-03T14:30:00+02:00"

+++

All APIs are experiencing degraded performance, also affecting the usage of the Console. We are currently investigating the underlying issue.

## Update Friday

Friday afternoon we identified the issue and deployed a temporary solution that greatly reduced the issue, but doesn't address the root cause. We will work on addressing the root cause over the weekend and provide a new update with more details when the final fix is deployed.

At this time the Console is fully operational and virtually all queries against all APIs perform as expected.

## Update Saturday

The temporary solution has proven to provide stable performance, so at this point we declare the incident resolved. We will post a detailed update once the permanent solution has been rolled out.

In addition to the degraded performance, a bug was introduced Thursday that caused UPDATE and DELETE subscriptions to not work for specific types. As we were busy investigating the performance incident it took longer to react to this than normal. At this time Subscriptions are fully working for all projects.

## What Happened

On Thursday we deployed a major refactoring of all APIs. Our normal engineering practice is to do small incremental releases that can be tested and deployed independently. The nature of this particular change was such that we decided to do a big release across all services. After the deployment, all metrics indicated no issues. Thirty minutes after the release we started to observe elevated error rates and further investigation showed that API servers were being taken out of clusters serving live traffic because they became too slow to respond to requests. The complex nature of the recent release caused delay in identifying the root cause.

The issue turned out to not be related to recent code changes but were instead caused by changes introduced in specific customer projects. Friday afternoon, we had identified specific projects that were causing API servers to be taken out of the cluster. Further investigation revealed a fundamental flaw in the way Graphcool generates GraphQL input objects used in [nested mutations](https://www.graph.cool/blog/improving-dx-with-nested-mutations-vietahx7ih/).

Graphcool is pushing the limits of GraphQL in order to support the most convenient API for developers. Our support for nested mutations was implemented with a naive recursive algorithm suffering from combinatorial explosion for types with many relations, causing schema build times to sky rocket and GraphQL schemas to be much larger than required.

Today, we released the final fix to this issue, reducing the average build time from 90 ms to 3 ms and the slowest schema build time by 3 orders of magnitude.

## What we are changing

Graphcool is a multi-tenant system that is subject to the issue known as noisy neighbours - the fact that other customers on the same machine can affect the performance of your project. We are mitigating this issue by clustering both the API and database layer as well as employing per-project throttling to ensure that too many requests against a single project cannot impact other projects in the same cluster. This strategy works really well, but so far the schema building component has not been subject to throttling. We have introduced detailed monitoring of this component and are investigating how we can further isolate this component.
