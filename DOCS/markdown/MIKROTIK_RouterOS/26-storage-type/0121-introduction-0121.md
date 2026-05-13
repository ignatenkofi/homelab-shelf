## Introduction 

It is the sole responsibility of administrators to configure the Maximum Transmission Unit (MTU) such that intended services and applications can be successfully implemented in the network. In other words - administrators must make sure that MTUs are configured in a way that packet sizes do not exceed the capabilities of network equipment. 

Originally MTU was introduced because of the high error rates and low speed of communications. Fragmentation of the data stream gives the ability to correct corruption errors only by resending corrupted fragments, not the whole stream. Also on low-speed connections such as modems, it can take too much time to send a big fragment, so in this case, communication is possible only with smaller fragments. 

But in the present day we have much lower error rates and higher speed of communication, this opens a possibility to increase the value of MTU. By increasing the value of MTU we will result in less protocol overhead and reduce CPU utilization mostly due to interrupt reduction. This way some nonstandard frames started to emerge: 

Giant or Jumbo frames - frames that are bigger than standard (IEEE) Ethernet MTU; Baby Giant or Baby Jumbo frames - frames that are just slightly bigger than standard (IEEE) Ethernet MTU; 

It is common now for Ethernet interfaces to support physical MTU above standard, but this can not be taken for granted. Abilities of other network equipment must be taken into account as well - for example, if 2 routers with Ethernet interfaces supporting physical MTU 1526 are connected through an Ethernet switch, in order to successfully implement some application that will produce these big Ethernet frames, the switch must also support forwarding such frames.
