## Firewall considerations 

The default RouterOS firewall will block the tunnel from establishing properly. The traffic should be accepted in the "input" chain before any drop rules on both sites.
