## Nstreme 

Sub-menu: `/interface wireless nstreme` 

This menu allows to switch a wireless card to the nstreme mode. In this case the card will work only with nstreme clients. 

**==> picture [504 x 320] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string;  Short description of an entry<br>Default: )<br>disable-csma  (yes | no;  Disable CSMA/CA when polling is used (better performance)<br>Default: no )<br>enable-nstreme  (yes | no Whether to switch the card into the nstreme mode<br>; Default: no )<br>enable-polling  (yes | no;  Whether to use polling for clients<br>Default: yes )<br>framer-limit  (integer  Maximal frame size<br>[100..4000]; Default: 3200<br>)<br>framer-policy  (best-fit |  The method how to combine frames. A number of frames may be combined into a bigger one to reduce the amount of<br>dynamic-size | exact- protocol overhead (and thus increase speed). The card is not waiting for frames, but in case a number of packets are<br>size | none; Default: none queued for transmitting, they can be combined. There are several methods of framing:<br>)<br>none  - do nothing special, do not combine packets (framing is disabled)<br>best-fit  - put as many packets as possible in one frame, until the framer-limit limit is met, but do not fragment<br>packets<br>exact-size  - put as many packets as possible in one frame, until the framer-limit limit is met, even if fragmentation<br>will be needed (best performance)<br>dynamic-size  - choose the best frame size dynamically<br>name  (string) Name of an interface, to which setting will be applied. Read only.<br>**----- End of picture text -----**<br>

Note: The settings here (except for enabling nstreme) are relevant only on Access Point, they are ignored for client devices! The client automatically adapts to the AP settings. 

WDS for Nstreme protocol requires using station-wds mode on one of the peers. Configurations with WDS between AP modes (bridge and ap-bridge) will not work. 

1408
