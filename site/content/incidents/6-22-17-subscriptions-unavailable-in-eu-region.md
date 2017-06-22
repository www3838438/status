+++
title = "Subscriptions Unavailable in EU Region"
severity = "partial-outage"
affectedsystems = [
  "Subscriptions",
]
resolved = true
date = "2017-06-22T01:45:00+01:00"

+++

# What Happened

Today at 1:45 CET The subscriptions API became unavailable in the EU region. 
Normally our monitoring systems would add new servers to the cluster and alert the on-call engineer. Today neither happened.

# What we're changing

Short term, we are looking into why our automated monitoring system failed to detect this issue.

Long term, we are investing in tooling that can help us understand complex failure scenarios in the production environment.
This will allow us to more quickly address the root cause of issues like this.
