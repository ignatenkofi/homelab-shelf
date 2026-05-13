## RouterOS Server 

```
/ip ipsec key qkd
```

```
set address=10.13.2.9:8020 cache-size=1 certificate=sae-server key-size=32 \
   kme-id=server-kme-id peer-sae-id=client-sae-id
```

```
/ip ipsec profile add name=qkd-profile ppk=qkd
```

- `/ip ipsec proposal add name=qkd-proposal auth-algorithms=sha256 enc-algorithms=aes-256-gcm pfs-group=modp2048` 

> `/ip ipsec peer add address=10.20.1.2 exchange-mode=ike2 name=peer-client profile=qkd-profile proposal-check=obey /ip ipsec identity add peer=peer-client profile=qkd-profile` 

> `/ip ipsec policy add src-address=10.1.0.0/24 dst-address=10.2.0.0/24 peer=peer-client proposal=qkd-proposal tunnel=yes`
