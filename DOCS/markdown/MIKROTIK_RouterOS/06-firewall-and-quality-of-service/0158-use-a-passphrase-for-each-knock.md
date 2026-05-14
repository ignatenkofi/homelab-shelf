## Use a passphrase for each knock 

You could go even further by sending a passphrase with each knock. 

**==> picture [13 x 13] intentionally omitted <==**

Warning 

Layer7 rules are very resource-intensive. Do not use it unless you know what you are doing. 

Then create a layer7 regex check that can be requested on the knock rule. 

/ip firewall layer7-protocol add name=pass regexp="^passphrase/$" 

/ip firewall filter 

add action=add-src-to-address-list address-list=888 address-list-timeout=30s chain=input dst-port=888 in-interface-list=WAN protocol=udp layer7protocol=pass 

**==> picture [13 x 13] intentionally omitted <==**

For additional security layer see the Bruteforse prevention article: Bruteforce prevention 

741
