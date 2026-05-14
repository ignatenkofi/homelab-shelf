## What ports does ZeroTier use? 

It listens on three 3 UDP ports: 

9993 - The default 

A random, high numbered port derived from your ZeroTier address 

A random, high numbered port for use with UPnP/NAT-PMP mappings 

That means your peers could be listening on any port. To talk with them directly, you need to be able to send them to any port.
