+++ title = "Degraded Performance on Simple API" severity = "partial-outage" affectedsystems = [ "Simple API", ] resolved = true date = "2017-05-23T2:00:00+01:00"
+++



# What Happened

Today at 14:55 CET we observed slow queries and sporadic timeouts on the Simple API. Monitoring showed increased CPU use on the entire cluster. 

At 15:05 we could determine that adding capacity did not resolve the issue. In the following 15 minutes we examined logs and metrics to identify anomalies. We identified an internal reporting process that began continuously timing out at 14:52. Disabling this process resolved the issue.

# What we're changing

All Graphcool APIs throttle requests to ensure resources are never exhausted. Currently throttling is applied locally on each server in a cluster, so if a project is able to exhaust resources on a single server, adding more servers doesn't guarantee that other projects will be able to keep operating.

To address this we are doing two things. First, we will ensure that project-based throttling is enforced throughout the cluster. Secondly, over the next two months we will invest heavily in increasing performance of each node in the cluster. We have identified a series of optimizations that will allow us to increase server throughput 5 times and significantly reduce latency. These changes will ensure more stable service during events like today and improve latency of all queries and mutations to Graphcool.

# Infrastructure Maintenance

Today we are performing maintenance on the Graphcool infrastructure. Your projects might experience up to 5 minutes of reduced availability. In addition, it is possible that any schema migrations you perform during this period will be partially applied. This will result in errors in the Console, but will not impact your production API. If this happens, please contact our support via the website chat or in Slack.
