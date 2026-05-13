## IPv6 Addressing 

Internet Protocol version 6 (IPv6) is the newer version of the Internet Protocol (IP). It was initially expected to replace IPv4 in a short enough time, but for now, it seems that these two versions will coexist on the Internet in foreseeable future. Nevertheless, IPv6 becomes more important, as the date of the unallocated IPv4 address pool's exhaustion approaches. 

The two main benefits of IPv6 over IPv4 are: 

much larger address space; support of stateless and stateful address auto-configuration; built-in security; 

new header format (faster forwarding). 

IPv6 uses 16 bytes addresses compared to 4-byte addresses in IPv4. IPv6 address syntax and types are described in RFC 4291. 

There are multiple IPv6 address types, that can be recognized by their prefix. RouterOS distinguishes the following: 

multicast (with prefix ff00::/8) link-local (with prefix fe80::/10) unique local addresses (with prefix fc00::/7) loopback (the address::1/128) 

unspecified (the address::/128) 

other (all other addresses, including the obsoleted site-local addresses, and RFC 4193 unique local addresses; they all are treated as global unicast). 

One difference between IPv6 and IPv4 addresses is that IPv6 automatically generates a link-local IPv6 address for each active interface that has IPv6 support. 

IPv6 addresses are represented a little bit differently than IPv4 addresses. For IPv6, the 128-bit address is divided into eight 16-bit blocks, and each 16-bit block is converted to a 4-digit hexadecimal number and separated by colons. The resulting representation is called colon-hexadecimal. 

In the example below IPv6 address in binary format is converted to a colon-hexadecimal representation 

```
0010000000000001 0000010001110000 0001111100001001 0000000100110001
0000000000000000 0000000000000000 0000000000000000 0000000000001001
```

```
2001:0470:1f09:0131:0000:0000:0000:0009
```

The IPv6 address can be further simplified by removing leading zeros in each block: 

```
2001:470:1f09:131:0:0:0:9
```

As you can see IPv6 addresses can have long sequences of zeros. This contiguous sequence can be compressed to :: 

```
2001:470:1f09:131::9
```

163 

**==> picture [13 x 13] intentionally omitted <==**

Zero compression can only be used once. Otherwise, you could not determine the number of 0 bits represented by each instance of a doublecolon 

IPv6 prefix is written in address/prefix-length format. Compared to IPv4 decimal representation of a network mask cannot be used. Prefix examples: 

```
2001:470:1f09:131::/64
2001:db8:1234::/48
2607:f580::/32
2000::/3
```
