## Network ID 

1602 

The gateway will forward to the server every single LoRaWAN payload it receives. That includes neighboring LoRaWAN node's payloads as well. It might not be ideal to forward everything, as, for example, it can increase the data amount used (and directly impact ISP plan cost). 

The NetID menu allows you to specify a balcklisted or a whitelisted range of NetIDs that the gateway should forward (if it is "whitelisted") or should block (if it is "blacklisted"). After adding the list, make sure to apply it to the server settings. 

The filter's work using the following pricniple: 

1) By default, everything is allowed (unless whitelist/blacklist filters are added);
