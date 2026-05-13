## Scanner 

PPPoE Scanner allows scanning all active PPPoE servers in the layer2 broadcast domain. Command to run scanner is as follows: 

```
/interface pppoe-client scan [interface]
```

Available read only properties: 

1252 

**==> picture [201 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>service  (string) Service name configured on server<br>mac-address  (MAC) Mac address of detected server<br>ac-name  (string) name of the Access Concentrator<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

For Windows, some connection instructions may use the form where the "phone number", such as "MikroTik_AC\mt1", is specified to indicate that "MikroTik_AC" is the access concentrator name and "mt1" is the service name. 

**==> picture [13 x 13] intentionally omitted <==**

Specifying MRRU means enabling MP (Multilink PPP) over a single link. This protocol is used to split big packets into smaller ones. Under Windows, it can be enabled in the Networking tab, Settings button, "Negotiate multi-link for single link connections". MRRU is hardcoded to 1614 on Windows. This setting is useful to overcome PathMTU discovery failures. The MP setting should be enabled on both peers.
