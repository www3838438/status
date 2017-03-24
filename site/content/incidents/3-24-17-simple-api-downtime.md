+++
title = "Simple API Downtime"
severity = "partial-outage"
affectedsystems = [
  "Simple API",
]
resolved = true
date = "2017-03-24T2:00:00+01:00"

+++

Update: We've found and resolved the issue. We'll shortly publish a more detailed post-mortem.

The Simple API is currently unavailable. We're looking into the problem.

### What Happened

Tonight at 1:40 CET api.graph.cool/simple became unavailable. At 9:05 CET we restored full access. 

Two days ago we moved our api clusters to a new infrastructure setup. This was part of ongoing maintenance and was done without downtime. In this process we also changed our deployment setup and unfortunately a bug was introduced that would allow broken builds to be deployed to production. Such a broken build was pushed yesterday at 10:30 CET. When the load balancer attempted to add this build to the cluster it correctly detected that the build was broken and blocked it from being included in the cluster. From 10:30 to 1:40 the load balancer continuously tried to deploy the broken build. At 1:40 a separate event occoured that caused the existing simple-api instances to be removed from the load balancer. Ordinarily this woudln't be an issue, but because the latest build was broken the load balancer had no way add new capacity.

In addition to the cluster infrastructure change we recently made changes to our logging infrastructure. For this reason we were not alerted to errors happening during instance initialization.

### What Are we Changing

We have already changed our deployment setup so that broken builds can no longer be deployed to production. We are currently improving our logging infrastructure to ensure that we are alerted about all incidents in the future.
As described above, the incident that occured at 1:40 tonight could only happen because the deployment of a broken build was pending for the previous 3 hours. This is a condition we could have detected before it impacted production. Over the next two days we will identify such conditions in our setup and put in place predictive alerting. This will allow us to respond to simple errors before they impact production.
