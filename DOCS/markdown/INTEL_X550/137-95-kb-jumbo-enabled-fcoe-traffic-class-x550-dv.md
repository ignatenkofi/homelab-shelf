## 9.5 KB Jumbo Enabled                           FCoE Traffic Class                                X550 DV

                   No                                           No                                         24 KB

                   No                                          Yes                                         25 KB

                   Yes                                          No                                         50 KB

                   Yes                                         Yes                                         35 KB

                   No                                           No                                         27 KB

                   No                                          Yes                                         27 KB

                   Yes                                          No                                         60 KB

                   Yes                                         Yes                                         45 KB

Note:   9.5 KB Jumbo enabled/disabled is a global setting per port which concerns all Traffic Classes except the FCoE Traffic Class.

3.7.4.3.4                FC Low Threshold — FCRTL

The low threshold value is aimed to protect against wasted available host bandwidth. There is some
latency from the time that the low threshold is crossed until the XON frame is sent and packets are
received from the link partner. The low threshold must be set high enough so that the Rx packet buffer
does not get empty before any new entire packets are received from the link partner. When considering
data movement from the Rx packet buffer to host memory, large packets represent the worst.
Assuming the host bandwidth is about the bandwidth on the wire (when dual ports are active at a given
time), and assuming a PCIe round trip is required to get the receive descriptors, we get the following
formula for FCRTL:
    FCRTL = 2 x MaxFrame(TC) + PCIe round trip delay

PCIe round trip delay is assumed to be ~ 1 us and it must cover for worst case incoming traffic pattern
(buffer utilization by 1.44 than wire rate):
    FCRTL (bit time units) = 2 x MaxFrame(TC) + 1.44 x 10,000

Setting the FCRTL to lower values than expressed by the previous equation is permitted. It might
simply result with potential sub-optimal use of the PCIe bus once bandwidth is available.

Table 3-45. X550 FCRTL
