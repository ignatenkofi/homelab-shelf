## 4.7 Access to Shared Resources

Part of the resources in the X550 are shared between several software entities — namely the drivers of
the two ports and internal firmware. To avoid contentions, a driver that needs to access one of these
resources should use the Gaining Control of Shared Resource by Software flow described in
Section 11.8.4.1 to acquire ownership of this resource, and use the Releasing a Shared Resource by
Software flow described in Section 11.8.4.2 to relinquish ownership of this resource.
The shared resources are:
 • NVM
 • PHY 0 and PHY 1 registers
 • MAC CSRs

333369-009                                                                                          179
                                 Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                          Initialization

NOTE:   This page intentionally left blank.

180                                                                                         333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

Chapter 5                      Power Management and Delivery

This section defines how power management is implemented in the X550.
