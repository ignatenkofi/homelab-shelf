## Overview 

Package: `wifi-qcom` 

**==> picture [13 x 13] intentionally omitted <==**

This guide is meant for 802.11 AX devices running **`wifi-qcom`** package/drivers. 

Wi-Fi devices can play different roles. The most common device, almost every household has, is called a Wi-Fi router. A typical Wi-Fi router, usually, has a WAN port (for ISP connection), LAN ports (for local PCs, wired printers etc) and a WLAN network (Wi-Fi network). Routers are also called "gateways" and "firewalls", because they act as a "doorway" for your local network clients into the internet (those devices "hide" LAN connected clients behind them and protect them). 

**==> picture [13 x 13] intentionally omitted <==**

Router → is a firewall/gateway device, which has an ISP cable connected to it, is firewall protected and has DHCP-server functionality enabled (which provides IP address to the connected, both wirelessly and via a wire, LAN clients). 

Another role for a Wi-Fi device, is called an "access point" or an "AP" for short. Those devices, typically, are connected to the main "router/gateway /firewall" via an ethernet connection (to the router's LAN port), they are not firewall protected, and do not have DHCP-server functionality enabled (they do not provide IP addresses). APs have all their Wi-Fi and LAN interfaces/ports bridged, and thus, APs "take" IP address from the router connection, and "pass" them down to AP-connected clients (acting as a "layer2" bridge/switch). 

**==> picture [13 x 13] intentionally omitted <==**

Access point → are "bridge" devices, which are connected to the router using an Ethernet cable, they are not firewall protected, and they have D HCP-server functionality disabled (they "bridge" DHCP requests from the router to AP's clients). 

In other words, a Wi-Fi router is an AP with additional functionality . 

APs (devices that broadcast Wi-Fi networks) run on 2.4 and/or 5 GHz frequency. 5 GHz networks enable a much better throughput, but with reduced range. 2.4 GHz networks ensure a better coverage, but with less throughput. 

Indoor APs are, usually, equipped with omnidirectional antennas (which allow broadcasting the signal in a "donut" shape around the AP, 360°). For indoor and short distance outdoor installations, it is a perfect antenna to use. Using a simple home AP with omnidirection antennas, you can achieve a distance of up to ±100 meters in an "ideal" interference-free line of sight setup. Which is reduced much further inside buildings. Concrete, pipes, metal, water...and all kinds of other different materials affect WiFi indoors. Some items can absorb, some deflect, some diffract and some can scatter the signal. 

With that in mind, it is not always possible to cover the required range with a single AP/router, and additional APs need to be installed. Meaning, that if you have a problematic spot in your home, where Wi-Fi signal is poor or non-existent, consider installing a new AP closer to the problematic spot. 

**==> picture [13 x 13] intentionally omitted <==**

This guide is meant for a "basic" or a so-called "standalone" AP setup . You can use it, if you have a 3d-party vendor Wi-Fi router (non-MikroTik), if you have a legacy Wi-Fi 5 (AC) MikroTik router, or if your previous setup did not have any Wi-Fi APs at all. 

For setups that consist of **`wifi-qcom`** package/driver APs, use CAPSMAN management , as it enables 802.11 r/k/v roaming standards, which smoothen client's transition. 

1377 

**==> picture [13 x 13] intentionally omitted <==**

Non-802.11 r/k/v roaming! 

In "standalone" AP setups, if you simply copy SSID name from your router settings and configure the AP to broadcast the same SSID name →  roaming will be purely client dependent. 

Roaming is when your client device transitions between different APs which use the same WiFi name. There are standards that can help "accelerate" and "smoothen" the transition (like 802.11 r/k/v) but, unfortunately, they can not be used in this setup (because there is no "manager" device) and so, the decision, "to roam" or "not to roam" is up to the client fully. Different vendors have different algorithms implemented that decide how and when your client device should switch. 

Keep that in mind! Some devices, that have a good algorithm (decision-making), will roam properly, while others might stick to a poor signal (furthest) AP. 

Most, if not all, of our MikroTik Wi-Fi devices come pre-configured in the "router" role. This guide will show you how to turn them into standalone AP role devices (layer2 bridged APs).
