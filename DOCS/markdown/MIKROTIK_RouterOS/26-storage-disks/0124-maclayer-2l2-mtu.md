## MAC/Layer-2/L2 MTU 

L2MTU indicates the maximum size of the frame without the MAC header that can be sent by this interface. 

In RouterOS L2MTU values can be seen in the "/interface" menu. L2MTU support is added for all Routerboard related Ethernet interfaces, VLANs, Bridge, VPLS, and wireless interfaces. Some of them support the configuration of the L2MTU value. All other Ethernet interfaces might indicate L2MTU only if the chipset is the same as Routerboard Ethernets. 

This will allow users to check if the desired setup is possible. Users will be able to utilize additional bytes for VLAN and MPLS tags, or simply increase interface MTU to get rid of some unnecessary fragmentation. 

This table shows max-l2mtu supported by Mikrotik RouterBoards (available in the "/interface print" menu as the value of the read-only "max-l2mtu" option): 

**==> picture [516 x 559] intentionally omitted <==**

**----- Start of picture text -----**<br>
Model name MTU description<br>RB SXT series, RB LHG, RB LDF, PL6411-2nD, PL7411-2nD, RB711 series, wAP R-2nD, RB912R- ether1:2028<br>2nD-LTm (LtAP mini), RB Metal series, RB SXT Lite series, RB Groove series, Cube Lite60, LHG<br>Lite60<br>RB SXT G series, RB DynaDish, wAP ac, RB QRT series, RB711G series, RB911G, RB912UAG ether1:4076<br>RB OmniTik series, RB750, RB750UP, RB751U-2HnD, RB951-2n ether1:4076; ether2-ether5:2028<br>RB OmniTik ac series, RB750GL, RB750Gr2 ether1-ether5:4074<br>RB mAP, RB mAP lite, RB cAP, RB wAP ether1-ether2:2028<br>RB750r2, RB750P-PBr2, RB750UPr2, RB941-2nD, RB951Ui/RB952Ui series ether1-ether5:2028<br>RB750Gr3 ether1-ether5:2026<br>RB751G-2HnD, RB951G-2HnD ether1-ether5:4074<br>RB962UiGS, RB960PGS ether1-ether5:4074; sfp1:4076<br>RB LHGG series ether1:9214<br>LHG XL 52 ac ether1:9214; sfp1:9214<br>RB1100Hx2, RB1100AHx2 ether1-ether10:9498; ether11:9500; ether12-<br>ether13:9116<br>RB4011iGS+ series ether1-ether10:9578; sfp-sfpplus1:9982<br>CCR1009 series ether1-ether4:10224; ether5-ether8:10226; sfp1:<br>10226; sfp-sfpplus1:10226<br>CCR1016 series ether1-ether12:10226; sfp1-sfp12:10226; sfp-<br>sfpplus1:10226<br>CCR1036 series ether1-ether12:10226; sfp1-sfp4:10226; sfp-<br>sfpplus1-sfp-sfpplus2:10226<br>CCR1072 series ether1:9116; sfp-sfpplus1-sfp-sfpplus8:10226<br>CCR2004-1G-12S+2XS ether1:9586; sfp-sfpplus1-sfp-sfpplus12:9578;<br>sfp28-1 - sfp28-2:9578<br>CCR2004-16G-2S+ ether1-ether16:9582; sfp-sfpplus1-sfp-sfpplus2:<br>9586<br>CCR2116-12G-4S+ ether1-ether12:9570; ether13:9586; sfp-sfpplus1-<br>sfp-sfpplus4:9570<br>CCR2216-1G-12XS-2XQ ether1:9586; sfp28-1 - sfp28-12:9570; qsfp28-1-<br>1 - qsfp28-2-4:9570<br>CRS109-8G-1S ether1-ether8:4064; sfp1:4064<br>CRS125-24G-1S ether1-ether24:4064; sfp1:4064<br>**----- End of picture text -----**<br>


1712 

**==> picture [516 x 681] intentionally omitted <==**

**----- Start of picture text -----**<br>
CRS112-8G-4S, CRS112-8P-4S ether1-ether8:9204; sfp9-sfp12:9204<br>CRS106-1C-5S sfp1-sfp5:9204; combo1:9204<br>CRS210-8G-2S+ ether1-ether8:9204; sfp-sfpplus1:9204; sfpplus2:<br>9204<br>CRS212-1G-10S-1S+ ether1:9204; sfp1-sfp10:9204; sfpplus1:9204<br>CRS226-24G-2S+ ether1-ether24:9204; sfp-sfpplus1:9204;<br>sfpplus2:9204<br>CRS326-24G-2S+, CSS326-24G-2S+ ether1-ether24:10218; sfp-sfpplus1:10218;<br>sfpplus2:10218<br>CRS317-1G-16S+ ether1:10218; sfp-sfpplus1-sfp-sfpplus16:10218<br>CRS328-24P-4S+ ether1-ether24:10218; sfp-sfpplus1-sfp-sfpplus4:<br>10218<br>CRS328-4C-20S-4S+ combo1-combo4:10218; sfp1-sfp20:10218; sfp-<br>sfpplus1-sfp-sfpplus4:10218<br>CRS305-1G-4S+ ether1:10218; sfp-sfpplus1-sfp-sfpplus4:10218<br>CRS304-4XG ether1-ether4:10218; ether5:9676<br>CRS309-1G-8S+ ether1:10218; sfp-sfpplus1-sfp-sfpplus8:10218<br>netFiber 9/IN (CRS310-1G-5S-4S+) sfp1-sfp5:10218; sfp-sfpplus1-sfp-sfpplus4:10218<br>CRS310-8G+2S+IN ether1-ether8:10218; sfp-sfpplus1-sfp-sfpplus2:<br>10218<br>CRS312-4C+8XG combo1-combo4:10218; ether1-ether8:10218;<br>ether9:2028<br>netPower 15FR (CRS318-1Fi-15Fr-2S) ether1-ether16:10218; sfp1-sfp2:10218<br>netPower 16P (CRS318-16P-2S+) ether1-ether16:10218; sfp-sfpplus1-sfp-sfpplus2:<br>10218<br>CRS326-4C+20G+2Q+ combo1-combo4:10218; ether1-ether20:10218;<br>qsfpplus1-1-qsfpplus2-4:10218; ether21:2028<br>CRS326-24S+2Q+ sfp-sfpplus1-sfp-sfpplus24:10218; qsfpplus1-1-<br>qsfpplus2-4:10218; ether1:2028<br>CRS354-48G-4S+2Q+, CRS354-48P-4S+2Q+ sfp-sfpplus1-sfp-sfpplus4:10218; qsfpplus1-1-<br>qsfpplus2-4:10218; ether1-ether48:10218;<br>ether49:2028<br>CRS418-8P-8G-2S+RM ether1-ether16:10218; ether17:9018; sfp-<br>sfpplus1-sfp-sfpplus2: 10218<br>CRS504-4XQ-IN ether1:2028; qsfp28-1-1 - qsfp28-4-4:10218<br>CRS510-8XS-2XQ-IN ether1:2028; sfp28-1 - sfp28-8:10218; qsfp28-1-<br>1 - qsfp28-2-4:10218<br>CRS518-16XS-2XQ ether1:2028; sfp28-1 - sfp28-16:10218; qsfp28-1-<br>1 - qsfp28-2-4:10218<br>CSS610-8G-2S+, CSS610-8P-2S+ ether1-ether8:10218; sfp-sfpplus1-sfp-sfpplus2:<br>10218<br>D52G-5HacD2HnD (hAP ac²) ether1-ether5:9124<br>C52iG-5HaxD2HaxD (hAP ax2) ether1-ether5:9214<br>**----- End of picture text -----**<br>


1713 

**==> picture [516 x 514] intentionally omitted <==**

**----- Start of picture text -----**<br>
C53UiG+5HPaxD2HPaxD (hAP ax3) ether1-ether5:9214<br>L41G-2axD (hAP ax lite) ether1-ether4:2026<br>cAP ac ether1-ether2:9124<br>GPEN21 ether1-ether2:10222; sfp1: 10222<br>wAP60G, LHG60G ether1:9124<br>RB260GS series, CSS106-5G-1S, CSS106-1G-4P-1S ether1-ether5:9198; sfp1:9198<br>RBFTC11 ether1:4046; sfp1:4046<br>RBM33G ether1-ether3:2026<br>RBM11G ether1:2026<br>RB760iGS ether1-ether5:2026; sfp1:2026<br>E50UG ether1:2048; ether2-ether5:2026<br>RB411 series ether1:1526<br>RB433 series, RB450, RB493 series ether1:1526; ether2-ether3:1522<br>RB450Gx4 ether1-ether5:9214<br>RB411GL ether1:1520<br>RB433GL, RB435G , RB450G, RB493G ether1-ether3:1520<br>RB800 ether1-ether2:9500; ether3:9116<br>RB850Gx2 ether1-ether5:1580<br>RB921UAGS, RB922UAGS ether1:4076; sfp1:4076<br>D23UGS-5HPacD2HnD (NetMetal ac²) ether1:9214 ; sfp1:9214<br>RB953GS ether1-ether2:4074; sfp1:4074; sfp2:4076<br>RB2011 series ether1-ether5:4074; ether6-ether10:2028; sfp1:<br>4074<br>RB3011 series ether1-ether5:8156; ether6-ether10:8156; sfp1:<br>8158<br>RB5009 series ether1-ether8: 9796; sfp-sfpplus1: 9796<br>L009 series ether1: 8158; ether2-ether8: 8154; sfp1: 8154<br>RB44Ge ether1-ether4:9116<br>**----- End of picture text -----**<br>


All wireless interfaces in RouterOS (including Nstreme2) support 2290 byte L2MTU. 

**==> picture [13 x 13] intentionally omitted <==**

L2MTU configuration changes evoke all interface reloads (link down/link up) due to necessary internal processes. 

It is recommended to configure L2MTU with caution by keeping in mind that it can cause short interruption with connected devices.
