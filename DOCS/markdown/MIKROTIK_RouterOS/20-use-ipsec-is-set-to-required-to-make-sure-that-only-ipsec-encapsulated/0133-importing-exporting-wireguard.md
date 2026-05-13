## Importing, Exporting Wireguard 

Configuration can be done in various ways, here is simple wg import file example: export 

**==> picture [13 x 13] intentionally omitted <==**

Minimum parameters must be specified for importing on the client device by QR-code/file. 

Example: 

```
interface: wireguard1
public-key: v/oIzPyFm1FPHrqhytZgsKjU7mUToQHLrW+Tb5e601M=
private-key: KMwxqe/iXAU8Jn9dd1o5pPdHep2blGxNWm9I944/I24=
allowed-address: 192.168.88.3/24
client-address: 192.168.88.3/32
client-endpoint: example.com:13231
```

1270 

**==> picture [13 x 13] intentionally omitted <==**

When using interface/wireguard/wg-import file=, you may get Could not parse error, if Wireguard import file starts with #, use it clean as per example: `[Interface] Address =192.168.88.3/24 ListenPort = 13533 PrivateKey = UBLqJEFZZf9wszZSUF2BPWa9dsMX99RbEcxlNfxWffk=` 

**==> picture [13 x 13] intentionally omitted <==**

Starting from 7.19_ab41, config-string parameter has been added, for example using this cli command you can import your configuration: 

```
/interface wireguard/wg-import config-string="
[Interface]
Address =192.168.88.3/24
ListenPort = 13533
PrivateKey = UBLqJEFZZf9wszZSUF2BPWa9dsMX99RbEcxlNfxWffk=
[Peer]
PublicKey = EoF7HlFu3fbOnuYbyGqLMJkPZgQk9n3WwONZuJZ6qWc=
Endpoint = 199.168.100.10:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25"
```
