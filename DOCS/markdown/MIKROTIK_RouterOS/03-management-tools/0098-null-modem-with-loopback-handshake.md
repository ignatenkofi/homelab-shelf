## Null Modem With Loopback Handshake 

236 

The problem with the first cable is when connected to a device on which hardware flow control is enabled software may hang when checking modem signal lines. 

Null modem cable with loop back handshake fixes the problem, its main purpose is to fool well-defined software into thinking there is handshaking available: 

**==> picture [318 x 155] intentionally omitted <==**

**----- Start of picture text -----**<br>
Side1 (DB9f) Side2 (DB9f) Function<br>2 3 Rx ← Tx<br>3 2 Tx → Rx<br>5 5 GND<br>1+4+6 - DTR → CD + DSR<br>- 1+4+6 DTR → CD + DSR<br>7+8 - RTS → CTS<br>- 7+8 RTS → CTS<br>**----- End of picture text -----**<br>

Hardware flow control is not possible with this cable. Also if remote software does not send its own ready signal to DTR output communication will hang.
