## Sub-menu: `/iot lora netid` 

**==> picture [353 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>netids  (string; Default: ) Define the NetIDs<br>logging  (yes | no; Default: no) Enables additional logging for the filter feature.<br>name  (string; Default: ) Define the name for the ID.<br>type  (blacklist | whitelist; Default: whitelist) Define the type for the filter:<br>blacklist (if the range matches it blocks/drops packets)<br>whitelist (if the range matches it forwards the packets)<br>**----- End of picture text -----**<br>


To add a filter that allows a specific NetID (in this example, 000013 NetID, which belongs to TTN), use the command: 

```
/iot lora netid add name=allow_TTN netids=000013-000013 type=whitelist
```

To block all other NetIDs use " `type=blacklist` ": 

```
/iot lora netid add name=block_all netids=000000-ffffff type=blacklist
```

Disable LoRa interface: 

```
/iot/lora/disable [find where ]
```

Apply both ranges to the LoRa server you are using and enable the interface again: 

```
/iot/lora/servers/set netid=block_all,allow_TTN [find where address ~ "eu1.cloud.thethings.network"]
/iot/lora/enable [find where ]
```
