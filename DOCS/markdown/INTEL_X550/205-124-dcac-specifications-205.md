## 12.4 DC/AC Specifications

### 12.4.1 Digital Functional 3.3 V I/O DC Electrical

                   Characteristics

Table 12-5. Digital I/O LAN_PWR_GOOD
  Symbol             Parameter                       Description             Min         Typ       Max        Units

VIH        Input High Voltage                                                0.84                  3.60         V

VIL        Input Low Voltage                                                -0.30                  0.36         V

VT         Threshold Point                                                               0.60                   V

           Input Leakage Current at
lil
           VI=3.3 V or 0 V
                                                                                                               A

           Tri-state Output Leakage
IOZ
           Current at VO=3.3 V or 0 V
                                                                                                               A

PD         Internal Pull Down                                                 50                    70         K

PU         Internal Pull Up                                                   50                    70         K

Table 12-6. Digital I/O LED, SDP
  Symbol             Parameter                        Conditions             Min         Max      Units       Note

                                             LED IOH = -16 mA
VOH        Output High Voltage               SDP IOH = -12 mA                2.4                    V
                                             VCC3P3 = minimum

                                             LED IOL = 16 mA
VOL        Output Low Voltage                SDP IOL = 12 mA                             0.4        V
                                             VCC3P3 = minimum

VIH        Input High Voltage                                                2.0         3.45       V

VIL        Input Low Voltage                                                 -0.3        0.8        V

lil        Input Leakage Current                                                         10         A
IOFF       Current at IDDQ Mode                                                          10         A
PD         Internal Pull Down                                                 50         70         K

Cin        Pin Capacitance                                                                5         pF

Cload      Pin Capacitance                                                                5         pF

Notes:
 1. Table 12-6 applies to ENCRYPTION_EN, LED0_[3:0], LED1_[3:0], SDP0_[3:0], and SDP1_[3:0].
 2. Digital I/O is 3.3 V input tolerance.

1122                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

Table 12-7. Digital I/O Flash
   Symbol              Parameter1                      Conditions            Min       Max   Units   Note

                                              IOH = -12 mA
 VOH         Output High Voltage                                              2.4             V
                                              VCC3P3 = minimum

                                              IOL = 12 mA
 VOL         Output Low Voltage                                                        0.7    V
                                              VCC3P3 = minimum

 VIH         Input High Voltage                                               2.0      3.6    V

 VIL         Input Low Voltage                                               -0.3      0.7    V

 lil         Input Leakage Current                                                     10     A
 IOFF        Current at IDDQ Mode                                                      10     A
 PU          Internal Pull Up                                                 50       70     K

 Cin         Pin Capacitance                                                            5     pF

 Cload       Pin Capacitance                                                            5     pF

 Note:   Table 12-7 applies to FLSH_SO, FLSH_SI, FLSH_CE_N, FLSH_SCK.

1. Parameters listed are 3.3 V tolerant.

Table 12-8. Digital I/O JTAG
   Symbol               Parameter                      Conditions            Min       Max   Units   Note

                                              IOH = -12 mA
 VOH         Output High Voltage                                              2.4             V
                                              VCC3P3 = minimum

                                              IOL = 12 mA
 VOL         Output Low Voltage                                                        0.7    V
                                              VCC3P3 = minimum

 VIH         Input High Voltage                                               2.0      3.6    V

 VIL         Input Low Voltage                                               -0.3      0.7    V

 lil         Input Leakage Current                                                     10     A
 IOFF        Current at IDDQ Mode                                                      10     A
 PU          Internal Pull Up                                                 50       70     K

 PD          Internal Pull Down                                               34       101    K

 Cin         Pin Capacitance                                                            5     pF

 Cload       Pin Capacitance                                                            5     pF

 Note:   Table 12-8 applies to TDO, TDI, TMS, TCK. TRST_N.

333369-009                                                                                              1123
                                       Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                            Electrical/Mechanical Specification

Table 12-9. Digital I/O Miscellaneous, PE_RST_N
  Symbol               Parameter                         Conditions                  Min       Max        Units       Note

                                               IOH = -12 mA
VOH          Output High Voltage                                                     2.4                    V
                                               VCC3P3 = minimum

                                               IOL = 12 mA
VOL          Output Low Voltage                                                                 0.7         V
                                               VCC3P3 = minimum

VIH          Input High Voltage                                                      2.0        3.6         V

VIL          Input Low Voltage                                                      -0.3        0.7         V

lil          Input Leakage Current                                                              10          A
IOFF         Current at IDDQ Mode                                                               10          A
PU           Internal Pull Up                                                        50         70          K

Cin          Pin Capacitance                                                                     5          pF

Cload        Pin Capacitance                                                                     5          pF

Note:     Table 12-9 applies to AUX_PWR, MAIN_PWR_OK, LAN1_DIS_N, LAN0_DIS_N, BYPASS_POR, ENCRYPTION_EN, and
          PE_RST_N.

### 12.4.2 Open Drain I/Os

Table 12-10. Open Drain I/Os
  Symbol               Parameter                          Condition                  Min       Max        Units       Note

Vih          Input High Voltage                                                      2.1                    V

Vil          Input Low Voltage                                                                  0.8         V

Ileakage     Output Leakage Current            0  Vin  VCC3P3 maximum                         ±10         A          2

Vol          Output Low Voltage                @ Ipullup = 4 mA                                 0.4         V           5

Ipullup      Current Sinking                   Vol = 0.4 V                            4                     mA

Cin          Input Pin Capacitance                                                               7          pF          3

Cload        Maximum Load Pin Capacitance                                                       30          pF          4

Ioffsmb      Input leakage Current             VCC3P3 off or floating                           ±10         A          2

Notes:
 1. Section 12.4.2 applies to SMBD, SMBCLK, SMBALRT_N, PE_WAKE_N.
 2. Device must meet this specification whether powered or un-powered.
 3. Characterized, not tested.
 4. Cload should be calculated according to the external pull-up resistor and the frequency.
 5. OD no high output drive. VOL max=0.4 V at 16 mA, VOL max=0.2 V at 0.1 mA.

The buffer specification meets the SMBus specification requirements defined at: www.smbus.org.

1124                                                                                                               333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

### 12.4.3 NC-SI I/O DC Specification

Table 12-11. NC-SI I/O DC Specification
 Symbol                 Parameter                          Conditions                Min.         Typ.         Max         Units

Vref1        Bus High Reference                                                       3.0         3.3          3.46          V

Vabs         Signal Voltage Range                                                    -0.3                     3.765          V

ViL          Input Low Voltage                                                                                 0.8           V

ViH          Input High Voltage                                                       2.0                                    V

                                                  IoL = 4 mA
VoL          Output Low Voltage                                                        0                       0.4           V
                                                  Vref= Vrefmin

                                                  IoL = -4 mA
VoH          Output High Voltage                                                      2.4                      Vref          V
                                                  Vref= Vrefmin

                                                  Vin = 3.6 V
IiH          Input High Current                                                        0                       200           A
                                                  Vref = 3.6 V

                                                  Vin = 0 V
IiL          Input Low Current                                                       -20                        0            A
                                                  Vrefmin to Vrefmax

Vckm         Clock Midpoint Reference Level                                                                    1.4           V

             Leakage Current for Output           0  Vin  Vihmax
Iz                                                                                   -20                        20           A
             Signals in High-Impedance State      @Vref = Vrefmax

Notes:
 1. Vref = Bus high reference level. This parameter replaces the term supply voltage since actual devices can have internal
    mechanisms that determine the operating reference for the sideband interface that are different from the device’s overall
    power supply inputs. Vref is a reference point that is used for measuring parameters such as overshoot and undershoot and for
    determining limits on signal levels that are generated by a device. To facilitate system implementations, a device must provide
    a mechanism (such as a power supply pin, internal programmable reference, or reference level pin) to enable Vref to be set to
    within 20 mV of any point in the specified Vref range. This is to enable a system integrator to establish an interoperable Vref
    level for devices on the sideband interface. Although the NC-SI specification define the Vrefmax up to 3.6 V, the X550 supports
    the Vrefmax up to 3.46 V (3.3 V +5%).
 2. Section 12.4.3 applies to NCSI_CLK_IN, NCSI_CRS_DV, NCSI_RXD[1:0], NCSI_TX_EN and NCSI_TXD[1:0], NCSI_ARB_IN,
    NCSI_ARB_OUT.
 3. Refer to the Network Controller Sideband Interface (NC-SI) Specification for more details.

333369-009                                                                                                                        1125
                                      Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                        Electrical/Mechanical Specification

### 12.4.4 Digital I/F AC Specifications

#### 12.4.4.1 Digital I/O AC Electrical and Timing Characteristics

Table 12-12. Digital 3.3 V I/O AC Specifications — SDP
        Parameters                   Description            Min        Max                Condition               Notes

fsymbol                 Symbol Rate                                   25 MS/s

#### 12.4.4.2 Digital 3.3 V I/O AC Specifications — JTAG AC

                         Specifications

Table 12-13. JTAG I/F Timing Parameters
 Symbol                                   Parameter                             Min         Typ        Max         Unit

tjclk         JTCK clock frequency                                                                      10         MHz

tjh           JTMS and JTDI hold time                                            10                                 ns

tjsu          JTMS and JTDI setup time                                           10                                 ns

tjpr          JTDO propagation delay                                                                    15          ns

Notes:
 1. Table 12-13 applies to JTCK, JTMS, JTDI and JTDO.
 2. Timing measured relative to JTCK reference voltage of VCC3P3/2.

Figure 12-2. JTAG AC Timing Diagram

1126                                                                                                           333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

#### 12.4.4.3 SMBus AC Specifications

The X550 meets the SMBus AC specification of 100 KHz as defined in SMBus specification, Version 2,
Section 3.1.1 (http://www.smbus.org/specs/).
The X550 also supports a 400 KHz SMBus (as an input clock from the MC and as a slave). The X550
meets the 100 KHz, 400 KHz, and 100 MHz specifications listed in Table 12-14.

Table 12-14. SMBus Timing Parameters (Master Mode)
                                                                           Typ        Typ        Typ
     Symbol                     Parameter                      Min                                        Max    Units
                                                                         100 KHz1   400 KHz2   1 MHz3,4

 FSMB           SMBus Frequency                                            100        400       1000      1000   KHz

                Time between STOP and START
 TBUF                                                          0.5         4.7        1.3        0.5              s
                condition driven by the X550

                Hold time after Start Condition. After
 THD:STA                                                      0.26          4         0.6        0.26             s
                this period, the first clock is generated.

 TSU:STA        Start Condition setup time                    0.14          2         0.3        0.14             s

 TSU:STO        Stop Condition setup time                     0.26          4         0.6        0.26             s

 THD:DAT        Data hold time                                  0          0.3         0          0               s

 TSU:DAT        Data setup time                               0.05         0.25       0.1        0.05             s

 TTIMEOUT       Detect SMBClk low timeout                      35           35         35        35       35      ms

 TLOW           SMBClk low time                                0.5         4.7        1.3        0.5              s

 THIGH          SMBClk high time                              0.26          4         0.6        0.26             s

1.   Specifications based on SMBus specification.
2.   Specifications based on I2C specification for Fast-mode (400 KHz).
3.   Specifications based on I2C specification rev 03 for Fast-mode Plus (1 MHz).
4.   1 MHz speed may vary and is impacted by the topology.

Table 12-15. SMBus Timing Parameters (Slave Mode)
                                                                         Min 100    Min 400     Min 1
     Symbol                          Parameter                                                            Max    Units
                                                                          KHz1       KHz2       MHz3

 FSMB          SMBus Frequency                                              10         10        10       1000   KHz

 TBUF          Time Between STOP and START                                 4.7        1.3        0.5              s

               Hold Time After Start Condition. After This Period, the
 THD,STA                                                                    4         0.6        0.26             s
               First Clock is Generated.

 TSU,STA       Start Condition Setup Time                                  4.7        0.6        0.26             s

 TSU,STO       Stop Condition Setup Time                                    4         0.6        0.26             s

 THD,DAT       Data Hold Time                                              300        100         0               s

 TLOW          SMBCLK Low Time                                             250        100        50               s

 THIGH         SMBCLK High Time                                            4.7        1.3        0.5              s

1. Specifications based on SMBus specification.
2. Specifications based on I2C specification for Fast-mode (400 KHz).
3. Specifications based on I2C specification rev 03 for Fast-mode Plus (1 MHz).

333369-009                                                                                                             1127
                                         Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                  Electrical/Mechanical Specification

Figure 12-3. SMBus I/F Timing Diagram

#### 12.4.4.4 Flash AC Specification

The X550 is designed to support a serial Flash.For Flash I/F timing specifications, see Table 12-16 and
Figure 12-4.

Table 12-16. Flash I/F Timing Parameters from Supported Flash Devices
  Symbol                                   Parameter                                  Min        Max        Units

fSCK        Serial Clock (SCK) Frequency                                                          25         MHz

fRDLF       SCK Frequency for Read Array (Low Frequency - 0x03 Opcode)                            25         MHz

tSCKH       SCK High Time                                                             16                      ns

tSCKL       SCK Low Time                                                              16                      ns

tSCKR(1)    SCK Rise Time - Peak-to-Peak (Slew Rate)                                  0.1                    V/ns

SCKF(1)     SCK Fall Time - Peak-to-Peak (Slew Rate)                                  0.1                    V/ns

tCSH        Chip Select High Time                                                     25                      ns

tCSLS       Chip Select Low Setup Time (Relative to SCK)                              10                      ns

tCSLH       Chip Select Low Hold Time (Relative to SCK)                               10                      ns

tCSHS       Chip Select High Setup Time (Relative to SCK)                             10                      ns

tCSHH       Chip Select High Hold Time (Relative to SCK)                              10                      ns

tDS         Data In Setup Time                                                         5                      ns

tDH         Data In Hold Time                                                          5                      ns

tDIS(1)     Output Disable Time                                                                   15          ns

tV(2)       Output Valid Time                                                                     15          ns

tOH         Output Hold Time                                                           1                      ns

1128                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

Figure 12-4. Serial Input Timing

Figure 12-5. Serial Output Timing

333369-009                                                                       1129
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                         Electrical/Mechanical Specification

#### 12.4.4.5 NC-SI AC Specifications

The X550 supports the NC-SI standard as defined in the Network Controller Sideband Interface (NC-SI)
specification. The NC-SI timing specifications can be found in Table 12-17 and Figure 12-6.

Table 12-17. NC-SI Interface AC Specifications
         Parameter               Symbol        Conditions          Min         Typ           Max          Units       Notes

REF_CLK Frequency                                                               50       50+100 ppm        MHz

REF_CLK Duty Cycle                                                 35                         65            %           2

Clock-to-Out[1]
                                Tco                                2.5                       12.5          ns          1,3
(10pF<=cload<=50 pF)

Skew Between Clocks             Tskew                                                        1.5           ns

TXD[1:0], TX_EN, RXD[1:0],
CRS_DV, RX_ER, ARB_IN,
                                Tsu                                 3                                      ns           3
ARB_OUT Data Setup to
REF_CLK Rising Edge

TXD[1:0], TX_EN, RXD[1:0],
CRS_DV, RX_ER, ARB_IN,
                                Thd                                 1                                      ns           3
ARB_OUT Data Hold From
REF_CLK Rising Edge

Signal Rise/Fall Time           Tr/Tf                               1                         6            ns           4

REF_CLK Rise/Fall Time          Tckr/Tckf                          0.5                       3.5           ns

Notes:
 1. This timing relates to the output pins timing while Tsu and Thd relate to timing at the input pins.
 2. REF_CLK duty cycle measurements are made from Vckm to Vckm; middle point (50% of Vref in Section 12.4.3). Clock skew
    Tskew is measured from Vckm to Vckm of two NC-SI devices and represents maximum clock skew between any two devices in
    the system.
 3. All timing measurements are made between Vckm and Vm; middle point (50% of Vref in Section 12.4.3). All output timing
    parameters are measured with a capacitive load between 10 pF and 50 pF.
 4. Rise and fall time are measured between points that cross 10% and 90% of Vref (see Figure 12-6). The middle points (50% of
    Vref) are marked as Vckm and Vm for clock and data, respectively.

Figure 12-6. NC-SI AC Specification

1130                                                                                                               333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

#### 12.4.4.6 Reset Signals

For power-on indication, the X550 can either use an internal power-on circuit, which monitors the 2.1 V,
