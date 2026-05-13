## SYN Flood 

An SYN flood is a form of DoS attack in which an attacker sends a succession of SYN requests to a target's system in an attempt to consume enough server resources to make the system unresponsive to legitimate traffic. Fortunately, in RouterOS we have a specific feature for such an attack: 

```
/ip/settings/set tcp-syncookies=yes
```

The feature works by sending back ACK packets that contain a little cryptographic hash, which the responding client will echo back with as part of its SYNACK packet. If the kernel doesn't see this "cookie" in the reply packet, it will assume the connection is bogus and drop it.
