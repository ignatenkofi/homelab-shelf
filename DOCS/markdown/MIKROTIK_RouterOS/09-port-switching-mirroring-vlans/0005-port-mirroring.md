## Port Mirroring 

Port mirroring lets the switch to copy all traffic that is going in and out of one port ( `mirror-source` ) and send out these copied frames to some other port ( `mirror-target` ). This feature can be used to easily set up a 'tap' device that receives all traffic that goes in/out of some specific port. Note that `mirrorsource` and `mirror-target` ports have to belong to the same switch (see which port belongs to which switch in `/interface ethernet` menu). Also, mirror-target can have a special ' `cpu` ' value, which means that mirrored packets should be sent out to the switch chips CPU port. Port mirroring happens independently of switching groups that have or have not been set up. 

Sub-menu: `/interface ethernet switch` 

**==> picture [516 x 133] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mirror-source  (name |  Selects a single mirroring source port. Ingress and egress traffic will be sent to the  mirror-target  port. Note that  mirror-<br>none; Default:  none ) target  port has to belong to the same switch (see which port belongs to which switch in /interface ethernet  menu).<br>mirror-target  (name |  Selects a single mirroring target port. Mirrored packets from  mirror-source  and  mirror  (see the property in rule and host<br>none | cpu; Default:  none table) will be sent to the selected port.<br>)<br>mirror-egress-target  (na Selects a single mirroring egress target port, only available on  88E6393X ,  88E6191X  and  88E6190 switch chips. Mirrored<br>me | none; Default:  none packets from  mirror-egress  (see the property in port menu) will be sent to the selected port.<br>)<br>**----- End of picture text -----**<br>


Sub-menu: `/interface ethernet switch rule` 

Property Description 

482 

mirror (no | yes; Whether to send a packet copy to `mirror-target` port. Default: no ) mirror-ports (name; Selects multiple mirroring target ports, only available on 88E6393X switch chip. Matched packets in the ACL rule will be Default: ) copied and sent to selected ports. 

Sub-menu: `/interface ethernet switch host` 

**==> picture [516 x 189] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mirror  (no | yes;  Whether to send a frame copy to  mirror-target  port from a frame with a matching MAC destination address (matching<br>Default: no ) destination or source address for CRS3xx series switches)<br>Sub-menu: /interface ethernet switch port<br>Property Description<br>mirror-egress  (no | yes;  Whether to send egress packet copy to the  mirror-egress-target  port, only available on  88E6393X ,  88E6191X<br>Default:  no ) and  88E6190  switch chips.<br>mirror-ingress  (no | yes;  Whether to send ingress packet copy to the  mirror-ingress-target  port, only available on  88E6393X ,  88E6191X<br>Default:  no ) and  88E6190  switch chips.<br>mirror-ingress-target  (name |  Selects a single mirroring ingress target port, only available on   88E6393X ,  88E6191X  and  88E6190  switch chips.<br>none; Default:  none ) Mirrored packets from  mirror-ingress  will be sent to the selected port.<br>**----- End of picture text -----**<br>


Port mirroring configuration example: 

```
/interface ethernet switch
```

```
set switch1 mirror-source=ether2 mirror-target=ether3
```

**==> picture [13 x 13] intentionally omitted <==**

If you set mirror-source as an Ethernet port for a device with at least two switch chips and these mirror-source ports are in a single bridge while mirror-target for both switch chips are set to send the packets to the CPU, then this will result in a loop, which can make your device inaccessible.
