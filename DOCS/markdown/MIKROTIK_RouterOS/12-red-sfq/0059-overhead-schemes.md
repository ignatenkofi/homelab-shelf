## Overhead Schemes 

The overhead compensation feature in CAKE allows it to account for the extra bytes added by various link layer technologies, which can be significant in some cases. This is important because CAKE operates on the packet sizes reported by the Linux kernel, which do not include these extra bytes. If the overhead is not accounted for, CAKE's shaper might allow more data onto the link than it can actually handle, leading to unexpected packet loss. 

1. Manual Overhead Specification : You can manually specify the overhead in bytes. For instance, if you know your link layer adds 18 bytes of overhead to each packet, you can configure CAKE with `overhead 18` . Negative values are also accepted, within a range of -64 to 256 bytes. 

2. MPU : The Minimum Packet Unit (MPU) parameter allows you to round up the size of each packet to a specified minimum. This is useful for link layer technologies that have a minimum packet size. For example, if your link layer technology has a minimum packet size of 64 bytes, you can configure CAKE with `mpu 64` . 

3. ATM : This is for Asynchronous Transfer Mode, a type of network technology often used in DSL broadband connections. ATM uses fixed 53-byte cells, each of which can carry 48 bytes of payload. The `atm` keyword compensates for this overhead. 

4. PTM : This is for Packet Transfer Mode, another network technology often used in VDSL2 connections. PTM uses a 64b/65b encoding scheme, which effectively reduces the usable bandwidth by a small amount. The `ptm` keyword compensates for this overhead. 

5. Failsafe Overhead Keywords : The `raw` and `conservative` keywords are provided for quick-and-dirty setup. `raw` turns off all overhead compensation in CAKE, and `conservative` compensates for more overhead than is likely to occur on any widely-deployed link technology. 

6. ADSL Overhead Keywords : Most ADSL modems use ATM cell framing and have additional overhead due to the PPPoA or PPPoE protocol used. Keywords such as `pppoa-vcmux` , `pppoe-llc` , etc. are provided to account for these overheads. 

7. VDSL2 Overhead Keywords : VDSL2 uses PTM instead of ATM and may also use PPPoE. Keywords such as `pppoe-ptm` and `bridged-ptm` are provided to account for these overheads. 

8. DOCSIS Cable Overhead Keyword : DOCSIS is the standard for providing Internet service over cable-TV infrastructure. The `docsis` keyword is provided to account for the overhead of DOCSIS. 

9. Ethernet Overhead Keywords : These keywords account for the overhead of Ethernet frames, including the preamble, inter-frame gap, and Frame 1 

Check Sequence. `ethernet` and `ether-vlan` are provided for Ethernet and Ethernet with VLAN respectively​ ​.
