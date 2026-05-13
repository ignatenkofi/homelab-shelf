## Known limitations 

Here is a list of known limitations by popular client software IKEv2 implementations. 

- Windows will always ignore networks received by split-include and request policy with destination 0.0.0.0/0 (TSr). When IPsec-SA is generated, Windows requests DHCP option 249 to which RouterOS will respond with configured split-include networks automatically. 

Both Apple macOS and iOS will only accept the first split-include network. 

Both Apple macOS and iOS will use the DNS servers from system-dns and static-dns parameters only when 0.0.0.0/0 split-include is used. 

- While some implementations can make use of different PFS group for phase 2, it is advised to use pfs-group=none under proposals to avoid any compatibility issues. 

1215
