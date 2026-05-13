## Bitwise Operators 

Bitwise operators are working only on IP, and IPv6 address data types. 

Operator Description 

Example 

1097 

**==> picture [509 x 231] intentionally omitted <==**

**----- Start of picture text -----**<br>
“~” bit inversion :put (~0.0.0.0)<br>:put (~::ffff)<br>“|” bitwise OR. Performs logical OR operation on each pair of corresponding bits. In each pair the result is  :put (192.168.88.0|0.<br>“1” if one of the bits or both bits is “1”, otherwise the result is “0”. 0.0.255)<br>:put (2001::1|::ffff)<br>“^” bitwise XOR. The same as OR, but the result in each position is “1” if two bits are not equal, and “0” if the  :put (1.1.1.1^255.<br>bits are equal. 255.0.0)<br>:put (2001::ffff:1^::<br>ffff:0)<br>“&” bitwise AND. In each pair, the result is “1” if the first and second bit is “1”. Otherwise, the result is “0”. :put (192.168.88.77<br>&255.255.255.0)<br>:put (2001::<br>1111&ffff::)<br>“<<” left shift by a given amount of bits, not supported for IPv6 address data type :put (192.168.88.77<br><<8)<br>“>>” right shift by a given amount of bits, not supported for IPv6 address data type :put (192.168.88.77<br>>>24)<br>**----- End of picture text -----**<br>


Calculate the subnet address from the given IP and CIDR Netmask using the "&" operator: 

```
{
:local IP 192.168.88.77;
:local CIDRnetmask 255.255.255.0;
:put ($IP&$CIDRnetmask);
}
```

Get the last 8 bits from the given IP addresses: 

```
 :put (192.168.88.77&0.0.0.255);
```

Use the "|" operator and inverted CIDR mask to calculate the broadcast address: 

```
{
:local IP 192.168.88.77;
:local Network 192.168.88.0;
:local CIDRnetmask 255.255.255.0;
:local InvertedCIDR (~$CIDRnetmask);
:put ($Network|$InvertedCIDR)
}
```
