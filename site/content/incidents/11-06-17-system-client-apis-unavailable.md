+++
title = "System and Client APIs unavailable"
severity = "major-outage"
affectedsystems = [
  "Simple API",
  "Simple Subscriptions API",
  "Relay API",
  "System API",
  "Files API",
  "Images API",
  "Function Engine",
  "Console",
]
resolved = true
date = "2017-11-06T17:15:00+02:00"

+++

**Investigating:** We are currently investigating a major outage across the System and client APIs.

**Resolved:** All APIs have been restored. Further investigation has determined that the cause of the issue was a misconfiguration of dependencies in our dependency injection framework. This particular misconfiguration did not manifest itself in our automated tests, and was mistakenly allowed to be deployed to production. To avoid this in the future, we are introducing a broader set of tests designed to catch configuration issues like this.
