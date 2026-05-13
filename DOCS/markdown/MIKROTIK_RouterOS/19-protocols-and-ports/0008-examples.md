## Examples 

If a file is requested return the file from the store called sata1: 

```
/ip tftp add req-filename=file.txt real-filename=/sata1/file.txt allow=yes read-only=yes
```

If we want to give out one specific file no matter what the user is requesting: 

```
/ip tftp add req-filename=.* real-filename=/sata1/file.txt allow=yes read-only=yes
```

If the user requests aaa.bin or bbb.bin then give them ccc.bin: 

```
/ip tftp add req-filename="(aaa.bin)|(bbb.bin)" real-filename="/sata1/ccc.bin\\0" allow=yes read-only=yes
```

**==> picture [13 x 13] intentionally omitted <==**

RouterOS receives TFTP requests, but the client gets a transfer timeout? 

Some embedded clients request large block sizes and yet do not handle fragmented packets correctly. For these clients, it is recommended to set "max-block-size" on the RouterOS side or "blksize" on Client-side to the value of the smallest MTU on your network minus 32 bytes (20 bytes for IP, 8 for UDP, and 4 for TFTP) and more if you use IP options on your network. 

1173
