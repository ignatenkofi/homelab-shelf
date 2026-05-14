## Other properties 

name (Text) : Unique queue identifier that can be used as parent option value for other queues both - limit both download and upload traffic 

upload - limit only traffic to the target 

download - limit only traffic from the target 

- time (TIME-TIME,sun,mon,tue,wed,thu,fri,sat - TIME is local time, all day names are optional; default: not set) : allow to specify time when particular queue will be active. Router must have correct time settings. 

- dst-address (IP address/netmask) : allows to select only specific stream (from target address to this destination address) for limitation explain what is target and what is dst and what is upload and what not 

- packet-marks (Comma separated list of packet mark names) : allows to use marked packets from /ip firewall mangle . Take look at the RouterOS p acket flow diagram. It is necessary to mark packets before the simple queues (before global-in HTB queue) or else target's download limitation will not work. The only mangle chain before global-in is prerouting.
