+++
title = "Intermittent Connectivity Issues in the Simple API (US Region)"
severity = "degraded-performance"
affectedsystems = [
  "Simple API",
]
resolved = true
date = "2017-12-10T06:16:00+01:00"

+++

**Investigating:** The Simple API in the US region is experiencing intermittent connectivity issues.

**Resolved:** Slow processing of subscription messages caused our API servers to lock up and restart. We are adding additional monitoring to this part of our infrastructure.
