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

Friday afternoon we identified the issue and deployed a temporary solution that greatly reduces the issue, but doesn't address the root cause. We will work on addressing the root cause over the weekend and provide a new update with more details when the final fix is deployed.

At this time the Console is fully operational and virtually all queries against all APIs perform as expected.

## Update Saturday

The temporary solution has proven to provide stable performance, so at this point we declare the incident resolved. We will post a detailed update once the permanent solution has been rolled out.

In addition to the degraded performance, a bug was introduced Thursday that caused UPDATE and DELETE subscriptions to not work for specific types. As we were busy investigating the performance incident it took longer to react to this than normal. At this time Subscriptions are fully working for all projects.
