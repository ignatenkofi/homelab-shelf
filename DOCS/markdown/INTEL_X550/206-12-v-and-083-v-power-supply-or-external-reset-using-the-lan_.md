## 1.2 V, and 0.83 V power supply, or external reset using the LAN_PWR_GOOD pad.

Table 12-18. POR Configuration
          Parameter                   LAN_PWR_GOOD

          Internal POR                      High

         External POR                   Reset Signal

The timing between the power-up sequence and the different reset signals when using the internal
power indication is described in Section 12.3.8.

12.4.4.6.1               External Power-On Reset

The X550 may use the LAN_PWR_GOOD pad as power-on indication.Table 12-19 lists the timing for the
external power-on signal.

Table 12-19. External Reset Specification
 Symbol                   Title                              Description                  Min   Max   Units

Tlpgw        LAN_PWR_GOOD Minimum Width        Minimum width for LAN_PWR_GOOD.             5    N/A    s

                                               Hold time following power-up (power
Tlpg         LAN_PWR_GOOD High Hold                                                       40    80     ms
                                               supplies in acceptable operating range).

Figure 12-7. External Reset Timing Diagram

### 12.4.5 PCIe Interface AC/DC Specification

The X550 PCIe interface supports the electrical specifications defined in:
 • PCI Express* 2.0 Card Electromechanical Specification.
 • PCI Express* 3.0 Base Specification, Chapter 4.

### 12.4.6 Network Interface AC/DC Specification

The AC/DC specification of the network interface is according to the 10GBASE-T, 1000BASE-T, and
100BASE-TX Standards (802.3, 802.3an, and 802.3u, respectively), and the and NBASE-T specification.
The 100BASE-T parameters are also described in standard ANSI X3.263.

333369-009                                                                                                  1131
                                  Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                           Electrical/Mechanical Specification
