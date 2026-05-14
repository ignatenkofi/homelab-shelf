## Join EUI 

The gateway will forward to the server every single LoRaWAN payload it receives. That includes neighboring LoRaWAN node's payloads as well. It might not be ideal to forward everything, as, for example, it can increase the data amount used (and directly impact ISP plan cost). 

The Join EUI menu allows you to specify a balcklisted or a whitelisted range of JOIN EUI's that the gateway should forward (if it is "whitelisted") or should block (if it is "blacklisted"). After adding the range, make sure to apply it to the server settings. 

The filter's work using the following pricniple: 

1) By default, everything is allowed (unless whitelist/blacklist filters are added); 

2) If "blacklist" filter range is added , and then a JOIN EUI packet that matches the blacklisted range appears nearby → it is droped ; 

3) If "whitelist" filter range is added, it has prioirty over the "blacklisted" filters . Meaning that if both "blacklist" and "whitelist" match the same JOIN EUI, "whitelist" takes prioirty and the packet is forwarded. 

You can find the Join EUI used by your node with the help of RouterOS GUI. Go to the "LoRa" section and to the "Traffic" sub-menu (which is only available using the graphical interface). After you power your LoRaWAN node, the node should send a "Join-request" packet. Double-click on it to inspect it: 

1601 

**==> picture [505 x 184] intentionally omitted <==**

Sub-menu: `/iot lora joineui` 

**==> picture [353 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>joineui  (string; Default: ) Define a range of Join EUI's.<br>logging  (yes | no; Default: no) Enables additional logging for the filter feature.<br>name  (string; Default: ) Define the name for the range.<br>type  (blacklist | whitelist; Default: whitelist) Define the type for the filter:<br>blacklist (if the range matches it blocks/drops packets)<br>whitelist (if the range matches it forwards the packets)<br>**----- End of picture text -----**<br>

An example of Join EUI would look like this E0 E1 E2 01 02 03 04 05 . It consists of 8 octets in HEX format. 

To add a range that blocks everything , add a filter like this: 

```
/iot lora joineui add name=block_all joineuis=0000000000000000-ffffffffffffffff type=blacklist logging=yes
```

To allow a specific single Join EUI, add a filter like this: 

```
/iot lora joineui add name=allow_my_node joineuis=E0E1E20102030405-E0E1E20102030405 type=whitelist logging=yes
```
