## 3.2 Management Interfaces

The X550 contains three possible interfaces to an external BMC.
 • SMBus
 • NC-SI (over RMII)
 • MCTP (over PCIe or SMBus)

### 3.2.1 SMBus

SMBus is an optional interface for pass-through and/or configuration traffic between an external BMC
and the X550. The SMBus channel behavior and the commands used to configure or read status from
the X550 are described in Section 11.5.
The X550 also enables reporting and controlling the device using the MCTP protocol over SMBus. The
MCTP interface is used by the BMC to control the NIC and for pass-through traffic. All network ports are
mapped to a single MCTP endpoint on SMBus. For information, refer to Section 11.5.

#### 3.2.1.1 Channel Behavior

The SMBus specification defines a maximum frequency of 100 KHz. However, when acting as a slave,
the X550 can receive transaction with a clock running at up to 1 MHz. When acting as a master, it can
toggle the clock at 100 KHz, 400 KHz or 1 MHz. The speed used is set by the SMBus Connection Speed
field in the SMBus Notification Timeout and Flags NVM word (Section 6.2.17.3).
