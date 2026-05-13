## Introduction 

Network load balancing is the ability to balance traffic across two or more links without using dynamic routing protocols. 

There are two type of balancing methods: 

per-packet - each packet of a single stream can be forwarded over different links. This method will work reliably especially on TCP and secure connections only when you are able to control both balancing endpoints. 

per-connection - all packets of the same connection (stream) is always sent over one link. This method is mandatory in setups where only one end of the balancing is under our control, for example, home router with multiple WAN connections. 

**==> picture [516 x 146] intentionally omitted <==**

**----- Start of picture text -----**<br>
Method Per-connection Per-packet<br>Nth Yes Yes<br>Firewall Mangle PCC (Per Connection  Yes No<br>Classifier)<br>Other matchers Yes Yes<br>ECMP (Equal Cost Multi-Path) Yes No<br>Bonding No Yes<br>OSPF Yes No<br>BGP Yes No<br>**----- End of picture text -----**<br>
