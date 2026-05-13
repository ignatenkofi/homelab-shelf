## Stats 

Using " `/interface ethernet print stats` " command, it is possible to see a wide range of Ethernet-related statistics. The list of statistics can differ between RouterBoard devices due to different Ethernet drivers. The list below contains all available counters across all RouterBoard devices. Most of the Ethernet statistics can be remotely monitored using SNMP and MIKROTIK-MIB. 

**==> picture [506 x 203] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>driver-rx-byte  (integer) Total count of received bytes on device CPU<br>driver-rx-packet  (integer) Total count of received packets on device CPU<br>driver-tx-byte  (integer) Total count of transmitted bytes by device CPU<br>driver-tx-packet  (integer) Total count of transmitted packets by device CPU<br>fc-fec-block-corrected  (integer) Total count of FC-FEC corrected blocks. Applies only when fec74 mode is used.<br>fc-fec-block-uncorrected  (integ Total count of FC-FEC uncorrected blocks. Applies only when fec74 mode is used.<br>er)<br>fc-fec-rx-block  (integer) Total count of FC-FEC received blocks. Applies only when fec74 mode is used.<br>rs-fec-corrected  (integer) Total count of RS-FEC corrected codewords. Applies only when fec91 mode is used.<br>rs-fec-symbol-error  (integer) Total count of RS-FEC symbol errors. Applies only when fec91 mode is used.<br>**----- End of picture text -----**<br>


1307 

**==> picture [506 x 692] intentionally omitted <==**

**----- Start of picture text -----**<br>
rs-fec-uncorrected  (integer) Total count of RS-FEC uncorrected codewords. Applies only when fec91 mode is used.<br>rx-64  (integer) Total count of received 64 byte frames<br>rx-65-127  (integer) Total count of received 65 to 127 byte frames<br>rx-128-255  (integer) Total count of received 128 to 255 byte frames<br>rx-256-511  (integer) Total count of received 256 to 511 byte frames<br>rx-512-1023  (integer) Total count of received 512 to 1023 byte frames<br>rx-1024-1518  (integer) Total count of received 1024 to 1518 byte frames<br>rx-1519-max  (integer) Total count of received frames larger than 1519 bytes<br>rx-align-error  (integer) Total count of received align error events - packets where bits are not aligned along octet boundaries<br>rx-broadcast  (integer) Total count of received broadcast frames<br>rx-bytes  (integer) Total count of received bytes<br>rx-carrier-error  (integer) Total count of received frames with carrier sense error<br>rx-code-error  (integer) Total count of received frames with code error<br>rx-control  (integer) Total count of received control or pause frames<br>rx-error-events  (integer) Total count of received frames with the active error event<br>rx-fcs-error  (integer) Total count of received frames with incorrect checksum<br>rx-fragment  (integer) Total count of received fragmented frames (not related to IP fragmentation)<br>rx-ip-header-checksum-error  (i Total count of received frames with IP header checksum error<br>nteger)<br>rx-jabber  (integer) Total count of received jabbed packets - a packet that is transmitted longer than the maximum packet length<br>rx-length-error  (integer) Total count of received frames with frame length error<br>rx-multicast  (integer) Total count of received multicast frames<br>rx-overflow  (integer) Total count of received overflowed frames can be caused when device resources are insufficient to receive a<br>certain frame<br>rx-pause  (integer) Total count of received pause frames<br>rx-runt  (integer) Total count of received frames shorter than the minimum 64 bytes, is usually caused by collisions<br>rx-tcp-checksum-error  (integer) Total count of received frames with TCP header checksum error<br>rx-too-long  (integer) Total count of received frames that were larger than the maximum supported frame size by the network device, see<br>the max-l2mtu property<br>rx-too-short  (integer) Total count of the received frame shorter than the minimum 64 bytes<br>rx-udp-checksum-error  (integer) Total count of received frames with UDP header checksum error<br>rx-unicast  (integer) Total count of received unicast frames<br>rx-unknown-op  (integer) Total count of received frames with unknown Ethernet protocol<br>tx-64  (integer) Total count of transmitted 64 byte frames<br>tx-65-127  (integer) Total count of transmitted 65 to 127 byte frames<br>tx-128-255  (integer) Total count of transmitted 128 to 255 byte frames<br>tx-256-511  (integer) Total count of transmitted 256 to 511 byte frames<br>tx-512-1023  (integer) Total count of transmitted 512 to 1023 byte frames<br>**----- End of picture text -----**<br>


1308 

**==> picture [506 x 681] intentionally omitted <==**

**----- Start of picture text -----**<br>
tx-1024-1518  (integer) Total count of transmitted 1024 to 1518 byte frames<br>tx-1519-max  (integer) Total count of transmitted frames larger than 1519 bytes<br>tx-align-error  (integer) Total count of transmitted align error events - packets where bits are not aligned along octet boundaries<br>tx-broadcast  (integer) Total count of transmitted broadcast frames<br>tx-bytes  (integer) Total count of transmitted bytes<br>tx-collision  (integer) Total count of transmitted frames that made collisions<br>tx-control  (integer) Total count of transmitted control or pause frames<br>tx-deferred  (integer) Total count of transmitted frames that were delayed on its first transmit attempt due to already busy medium<br>tx-drop  (integer) Total count of transmitted frames that were dropped due to the already full output queue<br>tx-excessive-collision  (integer) Total count of transmitted frames that already made multiple collisions and never got successfully transmitted<br>tx-excessive-deferred  (integer) Total count of transmitted frames that were deferred for an excessive period of time due to an already busy medium<br>tx-fcs-error  (integer) Total count of transmitted frames with incorrect checksum<br>tx-fragment  (integer) Total count of transmitted fragmented frames (not related to IP fragmentation)<br>tx-carrier-sense-error  (integer) Total count of transmitted frames with carrier sense error<br>tx-late-collision  (integer) Total count of transmitted frames that made collision after being already halfway transmitted<br>tx-multicast  (integer) Total count of transmitted multicast frames<br>tx-multiple-collision  (integer) Total count of transmitted frames that made more than one collision and subsequently transmitted successfully<br>tx-overflow  (integer) Total count of transmitted overflowed frames<br>tx-pause  (integer) Total count of transmitted pause frames<br>tx-all-queue-drop-byte  (integer) Total count of transmitted bytes dropped by all output queues<br>tx-all-queue-drop-packet  (integ Total count of transmitted packets dropped by all output queues<br>er)<br>tx-queueX-byte  (integer) Total count of transmitted bytes on a certain queue, the X should be replaced with a queue number<br>tx-queueX-packet  (integer) Total count of transmitted frames on a certain queue, the X should be replaced with a queue number<br>tx-runt  (integer) Total count of transmitted frames shorter than the minimum 64 bytes, is usually caused by collisions<br>tx-too-short  (integer) Total count of transmitted frames shorter than the minimum 64 bytes<br>tx-rx-64  (integer) Total count of transmitted and received 64 byte frames<br>tx-rx-64-127  (integer) Total count of transmitted and received 64 to 127 byte frames<br>tx-rx-128-255  (integer) Total count of transmitted and received 128 to 255 byte frames<br>tx-rx-256-511  (integer) Total count of transmitted and received 256 to 511 byte frames<br>tx-rx-512-1023  (integer) Total count of transmitted and received 512 to 1023 byte frames<br>tx-rx-1024-max  (integer) Total count of transmitted and received frames larger than 1024 bytes<br>tx-single-collision  (integer) Total count of transmitted frames that made only a single collision and subsequently transmitted successfully<br>tx-too-long  (integer) Total count of transmitted packets that were larger than the maximum packet size<br>tx-underrun  (integer) Total count of underrun frames which can be caused when device resources are insufficient to transmit a certain<br>frame<br>tx-unicast  (integer) Total count of transmitted unicast frames<br>**----- End of picture text -----**<br>


1309 

For example, the output of Ethernet stats on the hAP ac2 device: 

```
[admin@MikroTik] > /interface ethernet print stats
                      name:           ether1 ether2         ether3        ether4 ether5
            driver-rx-byte:  182 334 805 898      0  5 836 927 820    24 895 692      0
          driver-rx-packet:    4 449 562 546      0  4 320 155 362       259 449      0
            driver-tx-byte:   15 881 099 971      0 70 502 669 211    60 498 056     53
          driver-tx-packet:       52 724 428      0     54 231 229       106 498      1
                  rx-bytes:  178 663 398 808      0  5 983 590 739 1 358 140 795      0
              rx-too-short:                0      0              0             0      0
                     rx-64:       12 749 144      0        362 459       125 917      0
                 rx-65-127:        9 612 406      0     20 366 513       292 189      0
                rx-128-255:        6 259 883      0      1 672 588       261 013      0
                rx-256-511:        2 950 578      0        211 380       278 147      0
               rx-512-1023:        3 992 258      0        185 666       163 241      0
              rx-1024-1518:      119 034 611      0      2 796 559       696 254      0
               rx-1519-max:                0      0              0             0      0
               rx-too-long:                0      0              0             0      0
              rx-broadcast:       12 025 189      0      1 006 377        64 178      0
                  rx-pause:                0      0              0             0      0
              rx-multicast:        4 687 869      0         36 188       220 136      0
              rx-fcs-error:                0      0              0             0      0
            rx-align-error:                0      0              0             0      0
               rx-fragment:                0      0              0             0      0
               rx-overflow:                0      0              0             0      0
                  tx-bytes:   16 098 535 973      0 72 066 425 886   225 001 772      0
                     tx-64:        1 063 375      0        924 855        37 877      0
                 tx-65-127:       26 924 514      0      2 442 200       959 209      0
                tx-128-255:       14 588 113      0        924 746       295 961      0
                tx-256-511:        1 323 733      0      1 036 515        33 252      0
               tx-512-1023:        1 287 464      0      2 281 554         3 625      0
              tx-1024-1518:        7 537 154      0     48 212 304        64 659      0
               tx-1519-max:                0      0              0             0      0
               tx-too-long:                0      0              0             0      0
              tx-broadcast:              590      0        145 800       823 038      0
                  tx-pause:                0      0              0             0      0
              tx-multicast:                0      0      1 039 243        41 716      0
               tx-underrun:                0      0              0             0      0
              tx-collision:                0      0              0             0      0
    tx-excessive-collision:                0      0              0             0      0
     tx-multiple-collision:                0      0              0             0      0
       tx-single-collision:                0      0              0             0      0
     tx-excessive-deferred:                0      0              0             0      0
               tx-deferred:                0      0              0             0      0
         tx-late-collision:                0      0              0             0      0
```

1310
