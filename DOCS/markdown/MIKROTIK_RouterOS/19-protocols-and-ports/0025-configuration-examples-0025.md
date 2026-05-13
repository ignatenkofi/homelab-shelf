## Configuration Examples 

Parameter tunnel-id is a method of identifying a tunnel. It must be unique for each EoIP tunnel. 

**==> picture [13 x 13] intentionally omitted <==**

EoIP tunnel adds at least 42 byte overhead (8byte GRE + 14 byte Ethernet + 20 byte IP). MTU should be set to 1500 to eliminate packet fragmentation inside the tunnel (that allows transparent bridging of Ethernet-like networks so that it would be possible to transport full-sized Ethernet frame over the tunnel). 

When bridging EoIP tunnels, it is highly recommended to set unique MAC addresses for each tunnel for the bridge algorithms to work correctly. For EoIP interfaces you can use MAC addresses that are in the range from 00:00:5E:80:00:00 - 00:00:5E:FF:FF:FF , which IANA has reserved for such cases. Alternatively, you can set the second bit of the first byte to modify the auto-assigned address into a 'locally administered address', assigned by the network administrator, and thus use any MAC address, you just need to ensure they are unique between the hosts connected to one bridge.
