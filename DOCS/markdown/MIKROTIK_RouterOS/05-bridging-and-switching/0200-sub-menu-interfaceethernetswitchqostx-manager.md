## Sub-menu: `/interface/ethernet/switch/qos/tx-manager` 

Transmission (Tx) Manager controls packet enqueuing for transmission and packet tx order. Different switch ports can be assigned to different Tx managers. The maximum number of hardware Tx managers depends on the switch chip model. 

**==> picture [516 x 103] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string;  The user-defined name of the Tx Manager<br>Default: )<br>queue-buffers  (perc The total amount of hardware Tx buffers allocated to all ports linked to this Tx Manager. Any value but auto is NOT scaled by the<br>ent: 0%..100% |  number of ports. For example, if queue-buffers=30%, and there are 3 ports using this Tx Manager, each respective port receives<br>bytes | auto; Default: 10% of total available resources. Adding two more ports to the Tx Manager drops per-port buffers down to 6% (30/5).<br>auto )<br>**----- End of picture text -----**<br>

476 

**==> picture [13 x 13] intentionally omitted <==**

Port status has not effect on the allocated resources. Running ports receive the same amount of queue buffers as disconnected or disabled ones if all of them are assigned to the same Tx Manager.
