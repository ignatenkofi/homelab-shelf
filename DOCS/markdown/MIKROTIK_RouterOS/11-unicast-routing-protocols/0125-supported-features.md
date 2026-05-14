## Supported features 

Different services can be placed in specific VRF on which the service is listening for incoming or creating outgoing connections. By default, all services are using the `main` table, but it can be changed with a separate `vrf` parameter or by specifying the VRF name separated by "@" at the end of the IP address. 

1036 

Below is the list of supported services. 

**==> picture [516 x 633] intentionally omitted <==**

**----- Start of picture text -----**<br>
Feature Support Comment<br>BGP +<br>/routing bgp template<br>add name=bgp-template1 vrf=vrf1<br>/routing bgp vpls<br>add name=bgp-vpls1 site-id=10 vrf=vrf1<br>/routing bgp vpn<br>add label-allocation-policy=per-vrf vrf=vrf1<br>E-mail +<br>/tool e-mail<br>set address=192.168.88.1 vrf=vrf1<br>IP Services + VRF is supported for  telnet ,  www ,  ssh ,  www-ssl ,  api ,  winbox ,  api-ssl  services. The  ftp  service does<br>not support changing the VRF.<br>/ip service<br>set telnet vrf=vrf1<br>L2TP Client +<br>/interface l2tp-client<br>add connect-to=192.168.88.1@vrf1 name=l2tp-out1 user=l2tp-client<br>MPLS +<br>/mpls ldp<br>add vrf=vrf1<br>Netwatch +<br>/tool netwatch<br>add host=192.168.88.1@vrf1<br>NTP +<br>/system ntp client<br>set vrf=vrf1<br>/system ntp server<br>set vrf=vrf1<br>OSPF +<br>/routing ospf instance<br>add disabled=no name=ospf-instance-1 vrf=vrf1<br>ping +<br>/ping 192.168.88.1 vrf=vrf1<br>RADIUS +<br>/radius add address=192.168.88.1@vrf1<br>/radius incoming set vrf=vrf1<br>**----- End of picture text -----**<br>

1037 

**==> picture [516 x 689] intentionally omitted <==**

**----- Start of picture text -----**<br>
RIP +<br>/routing rip instance<br>add name=rip-instance-1 vrf=vrf1<br>RPKI +<br>/routing rpki<br>add vrf=vrf1<br>SNMP +<br>/snmp<br>set vrf=vrf1<br>EoIP +<br>/interface eoip<br>add remote-address=192.168.1.1@vrf1<br>IPIP +<br>/interface ipip<br>add remote-address=192.168.1.1@vrf1<br>GRE +<br>/interface gre<br>add remote-address=192.168.1.1@vrf1<br>SSTP-client +<br>/interface sstp-client<br>add connect-to=192.168.1.1@vrf1<br>OVPN- +<br>/interface ovpn-client<br>client<br>add connect-to=192.168.1.1@vrf1<br>L2TP-ether +<br>/interface l2tp-ether<br>add connect-to=192.168.2.2@vrf<br>VXLAN +<br>/interface vxlan<br>add vni=10 vtep-vrf=vrf1<br>Fetch +<br>/tool/fetch<br>address=10.155.28.236@vrf1 mode=ftp src-path=my_file.pcap user=admin password=""<br>DNS +<br>/ip dns set vrf=vrf1<br>Starting from<br>RouterOS v7.15<br>DHCP- +<br>/ip dhcp-relay set dhcp-server-vrf=vrf1<br>Relay<br>Starting from<br>RouterOS v7.15<br>If dhcp-client is in vrf - special parameter in "ip dhcp-relay" configuration is not needed<br>**----- End of picture text -----**<br>

1038 

Remote + `/system logging action` logging `add name=remote1 remote=192.168.1.1 target=remote vrf=vrf1` Starting from RouterOS v7.19
