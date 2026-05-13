## Protect the router itself 

Rules of thumb followed to set up the firewall: 

work with `new` connections to decrease the load on a router; accept what you need `drop` everything else, `log=yes` could be set to log some attackers, but keep in mind that it may add some load to he CPU on heavy attacks. 

We always start by accepting already known and accepted connections, so the first rule should be to accept "established" and "related" connections.
