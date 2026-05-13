## New features 

A New Kernel is implemented in RouterOSv7, which leads to performance changes due to route cache, as well some tasks might require higher CPU and RAM usage for different processes. 

completely new NTP client and server implementation 

merged individual packages, only bundle and a few extra packages remain (dropped support for LCD and KVM packages) new Command Line Interface (CLI) style (RouterOS v6 commands are still supported) support for Let's Encrypt certificate generation support for REST API support for UEFI boot mode on x86 CHR FastPath support for "vmxnet3" and "virtio-net" drivers support for "Cake" and "FQ_Codel" type queues support for IPv6 NAT 

support for Layer 3 hardware acceleration on all CRS3xx devices support for MBIM driver with basic functionality support for all modems with MBIM mode support for MLAG on CRS3xx devices 

support for VRRP grouping and connection tracking data synchronization between nodes support for Virtual eXtensible Local Area Network (VXLAN) support for L2TPv3 

support for OpenVPN UDP transport protocol support for WireGuard 

support for hardware offloaded VLAN filtering on RTL8367 (RB4011, RB100AHx4) and MT7621 (hEX, hEX S, RBM33G) switches support for ZeroTier on ARM and ARM64 devices 

completely new alternative wireless package "wifiwave2" with 802.11ac Wave2, WPA3, and 802.11w management frame protection support (requires ARM CPU and 256MB RAM) 

support for hardware offloaded VLAN filtering on RTL8367 (RB4011, RB100AHx4) and MT7621 (hEX, hEX S, RBM33G) switches support CPU frequency scaling for x86 devices
