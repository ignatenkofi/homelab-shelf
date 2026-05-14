## Sub-menu: `/interface/ethernet/switch/qos/tx-manager/queue` 

Each port has eight Tx queues. The assigned Tx Manager controls packet enqueuing and schedules transmission orders. Each queue can have either strict priority (where packets with the highest traffic class are always transmitted first) or grouped together for a weighted round-robin tx schedule. 

Creating a Tx Manager automatically creates all eight respective queue schedulers. 

**==> picture [13 x 13] intentionally omitted <==**

Changing any properties of Tx manager or queues completely halts traffic enqueueing and transmission during the offload process. Temporary packet loss is expected while the device is forwarding traffic. 

**==> picture [516 x 483] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>tx-manager  (na The linked Tx Manager<br>me; read-only)<br>traffic-class  (int The traffic class (tc0..tc7) and the respective port queue (queue0..queue7) that the scheduler controls.<br>eger: 0..7;<br>read-only)<br>schedule  (strict-<br>priority | high- strict-priority  - packets in the respective queue are always scheduled before moving to lower traffic classes. Packets with lower<br>priority-group |  traffic classes are not transmitted until the current queue is empty.<br>low-priority- high-priority-group  - all queues in the group are scheduled together by using a weighted round-robin principle. For example, if<br>group ) TC5 has weight 4, TC4 - 3, and TC3 - 2, then the scheduler transmits 4 packets from queue5, 3 packets from Q4, and 2 packets<br>from Q3 in a single round. To achieve lower latency, each round is "sliced" between all queues in the group. In other words, the<br>packet order in each round of the above example is "Q5, Q4, Q3, Q5, Q4, Q3, Q5, Q4, Q5".<br>low-priority-group  - similar logic to the high-priority-group, but the low-priority-group is scheduled only when all queues in the<br>high-priority-group are empty.<br>weight  (integer:  The weight value for the traffic class if it is a member of a schedule group. The field is not used in the case of strict priority schedule.<br>0..255; Default:  1<br>)<br>queue-buffers  ( The amount of hardware Tx buffers allocated to this queue. Any value but auto is NOT scaled by the number of ports, i.e., the value<br>percent: 0%.. gets split on ports linked to the Tx Manager. When given in percent, it means percentage of the tx-manager's queue-buffers value.<br>100% | bytes |<br>auto; Default:  a<br>uto )<br>use-shared- Allow the queue to use the shared buffer pool when  queue-buffers  are full. If the queue is full and the shared buffers are disabled, the<br>buffers  (yes |  packet gets dropped. If the shared buffers are enabled, the queue may use up to  shared-packet-cap  or  shared-poolX-packet-cap  (see<br>no) QoS Settings for details) packets from the shared pool.<br>shared-pool- The shared pool index for the queue to use. Relevant only if  use-shared-buffers=yes  and the device supports multiple shared pools.<br>index  (integer;<br>Default: ) 0<br>wred  (yes | no;  Enables/disables Weighted Random Early Detection for the given queue.<br>Default:  no)<br>ecn ( yes | no;  Enables/disables ECN marking of the transmitted packets.<br>Default: no )<br>wred-actual  (ye The actual WRED value.<br>s | no;  read-<br>only)<br>**----- End of picture text -----**<br>

477 

ecn-actual (yes The actual ECN value. 

| no;  read-only) 

**==> picture [13 x 13] intentionally omitted <==**

On some device models, due to hardware limitations, enabling ECN on one queue turns on CE marking of ECN-capable packets on all queues. In such cases, `ecn-actual=yes` despite `ecn=no` .
