## Security multi-passphrase properties 

```
/interface/wifi/security/multi-passphrase/
```

`multi-passphrase` allows the use of PPSK - private pre-shared keys. Added in 7.17beta1. 

It can be used by creating an access list entry and setting `multi-passphrase-group` name, or by assigning the group to a security profile that the interface uses. 

The total limit of supported passphrases is 10000, the limit is shared between all interfaces. When the interface has an associated multi-passphrase group, upon being enabled it will start caching all passphrases from the specified group, while caching is taking place, the authentication will be slower. Once caching is completed there will be no perceptible added delay due to the use of multi-passphrase group. 

If an access-list is used to apply `multi-passphrase-group` , the caching will start upon the first match for the group, and will continue until a match for the passphrase is found. 

If there are thousands of entries for possible passphrases under a single group - it might take a few minutes for caching to complete, depending on device configuration and model. 

**==> picture [13 x 13] intentionally omitted <==**

multi-passphrase is not supported for the WPA3-PSK authentication type. 

**==> picture [516 x 253] intentionally omitted <==**

**----- Start of picture text -----**<br>
group  (string) assigning the group to a security profile or an access list, will enable use of all passphrases defined under it<br>passphrase  (string  The passphrase to use for PSK authentication types. Multiple users can use the same passphrase.<br>of up to 63<br>characters) Not compatible with WPA3-PSK.<br>vlan-id  (integer 0.. vlan-id that will be assigned to clients using this passphrase<br>4095; Default: )<br>Only supported on wifi-qcom interfaces, if wifi-qcom-ac AP has a client that uses a passphrase that has vlan-id<br>associated with it, the client will not be able to join.<br>expires  (date and  The expiration date and time for passphrase specified in this entry, doesn't affect the whole group. Once the date is reached,<br>time; "YYYY-MM- existing clients using this passphrase will be disconnected, and new clients will not be able to connect using it. If not set,<br>DD HH:SS" passphrase can be used indefinetly.<br>isolation  (yes | no;  Determines whether the client device using this passphrase is isolated from other clients on AP.<br>Default:  no ) Traffic from an isolated client will not be forwarded to other clients and unicast traffic from a non-isolated client will not be<br>forwarded to an isolated one.<br>disabled  (yes | no;<br>Default:  no )<br>**----- End of picture text -----**<br>
