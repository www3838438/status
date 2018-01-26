+++
title = "Impaired Functions Deployment"
severity = "degraded-performance"
affectedsystems = [
  "Function Engine",
]
resolved = true
date = "2018-01-22T18:00:00+01:00"

+++

**Investigating:** Deploying Function is currently not possible. We are investigating the underlying issue.

**Update:** We are in close contact to our service provider to resolve this issue as soon as possible.

**Resolved:** We implemented a long-term solution for function deployment. We hit function deployment limits in our underlying AWS infrastructure, which caused function deployments to fail. To mitigate the issue, we now deploy functions evenly across a horizontally scalable number of AWS accounts.
