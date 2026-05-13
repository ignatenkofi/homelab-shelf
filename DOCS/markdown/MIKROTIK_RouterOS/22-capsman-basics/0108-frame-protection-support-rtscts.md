## Frame protection support (RTS/CTS) 

802.11 standard provides means to protect the transmission against other device transmission by using RTS/CTS protocol. Frame protection helps to fight "hidden node" problem. There are several types of protection: 

- RTS/CTS based protection - device willing to send frame at first sends RequestToSend frame and waits for ClearToSend frame from intended destination. By "seeing" RTS or CTS frame 802.11 compliant devices know that somebody is about to transmit and therefore do not initiate transmission themselves 

- "CTS to self" based protection - device willing to send frame sends CTS frame "to itself". As in RTS/CTS protocol every 802.11 compliant device receiving this frame know not to transmit. "CTS to self" based protection has less overhead, but it must be taken into account that this only protects against devices receiving CTS frame (e.g. if there are 2 "hidden" stations, there is no use for them to use "CTS to self" protection, because they will not be able to receive CTS sent by other station - in this case stations must use RTS/CTS so that other station knows not to transmit by seeing CTS transmitted by AP). 

Protection mode is controlled by hw-protection-mode setting of wireless interface. Possible values: none - for no protection (default), rts-cts for RTS/CTS based protection or cts-to-self for "CTS to self" based protection. 

Frame size threshold at which protection should be used is controlled by hw-protection-threshold setting of wireless interface. 

For example, to enable "CTS-to-self" based frame protection on AP for all frames, not depending on size, use command: 

```
[admin@MikroTik] /interface wireless> set 0 hw-protection-mode=cts-to-self hw-protection-threshold=0
```

To enable RTS/CTS based protection on client use command: 

```
[admin@MikroTik] /interface wireless> set 0 hw-protection-mode=rts-cts hw-protection-threshold=0
```
