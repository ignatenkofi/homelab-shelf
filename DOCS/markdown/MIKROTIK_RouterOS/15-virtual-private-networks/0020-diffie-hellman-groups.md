## Diffie-Hellman Groups 

Diffie-Hellman (DH) key exchange protocol allows two parties without any initial shared secret to create one securely. The following Modular Exponential (MODP) and ECP Diffie-Hellman (also known as "Oakley") Groups are supported: 

**==> picture [361 x 231] intentionally omitted <==**

**----- Start of picture text -----**<br>
Diffie-Hellman Group Name Reference<br>Group 1 768 bits MODP group RFC 2409<br>Group 2 1024 bits MODP group RFC 2409<br>Group 5 1536 bits MODP group RFC 3526<br>Group 14 2048 bits MODP group RFC 3526<br>Group 15 3072 bits MODP group RFC 3526<br>Group 16 4096 bits MODP group RFC 3526<br>Group 17 6144 bits MODP group RFC 3526<br>Group 18 8192 bits MODP group RFC 3526<br>Group 19 256 bits random ECP group RFC 5903<br>Group 20 384 bits random ECP group RFC 5903<br>Group 21 521 bits random ECP group RFC 5903<br>**----- End of picture text -----**<br>

More on standards can be found here. 

Larger DH groups offer better security but require more CPU power. Here are a few commonly used DH groups with varying levels of security and CPU impact: 

DH Group 14 (2048-bit) - Provides a reasonable balance between security and CPU usage. It offers 2048-bit key exchange, which is considered secure for most applications today and is widely supported. 

DH Group 5 (1536-bit) - Offers a slightly lower level of security compared to DH Group 14 but has a lower CPU impact due to the smaller key size. It is still considered secure for many scenarios. 

DH Group 2 (1024-bit) - Should be used with caution because it provides the least security among commonly used groups. It has a lower CPU impact but is susceptible to attacks, especially as computational power increases. It's generally not recommended for new deployments. 

For optimal security, it's advisable to use DH Group 19 . It's considered fast and secure. DH Group 2 should generally be avoided unless you have legacy devices that require it. 

**==> picture [13 x 13] intentionally omitted <==**

The correct way of calculating security for your network infrastructure would be to choose how many bits of security you want and you could see how long it would require to decrypt your data, then you have to choose algorithms. Please see information for reference https://www.keylength. com/en/4/ 

1190
