## LDP on Ipv6 and Dual-Stack links 

RouterOS implements RFC 7552 to support LDP on dual-stack links. 

Supported AFIs can be selected by LDP instance, as well as explicitly configured per LDP interface. 

```
/mpls ldp
add afi=ip,ipv6 lsr-id=111.111.111.1 preferred-afi=ipv6
/mpls ldp interface
add interface=ether2 afi=ip
add interface=ether3 afi=ipv6
```

850 

The example above enables LDP instance to use IPv4 and IPv6 address families and sets the preference to IPv6 with `preferred-afi` parameter. LDP interface configuration on the other hand explicitly sets that ether2 supports only IPv4 and ether3 supports only IPv6. 

The main question occurs how AFI is selected when there are a mix of different AFIs and what if one of the supported AFIs flaps. 

The logic behind sending hellos is as follows: 

if an interface has only one AFI: 

dual-stack element is not sent 

sends hello only if there is an IP address on the interface from the corresponding AFI. If an interface has both AFIs: 

dual-stack element is always sent and contains the value from preferred-afi 

sends hellos on each AFI if a corresponding address is present on the interface. 

From all received hellos peer determines which AFI to use for connection and for which AFIs to bind and send labels. For LDP to be able to use a specific AFI, receiving hello for that specific AFI is mandatory. Hello packet contains the transport address necessary for proper LDP operation. By comparing received AFI addresses, is determined active/passive role. 

The logic behind receiving and processing hellos is as follows: 

- if the LDP instance has only one AFI (it means that all interfaces can have only that specific AFI operational): drop hellos from not supported AFI 

   - ignore/forget the dual-stack element for the hello packet the role is determined only for this one specific AFI 

   - labels are sent only for this one specific AFI 

if the LDP instance has both AFIs (interfaces can have different combinations of supported AFIs): 

drop hellos from AFI that are not configured as supported on the interface. 

ignore/forget the dual-stack element (preference is not taken into account) for hello packets, if an interface has only one supported AFI. drop hello if received preference in dual-stack element does not match configured `preferred-afi` . 

If there are changes in hello packets, the existing session is terminated only in case if address family used by labels is changed, otherwise, the session is preserved. 

Dual-stack element in hello packets is set only if an interface is determined to be dual-stack compatible: 

Normally such an interface should be able to receive hellos from both AFIs, 

Before proceeding LDP should wait for hello from the preferred AFI. if hello is received only from one AFI: 

if hello from preferred AFI is not received then it is considered an error. otherwise, wait for missing hello for x seconds (x = 3 * hello-interval) 

if missing hello appears within a time interval consider peer to be dual-stack if missing hello did not appear, then consider peer to be single-stack 

if missing hello appeared after the time interval then restart the session. 

the dual-stack element indicates that LDP wants to distribute labels for both AFIs. 

In summary, the following combinations of AFIs and dual-stack element (ds6) are possible assuming that preferred-afi=ipv6: 

1.  ipv4 - wait X seconds, if no changes, then use the IPv4 LDP session and distribute IPv4 labels 

2.  ipv4+ds6 - wait for IPv6 hello, dual-stack element indicates that there should be IPv6 

3.  ipv6 - wait X seconds, if no changes, then use the IPv6 LDP session and distribute IPv6 labels 

4.  ipv6+ds6 - use IPv6 LDP session and distribute IPv6 labels 

5.  ipv4,ipv6 - use IPv6 LDP session and distribute IPv4 and IPv6 labels 

6.  ipv4,ipv6+ds6 - use IPv6 LDP session and distribute IPv4 and IPv6 labels
