## Introduction 

There are several types of switch chips on Routerboards and they have different sets of features. Most of them (from now on "Other") have only the basic "Port Switching" feature, but there are a few with more features: 

**==> picture [516 x 145] intentionally omitted <==**

**----- Start of picture text -----**<br>
Feature QCA8337 Atheros8327 Atheros8316 Atheros8227 Atheros7240 IPQ- ICPlus175D MT7621,  EN7523 RTL8367 88E6393X 88E6191X,<br>PPE MT7531 88E6190<br>Port  yes yes yes yes yes yes yes yes yes yes yes yes<br>Switching<br>Port  yes yes yes yes yes no yes yes yes yes yes yes<br>Mirroring<br>TX limit  [1] yes yes yes yes yes no no yes yes yes yes yes<br>RX limit  [1] yes yes no no no no no yes yes yes yes yes<br>Host table 2048 entries 2048 entries 2048 entries 1024 entries 2048 entries 2048  2048 entries  [2] 2048 entries 1024 entries 2048 entries 16k entries 16k entries<br>entries<br>Vlan table 4096 entries 4096 entries 4096 entries 4096 entries 16 entries no no 4096 entries  [3] 4096  4096 entries  [3] 4096 entries  [3] 4096 entries  [3]<br>entries  [3]<br>Rule table 92 rules 92 rules 32 rules no no no no no no no 256 no<br>**----- End of picture text -----**<br>

Notes 

1.  For QCA8337, Atheros8327, Atheros8316, Atheros8227, and Atheros7240 the Tx/Rx rate limits can be changed with `bandwidth` property on `"/i nterface ethernet"` menu, see more details in the Ethernet manual. For RTL8367, 88E6393X, 88E6191X, 88E6190, MT7621, MT7531 and EN7523 Tx/Rx rate limit can be changed with `egress-rate` and `ingress-rate` properties on " `/interface ethernet switch port` " menu. 

2.  MAC addresses are learned up to the specified number, but the content of a switch host table is not available in RouterOS and static host configuration is not supported. 

3.  Bridge HW vlan-filtering was added in the RouterOS 7.1 for RTL8367, MT7621, MT7531, EN7523. The switch does not support other `ethertype` 0x88a8 or 0x9100 (only 0x8100 is supported) and no `tag-stacking` . Using these features will disable HW offload. 

**==> picture [13 x 13] intentionally omitted <==**

Cloud Router Switch (CRS) series devices have highly advanced switch chips built-in, they support a wide variety of features. For more details about switch chip capabilities on CRS1xx/CRS2xx series devices check the CRS1xx/CRS2xx series switches manual, for CRS3xx series devices check the CRS3xx, CRS5xx series switches, and CCR2116, CCR2216 routers manual. 

479 

**==> picture [516 x 673] intentionally omitted <==**

**----- Start of picture text -----**<br>
RouterBoard Switch-chip description<br>C52iG-5HaxD2HaxD-TC (hAP ax2), C53UiG+5HPaxD2HPaxD (hAP ax3), Chateau ax series IPQ-PPE (ether1-ether5)<br>cAPGi-5HaxD2HaxD (cAP ax) IPQ-PPE (ether1-ether2)<br>L009 series 88E6190 (ether2-ether8, sfp1)<br>RB5009 series 88E6393X (ether1-ether8, sfp-<br>sfpplus1)<br>CCR2004-16G-2S+ 88E6191X (ether1-ether8); 88E6191X<br>(ether9-ether16);<br>RB4011iGS+ RTL8367 (ether1-ether5); RTL8367<br>(ether6-ether10);<br>RB1100AHx4 RTL8367 (ether1-ether5); RTL8367<br>(ether6-ether10); RTL8367 (ether11-<br>ether13)<br>L41G-2axD (hAP ax lite) MT7531 (ether1-ether4)<br>RB750Gr3 (hEX), RB760iGS (hEX S) MT7621 (ether1-ether5)<br>E50UG (hEX Refresh) EN7523 (ether2-ether5)<br>RBM33G MT7621 (ether1-ether3)<br>RB3011 series QCA8337 (ether1-ether5); QCA8337<br>(ether6-ether10)<br>RB OmniTik ac series QCA8337 (ether1-ether5)<br>RBwsAP-5Hac2nD (wsAP ac lite) Atheros8227 (ether1-ether3)<br>RB941-2nD (hAP lite) Atheros8227 (ether1-ether4)<br>RB951Ui-2nD (hAP); RB952Ui-5ac2nD (hAP ac lite); RB750r2 (hEX lite); RB750UPr2 (hEX PoE lite); RB750P- Atheros8227 (ether1-ether5)<br>PBr2 (PowerBox); RB750P r2; RBOmniTikU-5HnDr2 (OmniTIK 5); RBOmniTikUPA-5HnDr2 (OmniTIK 5 PoE)<br>RB750Gr2 (hEX); RB962UiGS-5HacT2HnT (hAP ac); RB960PGS (hEX PoE); RB960PGS-PB (PowerBox Pro) QCA8337 (ether1-ether5)<br>RB953GS Atheros8327 (ether1-ether3+sfp1)<br>RB850Gx2 Atheros8327 (ether1-ether5) with<br>ether1 optional<br>RB2011 series Atheros8327 (ether1-ether5+sfp1);<br>Atheros8227 (ether6-ether10)<br>RB750GL; RB751G-2HnD; RB951G-2HnD; RBD52G-5HacD2HnD (hAP ac²), RBD53iG-5HacD2HnD (hAP  Atheros8327 (ether1-ether5)<br>ac³), RBD53GR-5HacD2HnD&R11e-LTE6 (hAP ac³ LTE6 kit), RBD53G-5HacD2HnD-TC&EG12-EA (Chateau<br>LTE12)<br>RBcAPGi-5acD2nD (cAP ac), RBwAPGR-5HacD2HnD (wAP R ac and wAP ac LTE series), RBwAPG- Atheros8327 (ether1-ether2)<br>5HacD2HnD (wAP ac), RBD25G-5HPacQD2HPnD (Audience), RBD25GR-5HPacQD2HPnD&R11e-LTE6<br>(Audience LTE6 kit),<br>RBD22UGS-5HPacD2HnD (mANTBox 52 15s) Atheros8327 (ether1-sfp1)<br>RB1100AH Atheros8327 (ether1-ether5);<br>Atheros8327 (ether6-ether10)<br>RB1100AHx2 Atheros8327 (ether1-ether5);<br>Atheros8327 (ether6-ether10)<br>CCR1009-8G-1S-1S+; CCR1009-8G-1S Atheros8327 (ether1-ether4)<br>**----- End of picture text -----**<br>

480 

**==> picture [516 x 441] intentionally omitted <==**

**----- Start of picture text -----**<br>
RB493G Atheros8316 (ether1+ether6-ether9);<br>Atheros8316 (ether2-ether5)<br>RB435G Atheros8316 (ether1-ether3) with<br>ether1 optional<br>RB450G Atheros8316 (ether1-ether5) with<br>ether1 optional<br>RB450Gx4 Atheros8327 (ether1-ether5)<br>RB433GL Atheros8327 (ether1-ether3)<br>RB750G Atheros8316 (ether1-ether5)<br>RB1200 Atheros8316 (ether1-ether5)<br>RB1100 Atheros8316 (ether1-ether5);<br>Atheros8316 (ether6-ether10)<br>DISC Lite5 Atheros8227 (ether1)<br>RBmAP2nD Atheros8227 (ether1-ether2)<br>RBmAP2n Atheros7240 (ether1-ether2)<br>RB750 Atheros7240 (ether2-ether5)<br>RB750UP Atheros7240 (ether2-ether5)<br>RB751U-2HnD Atheros7240 (ether2-ether5)<br>RB951-2n Atheros7240 (ether2-ether5)<br>RB951Ui-2HnD Atheros8227 (ether1-ether5)<br>RB433 series ICPlus175D (ether2-ether3); older<br>models had ICPlus175C<br>RB450 ICPlus175D (ether2-ether5); older<br>models had ICPlus175C<br>RB493 series ICPlus178C (ether2-ether9)<br>RB816 ICPlus178C (ether1-ether16)<br>**----- End of picture text -----**<br>

The command-line configuration is under the switch menu. This menu contains a list of all switch chips present in the system and some sub-menus as well. 

```
[admin@MikroTik] > /interface ethernet switch print
Flags: I - invalid
```

```
 #   NAME         TYPE             MIRROR-SOURCE       MIRROR-TARGET       SWITCH-ALL-PORTS
 0   switch1      Atheros-8327     none                none
 1   switch2      Atheros-8227     none                none
```

Depending on the switch type there can be different configuration capabilities available.
