## Sub-menu: `/ip dhcp-server lease` 

DHCP server lease submenu is used to monitor and manage server leases. The issued leases are shown here as dynamic entries. You can also add static leases to issue a specific IP address to a particular client (identified by MAC address). 

Generally, the DHCP lease is allocated as follows: 

an unused lease is in the "waiting" state 

- if a client asks for an IP address, the server chooses one 

- if the client receives a statically assigned address, the lease becomes offered, and then bound with the respective lease time 

- if the client receives a dynamic address (taken from an IP address pool), the router sends a ping packet and waits for an answer for 0.5 seconds. During this time, the lease is marked testing 

895 

in the case where the address does not respond, the lease becomes offered and then bound with the respective lease time in other cases, the lease becomes busy for the lease time (there is a command to retest all busy addresses), and the client's request remains unanswered (the client will try again shortly) 

A client may free the leased address. The dynamic lease is removed, and the allocated address is returned to the address pool. But the static lease becomes busy until the client reacquires the address. 

**==> picture [13 x 13] intentionally omitted <==**

IP addresses assigned statically are not probed! 

**==> picture [501 x 555] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP; Default: 0.0.0.0 ) Specify IP address (or ip pool) for static lease. If set to 0.0.0.0 - a pool from the DHCP server will be used<br>address-list  (string; Default: none ) Address list to which address will be added if the lease is bound.<br>allow-dual-stack-queue  (yes | no;  Creates a single simple queue entry for both IPv4 and IPv6 addresses, and uses the MAC address and DUID<br>Default: yes ) for identification. Requires IPv6 DHCP Server to have this option enabled as well to work properly.<br>always-broadcast  (yes | no;  Changes whether to force broadcast DHCP replies:<br>Default:  no )<br>no - replies are sent based on the client's broadcast flag. If the server sends three consecutive offers, the<br>third and forth offer will be sent as a broadcast;<br>yes - replies are always broadcasted even when the client has not specified the broadcast flag.<br>block-access  (yes | no; Default: no Block access for this client<br>)<br>client-id  (string; Default: none ) If specified, must match the DHCP 'client identifier' option of the request<br>dhcp-option  (string; Default: none ) Add additional DHCP options from option list.<br>dhcp-option-set  (string; Default: n Add an additional set of DHCP options.<br>one )<br>insert-queue-before  (bottom |  Specify where to place dynamic simple queue entries for static DHCP leases with rate-limit parameter set.<br>first | name; Default: first )<br>lease-time  (time; Default: 0s ) Time that the client may use the address. If set to 0s lease will never expire.<br>mac-address  (MAC; Default: 00: If specified, must match the MAC address of the client<br>00:00:00:00:00 )<br>parent-queue  (string | none;  A dynamically created queue for this lease will be configured as a child queue of the specified parent queue.<br>Default:  none )<br>queue-type  (default, ethernet- Queue type that can be assigned to the specific lease<br>default, multi-queue-ethernet-<br>default, pcq-download-default,<br>synchronous-default, default-<br>small, hotspot-default, only-<br>hardware-queue, pcq-upload-<br>default, wireless-default)<br>rate-limit  (integer[/integer] [integer Adds a dynamic simple queue to limit IP's bandwidth to a specified rate. Requires the lease to be static. Format<br>[/integer] [integer[/integer] [integer is: rx-rate[/tx-rate] [rx-burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx-burst-time[/tx-burst-<br>[/integer]]]];; Default: ) time]]]]. All rates should be numbers with optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx-<br>rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst-threshold and tx-burst-time. If both rx-burst-<br>threshold and tx-burst-threshold are not specified (but burst-rate is specified), rx-rate and tx-rate is used as<br>burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default.<br>routes  ([dst-address/mask]  Routes that appear on the server when the client is connected. It is possible to specify multiple routes<br>[gateway] [distance]; Default:  none separated by commas. This setting will be ignored for OpenVPN.<br>)<br>**----- End of picture text -----**<br>


896 

server (string) Server name which serves this client use-src-mac (yes | no; Default: no ) When this option is set server uses the source MAC address instead of the received CHADDR to assign the address. status (waiting | testing | declined Shows the status of DHCP `lease` : | offered | bound | authorizing | conflict) waiting - waiting for static DHCP lease to get bound testing - checking for ARP conflicts declined - DHCP client replied with decline packet offered - server offered address to DHCP client, but did not yet receive DHCP request back bound - DHCP client accepted DHCP lease authorizing - communicating with RADIUS conflict - ARP conflict detected
