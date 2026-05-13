## Properties 

**==> picture [516 x 206] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>baud-rate  (integer | auto;  Baud rate (speed) used by the port. If set to  auto , then RouterOS tries to detect baud rate automatically.<br>Default:  auto )<br>data-bits  (7 | 8; Default: ) The number of data bits in each character.<br>7  - true ASCII<br>8  - any data (matches the size of a byte)<br>dtr  (on | off; Default: ) Whether to enable RS-232 DTR signal circuit used by flow control.<br>flow-control  (hardware | none |  method of flow control to pause and resume the transmission of data.<br>xon-xoff; Default: )<br>name  (string; Default: ) Name of the port.<br>parity  (even | none | odd;  Error detection method. If enabled, extra bit is sent to detect the communication errors. In most cases parity is set to  n<br>Default: ) one  and errors are handled by the communication protocol.<br>**----- End of picture text -----**<br>


1737 

rts (on | off; Default: ) Whether to enable RS-232 RTS signal circuit used by flow control. stop-bits (1 | 2; Default: ) Stop bits sent after each character. Electronic devices usually uses 1 stop bit. 

Read-only properties 

**==> picture [455 x 98] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>channels  (integer) Number of channels supported by the port.<br>inactive  (yes | no) Shows current port state,  inactive=yes  - device with port previous was connected, but currently is not present<br>line-state  ()<br>used-by  (string) Shows who  is currently are using port and channel (#).  For example, by default  Serial0  is used by serial-console.<br>**----- End of picture text -----**<br>
