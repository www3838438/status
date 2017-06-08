+++
title = "Intermittent Connectivity Issues On Simple API"
severity = "degraded-performance"
affectedsystems = [
  "Simple API",
]
resolved = true
date = "2017-06-8T02:00:00+01:00"

+++

# What Happened

Today at 2:05 CET we observed increased load on our Simple API cluster. We added servers to the cluster in order to deal with the increased load. Unfortunately by the time the new servers joined the cluster the load had further increased.

At 2:55 CET enough servers had joined the cluster to handle the spike in traffic. During this period the API servers would drop a percentage of all incoming requests. 

# What we're changing

The root cause of this incident was our inability to add API servers fast enough. We are working along two paths to increase API stability:

1. We are performing ongoing performance optimization on the API servers that will allow each server to handle significantly more traffic.

2. We will be improving the way we scale up clusters under load to make sure we can add capacity fast enough to be able to handle increased load.
