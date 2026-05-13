## Hardware Resources 

The hardware (switch chips) has limited resources (memory). There are two main hardware resources that are relevant to QoS: 

Packet descriptors - contain packet control information (target port, header alternation, etc). Data buffers - memory chunks containing the actual payload. Buffer size depends on the switch chip model. Usually - 256 bytes. 

One packet descriptor may use multiple buffers (depending on the payload size); buffers may be shared by multiple descriptors - in cases of multicast /broadcast. If the hardware does not have enough free descriptors or buffers, the packet gets dropped (tail-drop). 

Hardware resources can be limited per destination type (multicast/unicast), per port, and per each tx queue. If any limits are reached, no more packets can be enqueued for transmission, and further packets get dropped. 

RouterOS obscures low-level hardware information, allowing to set resource limits either in terms of packets or a percentage of the total amount. RouterOS automatically calculates the required hardware descriptor and buffer count based on the user-specified packet limit and port's MTU. Moreover, RouterOS comes with preconfigured hardware resources, so there is no need to do a manual configuration in common QoS environments. 

**==> picture [13 x 13] intentionally omitted <==**

Changing any hardware resource allocation parameter in runtime results in a temporary device halt when no packets can be enqueued nor transmitted. Temporary packet loss is expected while the device is forwarding traffic.
