## 12.8 Devices Supported

### 12.8.1 Flash

The X550 supports the following 3.3 V Flash devices with an SPI interface.
To provide some flexibility in the Bill of Materials (BOM), a few options are supported:

  Flash Size      Manufacturer                  Part Number

               EON Silicon         EN25QH32

               ESMT                F25L32PA / F25L32QA

               Fidelix             FM25Q32A

    4 MB      Macronix            MX25L3233F

               Micron              N25Q032A

               Spansion            S25FL132K

               Winbond             W25Q32FV

               Adesto Tech         AT25SF161-SHD-T

    8 MB      Macronix            MX25V1635FM2I

               Winbond             W25Q16JVSNIQ

               Adesto Tech         AT25SF321-SHD-T

    16 MB      Macronix            MX25L3233FM2I-08G

               Winbond             W25Q32JVSSIQ

               Adesto Tech         AT25SF641-SUT-T

    32 MB      Macronix            MX25L6433FM2I-08G

               Winbond             W25Q64JVSSIQ

333369-009                                                                                 1137
                                 Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                     Electrical/Mechanical Specification

NOTE:   This page intentionally left blank.

1138                                                                                        333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

Chapter 13 Design Considerations and
           Guidelines

This section provides guidelines for selecting components, connecting interfaces, using special pins, and
layout guidance.
Unused interfaces should be terminated with pull-up or pull-down resistors. These are indicated in
Section 2 or reference schematics. There are reserved pins, identified as RSVD_NC and RSVD_VSS. The
X550 might enter special test modes unless these strapping resistors are in place.
Some unused interfaces must be left open. Do not attach pull-up or pull-down resistors to any balls
identified as No Connect or Reserved No Connect.
