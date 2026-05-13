## Or from WinBox: 

**==> picture [504 x 299] intentionally omitted <==**

Configuring IP Access 

17 

As MAC connection can sometimes be unreliable, our first step is to configure the router to enable IP connectivity: 

Create a bridge interface and assign bridge ports; Assign an IP address to the bridge interface; Configure a DHCP server. 

Setting up the bridge and assigning an IP address are straightforward processes: 

```
/interface bridge add name=bridge1
/interface bridge port add interface=ether2 bridge=bridge1
/ip address add address=192.168.88.1/24 interface=bridge1
```

If you prefer WinBox/WebFig as configuration tools: 

Open Bridge window, Bridge tab should be selected; Click on the  button + to open a new dialog box. You can either enter a custom bridge name or retain the default bridge1 , then click OK to proceed; Switch to the Ports tab and click on the  button + to open another dialog box; Select interface ether2 and bridge bridge1 form drop-down lists and click on the OK button to apply settings; You may close the bridge dialog. 

18 

**==> picture [353 x 240] intentionally omitted <==**

**==> picture [376 x 240] intentionally omitted <==**

Access the IP menu and navigate to the Addresses dialog; Select the  button + to open a new dialog box; Enter IP address 192.168.88.1/24 select interface bridge1 from the drop-down list; Click OK to confirm the settings. 

19 

**==> picture [451 x 264] intentionally omitted <==**

Next, proceed with setting up a DHCP server. To simplify and expedite this process, we'll execute the setup command. 

```
[admin@MikroTik] > ip dhcp-server/ setup [enter]
Select interface to run DHCP server on
```

```
dhcp server interface: bridge1 [enter]
Select network for DHCP addresses
```

```
dhcp address space: 192.168.88.0/24 [enter]
Select gateway for given network
```

```
gateway for dhcp network: 192.168.88.1 [enter]
Select pool of ip addresses given out by DHCP server
```

```
addresses to give out: 192.168.88.2-192.168.88.254 [enter]
Select DNS servers
```

```
dns servers: 192.168.88.1 [enter]
Select lease time
```

```
lease time: 1800 [enter]
```

Notice that most of the configuration options are automatically determined and you just simply need to hit the enter key. 

The setup tool is also accessible in WinBox/WebFig: 

Navigate to IP -> DHCP Server window, ensuring the DHCP tab is selected; Click on the DHCP Setup button to open a new dialog; Select the bridge1 as the DHCP Server Interface and click Next ; Follow the wizard to complete the setup. 

20 

**==> picture [451 x 233] intentionally omitted <==**

Following these steps, the connected PC should now obtain a dynamic IP address. You can then close Winbox and reconnect to the router using the IP address (192.168.88.1).
