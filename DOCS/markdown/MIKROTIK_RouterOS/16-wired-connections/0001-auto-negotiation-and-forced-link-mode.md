## Auto-negotiation and Forced Link Mode 

Auto-negotiation is a communication method and a set of steps employed by Ethernet devices connected via twisted pair cables. It enables these devices to agree on key transmission settings, including speed, duplex mode, and flow control. During this process, the connected devices initially exchange information about their capabilities concerning these settings. Afterward, they mutually select the best possible transmission mode that both devices can support effectively. 

However, in RouterOS auto-negotiation behaves differently on SFP/QSFP ports compared to standard RJ45 Ethernet ports. In the case of SFP/QSFP interfaces, the negotiation process does not involve the exchange of advertised capabilities (no advertisement bits are shared). Instead, RouterOS attempts to bring up the link using the highest supported mode on each side. For a successful connection, both devices must advertise the same highest common mode. 

For example: 

Device A advertises `10G-baseCR` and `25G-baseCR` . Device B advertises only `10G-baseCR` . 

In this case, the link will not establish, because Device A prioritizes 25G while Device B advertise only 10G. 

To ensure a successful link: 

Both Device A and Device B must have the same highest advertised mode. So if Device B advertises `25G-baseCR` , and Device A also includes `25G-baseCR` as its highest advertisement, the link will be established. 

In summary, when configuring SFP/QSFP interfaces, make sure that the highest supported mode matches on both ends to ensure proper link establishment.
