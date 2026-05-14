## Null Modem Without Handshake 

This cable does not utilize handshake pins at all: 

**==> picture [317 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Side1 (DB9f) Side2 (DB9f) Function<br>2 3 Rx ← Tx<br>3 2 Tx → Rx<br>5 5 GND<br>**----- End of picture text -----**<br>

It allows data-only traffic on the cross-connected Rx/Tx lines. Hardware flow control is not possible with this type of cable. The only way to perform flow control is with software flow control using the XOFF and XON characters.
