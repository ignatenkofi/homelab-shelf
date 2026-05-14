## 4.1 Power Up

### 4.1.1 Power-Up Sequence

Figure 4-1 shows the X550’s power-up sequence from power ramp up until it is ready to accept host
commands.

                                  V cc pow er on (80% )

                              Stra ppin g p ins a re latch ed

                           PH Y P LL s stabilize (m ax 1 6 ms)

                    W ait for internal P owe r O n Reset d e-a ssertion
                             (~35 m s after pow er sta bilize s)

                                   H W Au to -Lo ad 1:
                                M NG E na, W ake up E na

                                          M NG /
                                                          No                         P C Ie* R eset      No
                                         W akeup
                                                                                     de-asserte d
                                          E na ?
                                               Y es                                          Y es
                         HW A uto -L oad 2: M AC , P HY , N C-S I,            W ait for P CIe * P LL sta ble
                            Co nfigure M N G and W a ke up

                                                                             HW A uto-Loa d 3 : Init P CIe,
                     M an age ability & W a keu p En able d (Dr sta te)   M AC & PH Y if n o MN G / W akeu p

                                                                                       D 0u state

Figure 4-1.    X550 Power-Up Sequence

333369-009                                                                                                     137
                                       Did this document help answer your questions?

                                                                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                                                                                         Initialization

### 4.1.2 Power-Up Timing Diagram

                              Power

                Base 50 / 25 MHz

                     Supplies good                        8

       LAN_POWER_GOOD pin                               Trspor
                                                1

                      Internal POR                  2     Tbgg + 2 x Tcal_pll + 2 x Tpll + Tclkdiv + Tefuse

  Bgap_good+Pll_cal+ fuses+pll lock

      Power On Reset (to mac and phy)
                                                              3

      Lan_power_good (internal in mac)                            Tramc
                                                                  4a
              mem_ready (SRAM)
                                                                       4b                                         5a             TFWl
                                                                                5
                                                                                                      TCWP                       TPHYFWl
                   Flash Accesses                                           Tsrar

                                                                                          6           6a                                   6b

           Autoloads from SRAM                                                         Tpciana

                                                                                                           7
                   SBT Calibration
                                                                                                       TSBTC
              Manageability / Wake

                       PCI Express
                    reference clock
                                                                            9
                           PERST#
                                                                                                                                                          17
                                                                                                                       tpcipll
                                                                                                                  10
                   PCIe PLL State         PLL reset                                                                                                              PLL Stable

                      Phy init done
                                                                                                                            12                                 13          14
                                                                                                                                                         PCIe config   PCIe config
              PCI Express Link up                                                                                                                   L0   access        response
                                                                                                                                                                         15
                            D-State                                                              Dr                                                      D0u                         D0a

                                                                                                                                                                                            16
                                                                                                                                                                                            TBIOSL

Figure 4-2.                 Power-Up Timing Diagram

Table 4-1.                  Notes for Power-Up Timing Diagram
  No.                                                                                                      Note

# 1 Internal Power On Reset (POR) is released Trspor after power is stable and the reset pin has been de-asserted, releasing

                PLL kickstart.

# 2 Bgap indication is checked. If it is good, the PLL starts calibration and lock mechanism. Once PHY PLLs are locked, the

                efuses are read and the clock dividers are released to provide stable clocks. Finally, the PHY releases the POR signal to
                the MAC.

    3 MAC starts its MAC-power-up-flow and internal LAN_PWR_Good signal is asserted (clocked on 50 MHz). At this stage,

                internal clocks are stable.

  4a            Clear RAM contents

# 5 Shadow RAM read.

  5a            Clear Flash write protection, Interleaved Manageability and PHY firmware load (in parallel). The FLASH accesses are
                active at the same time, but with only one SPI bus, the indicated times must be summed, arbitration determines which
                finishes first

138                                                                                                                                                                                        333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

Table 4-1.       Notes for Power-Up Timing Diagram [continued]
  No.                                                                 Note

    6 NVM read starts following the read of the Shadow RAM.

         First Flash auto-read sequence is owned by the MAC to load PCI analog section, LAN and PCIe sections, APM enable, and
         other configuration words from legacy NVM initialization section.
         A PERST# de-assertion restarts part of the auto-load process.

    5 APM wake-up and/or manageability active, based on NVM contents (if enabled).

# 6 In this second MAC auto-load sequence, MAC manageability and wake-up modules are loaded (if manageability /

         wake-up enabled).

   6a    First auto-load of LAN sections: MAC module if manageability is enabled.

   6b    Second auto-load of LAN sections PCIe general configuration; PCIe configuration space; LAN core modules, and MAC,
         module if manageability is not enabled.

    7 SVR calibration - should be done before PERST# de-assertion

    8 PERST# is de-asserted by minimum tPVPGL after power is stable (PCIe specification).

# 9 The PCIe reference clock is valid tPWRGD-CLK before the de-assertion of PERST# (PCIe specification).

# 10 De-assertion of PERST# to PCIe PLL stable tPCIPLL.

# 12 PCIe link training starts after tpgtrn from PERST# de-assertion (PCIe specification).

    13 A first PCIe configuration access might arrive after tpgcfg from PERST# de-assertion (PCIe specification).

    14 A first PCI configuration response can be sent after tpgres from PERST# de-assertion (PCIe specification).

# 15 Setting the Memory Access Enable or Bus Master Enable bits in the PCI Command register transitions the X550 from D0u

         to D0 state.

    16 BIOS software reads the PCIe driver and iSCSI/FCoE boot code from Flash, via expansion ROM.

# 17 Note: PHY Init Done is a per port indication.

         This indication is used by Windows drivers (by either polling or interrupt notification) to know that PHY Device IDs are
         readable via MDIO. The requirement is that it is readable within a maximum of 200 ms after software reset.

#### 4.1.2.1 Timing Requirements

The X550 requires the following start-up and power-state transitions.

Table 4-2.       Power-Up Timing Requirements
  Parameter                            Description                            Min       Max                     Notes

txog             Base 50 MHz clock stable from power stable.                           10 ms

tPWRGD-CLK       PCIe clock valid to PCIe power good.                        100 s       -      According to PCIe specification.

tPVPGL           Power rails stable to PCIe reset inactive.                  100 ms       -      According to PCIe specification.

tpgcfg           External PCIe reset signal to first configuration cycle.    100 ms              According to PCIe specification.

Note:        It is assumed that the external 50 MHz clock source is stable after power is applied; the
             timing for that is part of txog.

333369-009                                                                                                                          139
                                       Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                              Initialization

#### 4.1.2.2 Timing Guarantees

The X550 guarantees the following start-up and power-state transition related timing parameters.

Table 4-3.    Power-Up Timing Guarantees
  Parameter                   Description                    Min         Max                           Notes

txog          Xosc stable from power stable.                            10 ms

Trspor        Internal POR from power stable.              21,000 s   21,000 s    Uses an internal timer based on 50MHz
                                                                                    clock.

Tbgg          Bandgap good indication is checked.          5,280 s    10,560 s    If the bandgap does not report good,
                                                                                    kickstart is issued and the bandgap status
                                                                                    is checked again after Tbgg.

Tcal_pll      VCO calibration of one PLL                     41 s     5,200 s     worst case timing is when this step needs
                                                                                    to iterate.

Tpll          Lock detection of one PLL is checked.        5,280 s    10,560 s    If PLL is not locked, kickstart is issued and
                                                                                    the PLL lock status is checked again after
                                                                                    Tpll.

Tclkdiv       Release of reset to the clock dividers.       1.1 s      1.1 s

Tefuse        Read EFUSE content.                           500 s      500 s

tppg          Internal MAC power good delay from valid     37,423 s   63,581 us    Typically the time is no worse than 42 ms.
              power rail.

tfl           Flash auto-read duration.                                  3 ms

topll         PCIe reset to start of link training.                     10 ms

tpcipll       PCIe reset to PCIe PLL stable.                             3 ms

tpgtrn        PCIe reset to start of link training.                     20 ms       According to PCIe specification.

tpgres        PCIe reset to first configuration response    100 ms                  According to PCIe specification.
              cycle.

Tramc         RAM clear time                                 81 s

Tsrar         Shadow RAM read time                         10.8 ms

TFWl          Manageability firmware load                   300 ms      380 ms      Assumes 12.5 MHz clock

TPHYFWl       PHY firmware load                             160 ms      240 ms      Assumes 22.5 MHz clock

TCWP          Clear Write protect                           100 s

TPCIana       PCI Analog Section auto-load                  65 ms

TSBTC         PCI Analog Section auto-load                   7 ms       15 ms

TBIOSL        BIOS Expansion ROM auto-load                  700 ms      900 ms      Assumes 12.5 MHz clock

140                                                                                                                    333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

### 4.1.3 Main-Power/Aux-Power Operation

              XTAL-Ref Clock (50MHz)
              Power Supplies
              (3.3v/2.1v/1.2v/1.0/0.83v)
              AUX_PWR                             1

             LAN_PWR_GOOD pin                      2
                                                                      6
              MAIN_PWR_OK

              Internal Pwr-On-Rst                      3

              MAC-LAN-PWR-OK                                 4
              (Internal signal)
                                                                                                       11
              PE_RESET

              NVM init read                                            5            8

              LPLU signals (Internal)                                               7

              PHY Init (Internal)                                                           9
              AN and Link
              @100Mb or 1G                                                                           10

Figure 4-3.     Low-Power Modes Timing Diagram

Table 4-4.      Notes for Low-Power Modes Timing Diagram
  No.                                                             Note

# 1 AUX_PWR set to 1b, indicates that the X550 should support Aux-Power Mode.

# 2 LAN_PWR_GOOD signal de-asserted.

# 3 Internal Power-On-Reset de-asserted, indicates to all the X550 blocks that all power-rails are OK and the external Reset

         signal is de-asserted (reset_n).

# 4 MAC_LAN_PWR_OK de-asserted (internal signal), indicates that all clocks are stable.

    5 MAC reads configuration from NVM.

# 6 Main-Power-OK still de-asserted, indicates that the system still runs from Aux-Power.

    7 LPLU signals asserted from MAC to PHY, indicates the PHY needs to operate at low-speed (100 Mb/s or GbE)

    8 PHY reads configuration from NVM.

    9 PHY Init completes.

    10 PHY auto-negotiation to 100 Mb/s or GbE and establishes link (assuming LP available).

# 11 PE_RESET is still de-asserted, indicates that the system is still down, keep PCIe at reset, and the MAC at low-power

         modes (WoL or MNG).

333369-009                                                                                                                      141
                                        Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                       Initialization
