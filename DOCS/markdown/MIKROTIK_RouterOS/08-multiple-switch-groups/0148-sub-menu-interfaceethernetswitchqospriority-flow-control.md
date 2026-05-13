## Sub-menu: `/interface/ethernet/switch/qos/priority-flow-control` 

PFC configuration is organized in profiles. Different switch ports can be assigned to different PFC profiles. The maximum number of hardware Tx managers depends on the switch chip model. The builtin profile named " disabled " cannot be changed. 

**==> picture [516 x 200] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string; Default: ) The user-defined name of the PFC profile<br>pause-threshold  (percent:  Transmits a pause frame (XOFF) when the total size of enqueued packets reaches this threshold. Enqueued packets are<br>0%..100% | bytes | auto; counted per ingress port. Applies only when  tx=yes . The value can be given either explicitly in bytes or percent of the<br>Default:  auto) respective shared pool size ( shared-poolX-byte-cap ).<br>resume-threshold  (percen Transmits a resume frame (XON) when the total size of enqueued packets drops down to this threshold. Enqueued packets<br>t: 0%..100% | bytes | auto; are counted per ingress port. Applies only when  tx=yes . The value can be given either explicitly in bytes or percent of the<br>Default:  auto) respective shared pool size ( shared-poolX-byte-cap ).<br>rx  (yes | no; Default:  no) Enables receiving of PFC frames. The received PFC frame pauses the specific priority queues on the port that received the<br>PFC frame for the duration specified by the PFC frame. Disabling rx disables queue pausing.<br>traffic-class  (integer  The list of PFC-enabled traffic classes.<br>array: 0..7)<br>tx  (yes | no; Default:  no) Enables transmition of PFC frames.<br>**----- End of picture text -----**<br>


478
