## `/ip ipsec policy` 

```
add src-address=10.1.202.0/24 src-port=any dst-address=10.1.101.0/24 dst-port=any tunnel=yes action=encrypt
proposal=ike1-site2 peer=ike1-site2
```
