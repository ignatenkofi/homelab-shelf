## How WMM works 

WMM works by dividing traffic into 4 access categories: background, best effort, video, voice. QoS policy (different handling of access categories) is applied on transmitted packets, therefore the transmitting device is treating different packets differently, e.g. AP does not have control over how clients are transmitting packets, and clients do not have control over how AP transmits packets. 

Mikrotik AP and client classify packets based on the priority assigned to them, according to the table (as per WMM specification): 1,2 - background 0,3 - best effort 4,5 - video 6,7 - voice. 

To be able to use multiple WMM access categories, not just the best effort where all packets with default priority 0 go, priority must be set for those packets. By default, all packets (incoming and locally generated) inside the router have priority 0. 

The "Better" access category for a packet does not necessarily mean that it will be sent over the air before all other packets with the "worse" access category. WMM works by executing the DCF method for medium access with different settings for each access category (EDCF), which means that the "better" access category has a higher probability of getting access to medium - WMM enabled station can be considered to be 4 stations, one per access category, and the ones with "better" access category use settings that make them more likely to get chance to transmit (by using shorter backoff timeouts) when all are contending for medium. Details can be studied in 802.11e and WMM specifications. 

**==> picture [13 x 13] intentionally omitted <==**

WMM support can be enabled using the `wmm-support` setting. It only applies to bands B and G. Other bands will have it enabled regardless of this setting
