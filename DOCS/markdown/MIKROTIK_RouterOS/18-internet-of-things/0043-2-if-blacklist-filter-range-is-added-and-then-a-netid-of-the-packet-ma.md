## 2) If "blacklist" filter range is added , and then a NetID of the packet matches the blacklisted range → it is droped ; 

3) If "whitelist" filter range is added, it has prioirty over the "blacklisted" filters . Meaning that if both "blacklist" and "whitelist" match the same NetID,  "whitelist" takes prioirty and the packet is forwarded. 

NetIDs define the ranges of Device Addresses (DevAddr) that were assigned to different operators/servers by the LoRaWAN Alliance. A list with most ranges can be found in the TTN guide. 

DevAddr is assigned to the LoRaWAN node by the LoRaWAN server after the communication with the server takes place. For example, TTN will assign your node an address from within the range 26000000 - 27FFFFFF. You can find it under the LoRaWAN server dashboard or using RouterOS GUI, under the "Traffic" sub-menu (after "join-request" and "join-accept" communication takes place) in the Dev Addr column/field. 

Let's say TTN assigned 26 1B D8 D1 Dev Addr to your node. Based on the TTN guide, it falls under the 26000000 - 27FFFFFF DevAddr range and it belongs to the 000013 NetID .
