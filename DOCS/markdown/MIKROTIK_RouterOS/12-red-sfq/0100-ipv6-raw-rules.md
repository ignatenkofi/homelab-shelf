## IPv6 RAW Rules 

Raw IPv6 rules will perform the following actions: 

738 

add disabled accept rule - can be used to quickly disable RAW filtering without disabling all RAW rules; 

- drop packets that use bogon IPs; 

drop from invalid SRC and DST IPs; 

drop globally unroutable IPs coming from WAN; 

- drop bad ICMP; 

- accept everything else coming from WAN and LAN; 

drop everything else, to make sure that any newly added interface (like PPPoE connection to service provider) is protected against accidental misconfiguration.
