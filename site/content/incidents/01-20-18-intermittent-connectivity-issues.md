+++
title = "Intermittent Connectivity Issues in the Simple API"
severity = "degraded-performance"
affectedsystems = [
  "Simple API",
]
resolved = true
date = "2018-01-20T12:30:00+01:00"

+++

**Investigating:** The Simple API in the EU and AP region is experiencing intermittent connectivity issues.

**Resolved:** The underlying issue of slow queries was an event queue that filled up. We are adding capacity to the slow component to prevent this from happening again.
