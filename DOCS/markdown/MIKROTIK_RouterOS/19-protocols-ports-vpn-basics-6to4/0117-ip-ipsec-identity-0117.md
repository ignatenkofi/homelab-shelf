## `/ip ipsec identity` 

```
add auth-method=digital-signature certificate=server1 generate-policy=port-strict mode-config=ike2-conf
peer=ike2 policy-template-group=ike2-policies
```

**==> picture [13 x 13] intentionally omitted <==**

If the peer's ID (ID_i) is not matching with the certificate it sends, the identity lookup will fail. See remote-id  the in identities section. 

For example, we want to assign a different mode config for user "A", who uses certificate "rw-client1" to authenticate itself to the server. First of all, make sure a new mode config is created and ready to be applied for the specific user.
