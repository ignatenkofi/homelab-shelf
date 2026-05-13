## Stats 

To view matching statistics by firewall rules, run `/ip firewall filter print stats` command or `/ipv6 firewall filter print stats` for IPv6 firewall. 

**==> picture [253 x 62] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bytes  (integer) The total amount of bytes matched by the rule<br>packets  (integer) The total amount of packets matched by the rule<br>**----- End of picture text -----**<br>


656 

```
[admin@MikroTik] > ip firewall filter print stats
Flags: X - disabled, I - invalid, D - dynamic
 #    CHAIN
            ACTION                            BYTES         PACKETS
 0  D ;;; special dummy rule to show fasttrack counters
      forward
            passthrough              50 507 925 242      50 048 246
 1    ;;; defconf: drop invalid
      forward
            drop                            432 270           9 719
 2    ;;; defconf: drop invalid
      input
            drop                            125 943           2 434
 3    input
            accept                   20 090 211 549      20 009 864
 4    ;;; defconf: accept ICMP
      input
            accept                          634 926           7 648
 5    ;;; defconf: drop all not coming from LAN
      input
            drop                          4 288 079          83 428
 6    ;;; defconf: accept in ipsec policy
      forward
            accept                                0               0
7    ;;; defconf: accept out ipsec policy
      forward
            accept                                0               0
8    ;;; defconf: fasttrack
      forward
            fasttrack-connection     28 505 528 775      31 504 682
9    ;;; defconf: accept established,related, untracked
      forward
            accept                   28 505 528 775      31 504 682
10    ;;; defconf: drop all from WAN not DSTNATed
      forward
            drop                                  0               0
```

Statistics parameters can be reset by following commands: 

**==> picture [286 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Description<br>reset-counters  (id) Reset statistics counters for specific firewall rule or list of rules.<br>reset-counters-all Reset statistics counters for all firewall rules in the table.<br>**----- End of picture text -----**<br>
