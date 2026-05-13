## Summary 

Internet Group Management Protocol (IGMP) proxy can implement multicast routing. It is forwarding IGMP frames and is commonly used when there is no need for a more advanced protocol like PIM. 

IGMP proxy features: 

The simplest way how to do multicast routing; 

Can be used in topologies where PIM-SM is not suitable for some reason; It takes slightly less resources than PIM-SM; Ease of configuration. 

On the other hand, IGMP proxy is not well suited for complicated multicast routing setups. Compared to PIM-based solutions, IGMP proxy does not support more than one upstream interface and routing loops are not detected or avoided. 

By default, IGMP proxy upstream interface will send IGMPv3 membership reports and it will detect what IGMP version the upstream device (e.g. multicast router) is using based on received queries. In case IGMPv1/v2 queries are received, the upstream port will fall back to the lower IGMP version. It will convert back to IGMPv3 when IGMPv1/v2 querier present timer (400s) expires. Downstream interfaces of IGMP proxy will only send IGMPv2 queries. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS v7 has IGMP proxy configuration available in the main system package. Older RouterOS versions need an additional multicast package installed in order to use IGMP proxy. See more details about Packages.
