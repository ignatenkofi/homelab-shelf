## Control Word Usage 

In RouterOS, Control Word is used for packet fragmentation and reassembly inside the VPLS tunnel and is done by utilizing optional Control Word (CW) . CW is added between PW label (demultiplexor) and packet payload and adds an additional 4-byte overhead. 

**==> picture [13 x 13] intentionally omitted <==**

Reordering OOO packets are not implemented, out of order fragments will be dropped 

CW usage is controlled by the of `use-control-word` parameter in VPLS configuration. 

**==> picture [481 x 301] intentionally omitted <==**

As you can see Control Word is divided into 5 fields: 

0000 - 4-bits identifies that the packet is PW (not IP) Flags - 4bits Frag - 2bits value that indicates payload fragmentation. Len - 6bits 

Seq - 16bits sequence number used to detect packet loss / misordering. 

859 

According to RFC generation and processing of sequence numbers is optional. 

860
