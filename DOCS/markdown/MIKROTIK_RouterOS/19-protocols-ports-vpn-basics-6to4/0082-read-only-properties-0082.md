## Read-only properties 

**==> picture [367 x 212] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>AH  (yes | no) Whether AH protocol is used by this SA.<br>ESP  (yes | no) Whether ESP protocol is used by this SA.<br>add-lifetime  (time/time) Added lifetime for the SA in format soft/hard:<br>soft - time period after which IKE will try to establish new SA;<br>hard - time period after which SA is deleted.<br>addtime  (time) Date and time when this SA was added.<br>auth-algorithm  (md5 | null | sha1 | ...) Currently used authentication algorithm.<br>auth-key  (string) Used authentication key.<br>current-bytes  (64-bit integer) A number of bytes seen by this SA.<br>dst-address  (IP) The destination address of this SA.<br>**----- End of picture text -----**<br>


1202 

enc-algorithm (des | 3des | aes-cbc | ...) Currently used encryption algorithm. 

**==> picture [367 x 153] intentionally omitted <==**

**----- Start of picture text -----**<br>
enc-key  (string) Used encryption key.<br>enc-key-size  (number) Used encryption key length.<br>expires-in  (yes | no) Time left until rekeying.<br>hw-aead  (yes | no) Whether this SA is hardware accelerated.<br>replay  (integer) Size of replay window in bytes.<br>spi  (string) Security Parameter Index identification tag<br>src-address  (IP) The source address of this SA.<br>state  (string) Shows the current state of the SA ("mature", "dying" etc)<br>**----- End of picture text -----**<br>


Commands 

**==> picture [268 x 42] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>flush  () Manually removes all installed security associations.<br>**----- End of picture text -----**<br>
