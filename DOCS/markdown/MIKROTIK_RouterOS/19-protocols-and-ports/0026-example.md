## Example 

Let us assume we want to bridge two networks: 'Station' and 'AP'. By using EoIP setup can be made so that Station and AP LANs are in the same Layer2 broadcast domain. 

Consider the following setup: 

1180 

**==> picture [505 x 271] intentionally omitted <==**

As you know wireless stations cannot be bridged, to overcome this limitation (not involving WDS) we will create an EoIP tunnel over the wireless link and bridge it with interfaces connected to local networks. 

We will not cover wireless configuration in this example, let's assume that the wireless link is already established. 

At first, we create an EoIP tunnel on our AP: 

```
/interface eoip add name="eoip-remote" tunnel-id=0 remote-address=10.0.0.2 disabled=no
```
