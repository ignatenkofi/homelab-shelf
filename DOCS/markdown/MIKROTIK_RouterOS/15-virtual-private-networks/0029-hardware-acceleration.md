## Hardware acceleration 

Hardware acceleration allows doing a faster encryption process by using a built-in encryption engine inside the CPU. 

List of devices with hardware acceleration is available here 

**==> picture [519 x 222] intentionally omitted <==**

**----- Start of picture text -----**<br>
CPU DES and 3DES AES-CBC AES-CTR AES-GCM<br>MD5 SHA1 SHA256 SHA512 MD5 SHA1 SHA256 SHA512 MD5 SHA1 SHA256 SHA512 MD5 SHA1 SHA256 SHA<br>88F7040 no yes yes yes no yes yes yes no yes yes yes no yes yes yes<br>AL21400 yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes<br>AL32400 yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes<br>AL52400 yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes<br>AL73400 yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes yes<br>IPQ- no yes yes no no yes* yes* no no yes* yes* no no no no no<br>4018 /<br>IPQ-<br>4019<br>IPQ-  yes  yes  yes  no  yes  yes  yes  no  yes  yes  yes  no  no  no  no  no<br>5018<br>IPQ- no no no no no yes yes yes no yes yes yes no yes yes yes<br>6010<br>IPQ- no yes yes no no yes* yes* no no yes* yes* no no no no no<br>8064<br>IPQ- no no no no no yes yes yes no yes yes yes no yes yes yes<br>8072<br>MT7621A yes**** yes**** yes**** no yes yes yes no no no no no no no no no<br>**----- End of picture text -----**<br>

1193 

**==> picture [516 x 117] intentionally omitted <==**

**----- Start of picture text -----**<br>
EN7562 yes**** yes**** yes**** no yes yes yes no yes yes yes no no no no no<br>CT<br>P1023N no no no no yes** yes** yes** yes** no no no no no no no no<br>SN5CFB<br>P202AS yes yes yes no yes yes yes yes no no no no no no no no<br>SE2KFB<br>PPC460 no no no no yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes*** no no no no<br>GT<br>TLR4  yes yes yes no yes yes yes no yes yes yes no no no no no<br>(TILE)<br>x86  no no no no yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes*** yes***<br>(AES-NI)<br>**----- End of picture text -----**<br>

- supported only 128 bit and 256 bit key sizes 

- ** only manufactured since 2016, serial numbers that begin with number 5 and 7 

- *** AES-CBC and AES-CTR only encryption is accelerated, hashing done in software 

**** DES is not supported, only 3DES and/or AES-CBC 

IPsec throughput results of various encryption and hash algorithm combinations are published on the MikroTik products page.
