+++
title = "Mutations Unavailable"
severity = "partial-outage"
affectedsystems = [
  "Simple API",
  "Relay API",
  "File API",
]
resolved = true
date = "2017-04-12T09:00:00+01:00"

+++

### What happened

An hour ago our primary database had a failover event that promoted a read replica to master. During this period all APIs were unavailable for less than 2 minutes.

15 minutes later, following normal procedure, a new database instance was added to the cluster and promoted to master. When this happens, the replica that had temporarily acted as master is returned to its original role as a read replica.

To maintain data consistency in our cluster, read replicas disallow all write actions. Unfortunately, when the new instance assumed the master role some of our API servers kept sending writes to the temporary master that was now in read-only mode. For this reason mutations were failing sporadically for a period of 20 minutes after the failover.

Full service was restored when we manually restarted the affected API instances.

### What we're changing

We are investigating what caused the API servers to keep sending write traffic to the read-only DB instance.

We are extending the ongoing status checks on our API servers to cover mutations so a scenario like this can be automatically resolved in the future.

We are in dialogue with AWS to identify the root cause of the database failover event.
