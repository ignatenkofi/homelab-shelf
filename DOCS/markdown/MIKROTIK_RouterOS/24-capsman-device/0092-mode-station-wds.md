## Mode station-wds 

This mode works only with RouterOS APs. As a result of negotiating connection, separate WDS interface is created on AP for given station. This interface can be thought of point-to-point connection between AP and given station - whatever is sent out WDS interface is delivered to station (and only to particular station) and whatever station sends to AP is received from WDS interface (and not subject to forwarding between AP clients), preserving L2 addresses. 

This mode is supported for all wireless protocols except when 802.11 protocol is used in connection to non-RouterOS device. Mode uses 4 address frame format when used with 802.11 protocol, for other protocols (such as nstreme or nv2), protocol internal means are used. 

This mode is safe to use for L2 bridging and gives most administrative control on AP by means of separate WDS interface, for example use of bridge firewall, RSTP for loop detection and avoidance, etc. 

With station-wds mode, it is not possible to connect to CAPsMAN controlled CAP.
