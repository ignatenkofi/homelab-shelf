## Disable LoRa interface: 

```
/iot/lora/disable [find where ]
```

Apply both ranges to the LoRa server you are using and enable the interface again: 

```
/iot/lora/servers/set joineui=block_all,allow_my_node [find where address ~ "eu1.cloud.thethings.network"]
/iot/lora/enable [find where ]
```

As a result, we will only allow "JOIN EUI= E0 E1 E2 01 02 03 04 05 " node payloads to be forwraded, while every single possible other JOIN EUI will be dropped by the blacklist rule.
