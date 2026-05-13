## General Properties 

Sub-menu: `/system ptp` 

**==> picture [516 x 185] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>port Sub-menu used for adding, removing, or viewing assigned ports.<br>status Sub-menu that shows PTP ports, their state, and delay on slave ports.<br>comment  (string; Default: ) Short description of the PTP profile.<br>name ( string; Default: ) Name of the PTP profile.<br>domain  (integer [0..255]; Default:  auto Identifier used to separate different PTP instances.<br>)<br>delay-mode (auto | e2e | p2p;<br>Default:  auto ) auto - selects the delay mode automatically depending on the profile being used.<br>e2e - utilizes the delay request-response mechanism.<br>ptp - utilizes the peer delay mechanism.<br>**----- End of picture text -----**<br>


1160 

**==> picture [516 x 345] intentionally omitted <==**

**----- Start of picture text -----**<br>
priority1  (integer [0..255]; auto; Defau Parameter which takes part in the election of a grandmaster clock.<br>lt:  auto )<br>priority2  (integer [0..255]; auto; Defau Parameter which takes part in the election of a backup grandmaster clock.<br>lt:  auto )<br>profile  (802.1as; aes67; g8275.1;  Each profile comes with its own predefined auto values for PTP operating parameters and options:<br>smpte; default; Default:  default )<br>802.1as is an adaptation of PTP for use with Audio Video Bridging and Time-Sensitive Networking. Default(<br>auto) values: priority1=246, priority2=248, transport=l2-non-forwardable, delay-mode=p2p.<br>aes67 profile is for high-performance audio-over-IP interoperability. Default(auto) values: priority1=128,<br>priority2=128, domain=0, transport=ipv4, delay-mode=e2e.<br>g8275.1 profile is for frequency and phase synchronization in a fully PTP-aware network. Default(auto)<br>values: priority1=128, priority2=128, domain=24, transport=l2-non-forwardable, delay-mode=e2e.<br>smpte profile is for the synchronization of audio/video equipment in a professional broadcast environment. D<br>efault(auto) values: priority1=128, priority2=128, domain=127, transport=ipv4, delay-mode=e2e.<br>default profile, PTPv2 default configuration, allows for more configuration options than other profiles. Default<br>(auto) values: priority1=128, priority2=128, domain=0, transport=ipv4, delay-mode=e2e.<br>transport  (auto; ipv4; l2-forwardable;  Transport protocol to be used:<br>l2-non-forwardable; Default:  auto )<br>auto - automatically selects the transport mode based on the PTP profile in use.<br>ipv4 - uses the IPv4 multicast addresses 224.0.1.129 for PTP primary messages and 224.0.0.107 for PTP<br>peer delay messages.<br>l2-forwardable - uses the multicast MAC address  01-1B-19-00-00-00 , which is being forwarded through<br>PTP-unaware network equipment.<br>l2-non-forwardable - uses the multicast MAC address  01-80-C2-00-00-0E , ensuring that PTP messages<br>are not forwarded through PTP-unaware network equipment.<br>**----- End of picture text -----**<br>
