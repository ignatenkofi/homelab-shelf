## CPU Flow Control 

All switch chips have a special port that is called switchX-cpu , this is the CPU port for a switch chip, it is meant to forward traffic from a switch chip to the CPU, such a port is required for management traffic and routing features. By default the switch chip ensures that this special CPU port is not congested and sends out Pause Frames when link capacity is exceeded to make sure the port is not oversaturated, this feature is called CPU Flow Control . Without this feature packets that might be crucial for routing or management purposes might get dropped. 

Since RouterOS v6.43 it is possible to disable the CPU Flow Control feature on some devices that are using one of the following switch chips: QCA8337, Atheros8227, Atheros8327, Atheros7240, Atheros8316, 88E6191X and 88E6393X . Other switch chips have this feature enabled by default and cannot be changed. To disable CPU Flow Control use the following command: 

```
/interface ethernet switch set switch1 cpu-flow-control=no
```
