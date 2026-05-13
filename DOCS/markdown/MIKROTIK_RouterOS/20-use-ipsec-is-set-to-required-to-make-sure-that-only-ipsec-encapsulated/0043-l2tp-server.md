## L2TP Server 

An interface is created for each tunnel established to the given server. There are two types of interfaces in the L2TP server's configuration 

Static interfaces are added administratively if there is a need to reference the particular interface name (in firewall rules or elsewhere) created for the particular user; 

1237 

Dynamic interfaces are added to this list automatically whenever a user is connected and its username does not match any existing static entry (or in case the entry is active already, as there can not be two separate tunnel interfaces referenced by the same name); 

Dynamic interfaces appear when a user connects and disappear once the user disconnects, so it is impossible to reference the tunnel created for that use in router configuration (for example, in firewall), so if you need persistent rules for that user, create a static entry for him/her. Otherwise, it is safe to use a dynamic configuration. 

**==> picture [13 x 13] intentionally omitted <==**

in both cases PPP users must be configured properly - static entries do not replace PPP configuration.
