## Link Monitoring 

It is easy to notice that with the configuration above as soon as any individual link fails, the bonding interface throughput collapses. That's because no link monitoring is performed, consequently, the bonding driver is unaware of problems with the underlying links. Enabling link monitoring is a must in most bonding configurations. To enable ARP link monitoring, do the following:
