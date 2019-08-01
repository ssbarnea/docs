---
description: >-
  Use of future proof names for hosts and groups to avoid noisy warnings, bugs
  and other heaaches.
---

# Naming hosts and groups

While Ansible was quite flexible regarding what you could use for inventory hostnames and groups, things changed for the worse. Newer versions are complaining about use of dashes \(minus\) in group names.

Ansible also complains about using the same hostname as a groupname as this can cause confusions.

We also know that it would be pretty bad idea to use underlines as hostnames because they are not accepted by [RFC 822](https://www.ietf.org/rfc/rfc822.txt).

As I personally would find confusing to use different naming rules for hosts and groups, I came with the folowing practice:

* **remove dashes from groups,** even if it will take months to finalize it
* **rename groups** so they cannot accidentably be confused with single hosts. Using plurals seems fine.

There are ways to disable deprecation warnings or even to change the the group naming rules but you will only prolong your pain. 

Most people thing that getting a bandaid off quickly is less painful.

