## Q. How the route selection is done? 

A. The route with the best metric is always selected after the discovery process. There is also a configuration option to periodically reoptimize already known routes. 

Route metric is calculated as the sum of individual link metrics. 

Link metric is calculated in the same way as for (R)STP protocols: 

For Ethernet links the metric is configured statically (same as for OSPF, for example). 

For WDS links the metric is updated dynamically depending on actual link bandwidth, which in turn is influenced by wireless signal strength, and the selected data transfer rate. 

Currently, the protocol does not take into account the amount of bandwidth being used on a link, but that might be also used in the future.
