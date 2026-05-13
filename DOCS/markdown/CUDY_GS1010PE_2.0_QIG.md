---
title: CUDY GS1010PE 2.0 Quick Installation Guide
source: CUDY_GS1010PE_2.0_QIG.pdf
format: OCR (Tesseract --oem 1 --psm 6, English-only, 150 dpi)
note: Original is a visual diagram-heavy guide. OCR captures labels and spec table.
---

## Page 1

Hardware Connection LEDs & Button DIP Explanation
Power Socket Note: FS1010P for illustration
1. PoE ports can connect to non-PoE devices as well, but a
will only transmit data. jth ith
2, Here we take FS1010P for example. Your actual product li
; may differ, An
Powered Device (PD) i
(fe S| Oke ce $a
: ees) a © ‘ a a Pe 2 are
' a) PS : 2 Oo ho he ' ower On Power on poece cece eee ede,
‘VoIP Phone IP Camera Dual Band AP IPcamera | | NVR | | Router | Off Total PoE budget < 90% ' Watchdog 1
Gh Be PoE MaX Flash___90% = Total PoE budget = 95% ' Extend (1-8) |
{ | On Total PoE budget =95% ! VLAN (18) |
+} Off No link: ' |
Link/Data Flash Exchanging data ' 1
SES CES SO 9 107 On Link but no activity ' |
Beer Off No providing PoE power toe eee eee eee
cudy erry Pot ‘On Providing PoE Power
PAU aed oe oa Press to switch LED indication VLAN: Disabled by default. Switch ON to have the
GIRS TF between Link/Data and PoE. specified downlink ports isolated from each other, and
ee = ee PoE LED Button GS1010PE/GS1010PS2 LED 1-8 & only transmit data with the rest ports.
~ . > (For GS1010PE/ GS1005PTS1 LED 1-4 : green for Extend: Disabled by default. Switch ON to enable the
Gsto10Ps2y Link/Data, amber for PoE status, specified ports to achieve @ maximum transmission
FS1010P for illustration Gs1005PTS1) ‘GS1O10PE/GS1010PS2 LED 9-10: distance of 250meters, with speed capped at 10 Mbps.
green for 1000Mbps Link/Data, Watchdog: Disabled by default. Switch ON to enable
‘amber for 10/100Mbps Link/Data. PoE Watchdog function.

## Page 2

@ Specifications
eee J
Model FSI010P/FS1010PG/GS1005PTS1/ For GS1010P. + Cat. Se or higher cable: cuey
GS1010P/GS1010PE/GS1010PS2 10 * 10/100/1000Mbps R45 ports, 100 meters at Gigabit
Standard “IEEE 802.31 10BASE-T Auto-Negotiation MDVMIDX (for FSIO1OPG/GS100SPTS1/ Quick Installation Guide
+ IEEE 802.3u 10OBASE-TX PoE ports: Port 1-8 GSI010P/GSIO10PE/GS1010PS2)
- IEEE 802.3ab 1000BASE-T For GSI010PE/GS1010PS2: Power Supply + Input: 100-240V 50/60Hz 2.58 Unmanaged PoE Switch
(for FS1010PG/GS1005PTS1/ 10 * 10/100/1000Mbps R45 ports, + Total Power Supply: 120W Max Model: FS1010P | FS1010PG | GS1005PTS1 | GS1010P |
GS1O10P/GS1010PE/GS1010PS2) Auto-Negotiation MDVMIDX Installation Desktop GS1010PE | Gst010PS2
+ IEEE 802.32 1000BASE-X PoE ports: Port 1-8 + Rackmount via Brackets
(for GS1005PTS/GS1010PS2) 2* SFP ports (for GS1010PS2 only) (Brackets not included in the box)
+ IEEE 802.3x Flow Control For GSi005PTSI: OT
IEEE 802.3affat PoE 5 * 10/100/1000Mbps RJAS ports, ;
interface For FSTO10P: Auto-Negotiation MDVMIDX EU declaration of conformity
10* 10/00Mbps RJ4S ports, PoE ports: Port 1-4 cssonlalregurements and othe felevatprovilons of crectes
Auto-Negotiation MDIIMIDX 1* SFP port 2014/30/EU, 2014/35/EU, 2015/863/EU and 2011/65/EU,
PoE ports: Port 1-8 Network Media Cat.3 or higher cable Atplinww-cudycomon omy may be found at
‘ForFsioopG: ss—s—~S (Cable) 100 meters at 10 Mbps
8 * 10/100Mbps RJ45 ports, + Cat.5 or higher cable oo
2* 10/100/1000Mbps RU45 ports 100 meters at 100 Mbps © Rots | NEED TECH HELP? ooure |
Auto-Negotiation MDI/MIDX + Cat.Se or higher cable: mice merme, ' '
PoE ports: Port 1-8 250 meters at 10 Mbps CEXHIFER ABA x : @ wowcuay.com support@cudy.com ‘
