## 15.3 NVM Recovery Mode

NVM recovery mode is intended to recover from a misconfiguration, which can be caused by an
interrupted firmware update, power failure, host software access, or interrupted BMC configuration
access. This misconfiguration prevents firmware from executing successful initialization flows. These
flows enable the software device driver/BMC to fix the misconfiguration and cause firmware to initialize
the correct data path.
For more information on Recovery Mode, see the Recovery Mode in Intel® Ethernet Devices/Adapters
Application Note (Doc ID: 338102).

333369-009                                                                                          1191
                                 Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                           Diagnostics

NOTE:   This page intentionally left blank.

1192                                                                                       333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

Chapter 16 Glossary and Acronyms

         Term                                                           Definition

1’s complement          A system known as ones' complement can be used to represent negative numbers in a binary system.
                        The ones' complement form of a negative binary number is the bitwise NOT applied to it.

1000BASE-BX             1000BASE-BX is the PICMG 3.1 electrical specification for transmission of 1 Gb/s Ethernet or 1 Gb/s
                        fibre channel encoded data over the backplane.

1000BASE-CX             1000BASE-X over specialty shielded 150 W balanced copper jumper cable assemblies as specified in
                        IEEE 802.3 Clause 39.

1000BASE-T              1000BASE-T is the specification for 1 Gb/s Ethernet over category 5e twisted pair cables as defined in
                        IEEE 802.3 clause 40.

2’s complement          A system of two's-complement arithmetic represents negative integers by counting backwards and
                        wrapping around. Any number whose left-most bit is 1 is considered negative.

AAD                     Additional Authentication Data input, which is authenticated data that must be left un-encrypted.

ACK                     Acknowledgment

ACPI                    Advanced Configuration and Power Interface — ACPI reset is also known as D3hot-D0 transition.

AEN                     Address Enable

AER                     Advanced Error Reporting

AFE                     Analog Front End

AH                      IP Authentication Header — An IPsec header providing authentication capabilities defined in RFC 2402
                        For an example of an AH packet diagram see below:
                         • Next Header: Identifies the protocol of the transferred data.
                         • Payload Length: Size of AH packet.
                         • RESERVED: Reserved for future use (all zero until then).
                         • Security Parameters Index (SPI): Identifies the security parameters, which, in combination with the
                            IP Address, then identify the Security Association implemented with this packet.
                         • Sequence Number: Monotonically increasing number, used to prevent replay attacks.
                            Authentication Data: Contains the integrity check value (ICV) necessary to authenticate the packet;
                            it may contain padding.

AMT                     Active Management Technology (Intel® AMT)

AN                      Auto-negotiation

AN                      Association Number

APIC                    Advanced Programming Interrupt Controller

APM                     Advanced Power Management

APT                     Advanced Pass-Through mode

ARI                     Alternative Routing ID capability structure — This is a new capability that allows an interpretation of the
                        Device and Function fields as a single identification of a function within the bus.

ARI                     Alternate Requester ID Interpretation

ARP                     Address Resolution Protocol

Backbone                A bus shared by many clients for example a management backbone or a host backbone

BAR                     Base Address Register

BDF                     Bus/Device/Function

BER                     Bit Error Rate

BIOS                    Basic Input/Output System

BIST                    Built-In Self Test

333369-009                                                                                                                     1193
                                    Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Glossary and Acronyms

         Term                                                     Definition

BKM                Best Known Method

BMC                Baseboard Management Controller

BME                Bus Master Enable

BT                 Byte Time

BW (0f b/w)        Bandwidth

BWG                Bandwidth Group

Byte alignment     Implies that the physical addresses can be odd or even. Examples: 0FECBD9A1h, 02345ADC6h.

CAM                Content Addressable Memory

CCS                Current Cipher Suite

Ciphertext         Encrypted data, whose length is exactly that of the plaintext.

CNM                Congestion Notification Message

Concurrency        The concurrent (simultaneous) execution of multiple interacting computational tasks. These tasks may
                   be implemented as separate programs, or as a set of processes or threads created by a single program.

Core               Network Interface Registers

Corner case        Is a problem or situation that occurs only outside of normal operating parameters — specifically one
                   that manifests itself when multiple environmental variables or conditions are simultaneously at extreme
                   levels.
                   For example, a computer server may be unreliable, but only with the maximum complement of 64
                   processors, 512 GB of memory, and over 10,000 signed-on users. From Wiki.

CPID               Congestion Point Identifier – which should include the congestion point Ethernet MAC Address, as well
                   as a local identifier for the local congestion entity, usually a queue in the switch.

CRC                Cyclic Redundancy Check
                   A cyclic redundancy check (CRC) is a type of function that takes as input a data stream of unlimited
                   length and produces as output a value of a certain fixed size. The term CRC is often used to denote
                   either the function or the function's output. A CRC can be used in the same way as a checksum to
                   detect accidental alteration of data during transmission or storage. CRCs are popular because they are
                   simple to implement in binary hardware, are easy to analyze mathematically, and are particularly good
                   at detecting common errors caused by noise in transmission channels. From Wiki

CRS                Carrier Sense Indication

CSMA/CD            802.3 Carrier Sense Multiple Access / Collision Domain Ethernet LCI-2 Interface to an external LAN
                   Connected Device to provide wired LAN connectivity.

CSR                Control/Status Register

D0a                Active fully operational state. Once memory space is enabled all internal clocks are activated and the
D0 Active          LAN Controller enters an active state.

D0u                The D0u state is a low-power state used after PCI Reset (SPXB Reset) is de-asserted following power-up
D0 Uninitialized   (cold or warm), or on D3 exit.

D3Cold             Power Off. If Vcc is removed from the device, all of its PCI functions transition immediately to D3 cold.
                   When Power is restored a PCI Reset must be asserted.

D3Hot              In D3 the LAN Controller only responds to PCI configuration accesses and does not generate master
                   cycles.

DA                 Destination Address

DAC                Digital to Analog Converter

DAC                Dual Address Cycle messages

Data Frame         FC Frames that carry read or write data.

DBU                Data Buffer Unit

DCA                Direct Cache Access

1194                                                                                                             333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

         Term                                                          Definition

DCB                     Data Center Ethernet

DCX                     DCB Configuration Exchange protocol

DDP                     Direct Data placement

DEI                     Drop Eligible Indicator (802.1Q)

DFT                     Testability

DFX                     Design for *

DHCP                    Dynamic Host Configuration Protocol (protocol for automating the configuration of computers that use
                        TCP/IP).

DLLP                    Data Link Layer Packet /PCIe

DMA                     Direct Memory Access

DMTF NC-SI              Distributed Management Task Force
                        BMC-NIC interconnect for management.

DQ                      Descriptor Queue

Dr                      Internal Power management state when minimal function is provided (WoL, Manageability).

DSP                     Digital Signal Processor

DUT                     Device Under Test

DWORD (Double-Word)     Implies that the physical addresses may only be aligned on 4-byte boundaries, In other words, the last
alignment               nibble of the address may only end in 0, 4, 8, or Ch. For example, 0FECBD9A8h.

E-SOF                   FCoE Start of Frame

EAPOL                   Extensible Authentication Protocol over LAN

EAS                     External Architecture Specification.

ECC                     Error Correction Coding

ECRC                    End to End CRC

EDB                     End Data Bit

EEPROM                  Electrically Erasable Programmable Memory. A non-volatile memory located on the LAN controller that is
                        directly accessible from the host.

EHS                     External Heat Sink

EOP                     End-Of-Packet; when set indicates the last descriptor making up the packet.

EP                      End Point

ESN                     Extended Sequence Number

ESP                     IP Encapsulating Security Payload — An IPsec header providing encryption and authentication
                        capabilities defined in RFC 4303. The Encapsulating Security Payload (ESP) extension header provides
                        origin authenticity, integrity, and confidentiality protection of a packet. ESP also supports encryption-
                        only and authentication-only configurations, but using encryption without authentication is strongly
                        discouraged. Unlike the AH header, the IP packet header is not accounted for. ESP operates directly on
                        top of IP, using IP protocol number 50. ESP fields:
                         • Security Parameters Index (SPI): See AH
                         • Sequence Number: See AH
                         • Payload Data: See AH
                         • Padding: Used with some block ciphers to pad the data to the full length of a block.
                         • Pad Length: Size of padding in bytes.
                         • Next Header: Identifies the protocol of the transferred data.
                         • Authentication Data: Contains the data used to authenticate the packet.

EUI                     IEEE defined 64-bit Extended Unique Identifier

Extension Header        IPv6 protocol.

333369-009                                                                                                                    1195
                                      Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Glossary and Acronyms

            Term                                                  Definition

Fail-over          Fail-over is the ability to detect that the LAN connection on one port is lost, and enable the other port
                   for traffic.

FC                 Fiber Channel

FC                 Flow Control

FC Exchange        Complete Fiber Channel Read or Fiber Channel Write flow. It starts with the read or write requests by
                   the initiator (the host system) till the completion indication from the target (the remote disk).

FC Frame           Fiber Channel Frames are the smallest units sent between the initiator and the target. The FC-FS-2
                   specification defined the maximum frame size as 2112 bytes. Each Fiber Channel frame includes an FC
                   header and optional FC payload. It can also may include Extended headers and FC optional headers.
                   Extended headers are not expected in FCoE network and FC optional headers may not be used as well.

FC Sequence        A Fiber Channel Exchange is composed of multiple Fiber Channel sequences. Fiber Channel Sequence
                   can be a single or multiple frames that are sent by the initiator or the target. Each FC Sequence has a
                   unique “Sequence ID”.

FCoE               Fiber Channel over Ethernet

FCP_RSP Frame      Fiber Channel control Frames that are sent from the target to the initiator which defines the completion
                   of an FC read or write exchange.

FCS                Frame Check Sequence of Ethernet frames (also known as CRC)

FEC                Forward Error Correction

FEXT               Far End Crosstalk

Firmware (FW)      Embedded code on the LAN controller that is responsible for the implementation of the NC-SI protocol
                   and pass-through functionality.

FLR                Function level reset An OS in a VM must have complete control over a device, including its initialization,
                   without interfering with the rest of the functions.

FML                Fast Management Link

Fragment Header    An IPv6 extension Header

Frame              A unit composed of headers, data and footers that are sent or received by a device. Same as a Packet

FSM                Finite State Machine

FTS                Fast Training Sequence

GbE                Gigabit Ethernet (IEEE 802.3z-1998)

GMRP               GARP Multicast Registration Protocol (Cisco)

GPIO               General Purpose I/O

GSP                Group Strict Priority

HBA                Host Bus Adapters

Host Interface     RAM on the LAN controller that is shared between the firmware and the host. RAM is used to pass
                   commands from the host to firmware and responses from the firmware to the host.

HPC                High-Performance Computing

HT core option     Hyper Thread Intel's trademark for implementation of the simultaneous multi-threading technology on
                   the Pentium 4 micro architecture. It is a more advanced form of Super-threading that debuted on the
                   Intel Xeon processors and was later added to Pentium 4 processors. The technology improves processor
                   performance under certain workloads by providing useful work for execution units that would otherwise
                   be idle, for example during a cache miss. A Pentium 4 with Hyper-Threading enabled is treated by the
                   operating system as two processors instead of one. From Wiki

IANA               Internet Assigned Number Authority

IDS                Intrusion Detection Systems

IFCS               Insert Frame Check Sequence of Ethernet frames

IFS                Inter Frame Spacing

1196                                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

         Term                                                           Definition

IKE                      Internet Key Exchange

IOAT                     I/O Acceleration Technology

IOH                      I/O Hub

IOV                      Input Output Virtualization

IOV mode                 Operating through an IOVM or IOVI

IOVI                     I/O Virtual Intermediary: A special virtual machine that owns the physical device and is responsible for
                         the configuration of the physical device (also known as IOVM).

IOVM                     I/O Virtual Machine: A special virtual machine that owns the physical device and is responsible for the
                         configuration of the physical device (also known as IOVI).

IP — CPMP                Carrier Performance Measurement Plan

IP Tunneling             IP tunneling is the process of embedding one IP packet inside of another, for the purpose of simulating
                         a physical connection between two remote networks across an intermediate network.
                         IP tunnels are often used in conjunction with IPsec protocol to create a VPN between two or more
                         remote networks across a “hostile” network such as the Internet.

IPC                      Inter Processor Communication

IPG                      Inter Packet Gap

IPsec                    IP Security is a suite of protocols for securing Internet Protocol (IP) communications by authenticating
                         and/or encrypting each IP packet in a data stream. IPsec also includes protocols for cryptographic key
                         establishment.
                         IPsec is implemented by a set of cryptographic protocols for (1) securing packet flows and (2) internet
                         key exchange. There are two families of key exchange protocols.
                         The IP security architecture uses the concept of a security association as the basis for building security
                         functions into IP. A security association is simply the bundle of algorithms and parameters (such as
                         keys) that is being used to encrypt a particular flow. The actual choice of algorithm is left up to the
                         users. A security parameter index (SPI) is provided along with the destination address to allow the
                         security association for a packet to be looked up.
                         For multicast, therefore, a security association is provided for the group, and is duplicated across all
                         authorized receivers of the group. There may be more than one security association for a group, using
                         different SPIs, thereby allowing multiple levels and sets of security within a group. Indeed, each sender
                         can have multiple security associations, allowing authentication, since a receiver can only know that
                         someone knowing the keys sent the data. Note that the standard does not describe how the association
                         is chosen and duplicated across the group; it is assumed that a responsible party will make the choice.
                         From Wiki

iSCSI                    Internet SCSI (iSCSI) is a network protocol standard, officially ratified on 2003-02-11 by the Internet
                         Engineering Task Force, that allows the use of the SCSI protocol over TCP/IP networks. iSCSI is a
                         transport layer protocol in the SCSI-3 specifications framework. Other protocols in the transport layer
                         include SCSI Parallel Interface (SPI), Serial Attached SCSI (SAS) and Fibre Channel. From Wiki.

ISR                      Interrupt Service Routine

ITR                      Interrupt Throttling

IV                       Integrity Value

IV                       Initialization Vector

IV                       Initial Value

KaY                      Key agreement entity (KaY – in 802.1AE specification terminology) i.e. control and access the off
                         loading engine (SecY in 802.1AE specification terminology)

KVM                      Keyboard/Video/Mouse

LACP                     Link Aggregation Control Protocol

LAN auxiliary Power-Up   The event of connecting the LAN controller to a power source (occurs even before system power-up).

landing Zone             General targets for the product.
requirements

LDPC                     Low-Density Parity-check. Coding used in 802.3an (10GBASET) to protect transmitted data.

333369-009                                                                                                                     1197
                                     Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Glossary and Acronyms

          Term                                                  Definition

LF               Local Fault

LLC header       802.2 defines a special header that includes a SNAP (subnetwork access protocol) header + EtherType.
                 Some protocols, particularly those designed for the OSI networking stack, operate directly on top of
                 802.2 LLC, which provides both datagram and connection-oriented network services. This 802.2 header
                 is currently embedded in modern 802.3 frames (Ethernet II frames, aka. DIX frames).
                 The LLC header includes two additional eight-bit address fields, called service access points or SAPs in
                 OSI terminology; when both source and destination SAP are set to the value 0xAA, the SNAP service is
                 requested. The SNAP header + EtherType allows EtherType values to be used with all IEEE 802
                 protocols, as well as supporting private protocol ID spaces. In IEEE 802.3x-1997, the IEEE Ethernet
                 standard was changed to explicitly allow the use of the 16-bit field after the Ethernet MAC Addresses to
                 be used as a length field or a type field. This definition is from Wiki

LLDP             Link Layer Discovery Protocol

LLINT            Low Latency Interrupt

Local Traffic    In a virtual environment traffic between virtual machines.

LOM              LAN on Motherboard

LP               Link Partner

LS               Least significant / Lowest order (for example: LS bit = Least significant bit)

LSC              Link Status Change

LSO              Large Send Offload (also known as TSO)

LSP              Link Strict Priority

LTSSM            Link Training and Status State Machine Defined in the PCIe specs.

MAC              Media Access Control

MAUI             Multi Speed Attachment Unit Interface

MCH              Memory Controller Hub

MDC              Management Data Clock over MDC/MDIO lines.

MDI              Media Dependent Interface

MDIO             Management Data Input/Output Interface over MDC/MDIO lines.

MFVC             Multi-Function Virtual Channel Capability structure

MIB              Management Interface Bus

MIFS/MIPG        Minimum Inter Frame Spacing/Minimum Inter Packet Gap.

MMW              Maximum Memory Window

Mod / Modulo     In computing, the modulo operation finds the remainder of division of one number by another.

MPA              Marker PDU Aligned Framing for TCP.

MRQC             Multiple Receive Queues Command register

MS               Most significant / Highest order (for example: MS byte = Most significant byte)

MSFT             Microsoft®

MSI              Message Signaled Interrupt

MSS              Maximum Segment Size

MTA              Multicast Table Array

MTU              Maximum Transmission Unit

NACK             Negative Acknowledgment

native mode      Used for GPIO pin that is set to be controlled by the internal logic rather than by software.

NC-SI            Network Controller - Sideband Interface

1198                                                                                                             333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

            Term                                                           Definition

NEXT                    Near End Crosstalk

NFS                     Network File Server

NFTS                    Number of Fast Training Signals

NIC                     Network Interface Controller

Nonce                   96-bits initialization vector used by the AES-128 engine, which is distinct for each invocation of the
                        encryption operation for a fixed key. It is formed by the AES-128 SALT field stored for that IPsec flow in
                        the Tx SA Table, appended with the Initialization Vector (IV) field included in the IPsec packet:

NOS                     Network Operating System

NPRD                    Non-Posted Request Data

NRZ                     Non-return-to-Zero signaling

NSE                     No Snoop Enable

NTL                     No Touch Leakage

NTP                     Network Time Protocol

NVM                     Non Volatile Memory

OEM                     Original Equipment manufacturer

Packet                  A unit composed of headers, data and footers that are sent or received by a device. Also known as a
                        frame.

Pass Filters            Needs Definition Packets that match this type of filter continue on to their destination?

PB                      Packet Buffer

PBA                     Pending Bit Array (in MSI-X context)

PBA                     Printed Board Assembly (in NVM or board context). The nine-digit number used for Intel-manufactured
                        adapter cards.

PCS                     Physical Coding Sub-layer

PDU                     Protocol Data Units

PF                      Physical Function (in a virtualization context).

PFC                     Priority Flow Control

PHY                     Physical Layer Device

Plaintext               Data to be both authenticated and encrypted.

PMA                     Physical Medium Attachment

PMC                     Power Management Capabilities

PMD                     Physical Medium Dependent

PME                     Power Management Event

PN                      Packet Number

Pool                    Virtual ports

Power State D0a         Active fully operational state. Once memory space is enabled all internal clocks are activated and the
                        LAN Controller enters an active state.

Power State D0u         The D0u state is a low-power state used after SPXB Reset is de-asserted following power-up (cold or
                        warm), or on D3 exit.

Power State D3Cold      A Power down state with the PCI also in a power down state.

Power State D3Hot       A Power down state with the PCI continuing to receive a proper power supply.

Power State Dr          Device state when PCIe reset is asserted.

333369-009                                                                                                                    1199
                                   Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Glossary and Acronyms

         Term                                                      Definition

Power State Sx      LAN Connected Device: SMBus Active and PCI Powered down.

PPM                 Part Per Million

PRBS                Pseudo-Random Binary Sequence

PT                  Pass-Through

PTP                 Precision Time Protocol

QoS                 Quality of Service

QWORD (Quad-Word)   Implies that the physical addresses may only be aligned on 8byte boundaries; i.e., the last nibble of the
alignment           address may only end in 0, or 8. For example, 0FECBD9A8h.

RDMA                Remote Direct Memory Access

RDMAP               Remote Direct Memory Access Protocol

Receive latency     Measured from packet reception from the wire and until the descriptor is updated on PCIe.

Relax ordering      When the strict order of packets is not required, the device can send packets in an order that allows for
                    less power consumption and greater CPU efficiency.

RID                 Requester ID

RLT                 Rate-Limited flag bit

RMCP                Remote Management and Control Protocol (Distributed Management Task Force)

RMII                Reduced Media Independent Interface (Reduced MII)

RMON statistics     Remote Network Monitoring or Remote Monitoring

RPC header          Remote Procedure Call

RS                  Rate Scheduler

RSC                 Receive Side Coalescing coalesces incoming TCP/IP (and potentially UDP/IP) packets into larger receive
                    segments.

RSS                 Receive-Side Scaling is a mechanism to distribute received packets into several descriptor queues.
                    Software then assigns each queue to a different processor, therefore sharing the load of packet
                    processing among several processors.

RSTD                Reset Sequence Done

RSTI                Reset Sequence in Process

RT                  DCB (formerly ReedTown)

Rx, RX              Receive

SA                  Security Association (in IPsec context)

SA                  Source Address (in Ethernet frame context)

SAC                 Single Address Cycle (SAC) messages

SAK                 Security Associations Key

salt                In cryptography, a salt consists of random bits used as one of the inputs to a key derivation function.
                    Sometimes the initialization vector, a previously generated (preferably random) value, is used as a salt.
                    The other input is usually a password or passphrase. The output of the key derivation function is often
                    stored as the encrypted version of the password. A salt value can also be used as a key for use in a
                    cipher or other cryptographic algorithm. A salt value is typically used in a hash function. from Wiki

SAN                 Storage Area Networks

SAP                 Service Access Point — An identifying label for network endpoints used in OSI networking.

SC                  Secure Channel — Authentication and key exchange.

SC                  Secure Channel (SC) — A security relationship used to provide security guarantees for frames
                    transmitted from one member of a CA to the others. An SC is supported by a sequence of SAs thus
                    allowing the periodic use of fresh keys without terminating the relationship.

1200                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

           Term                                                          Definition

SCI                      Secure Channel Identifier — A globally unique identifier for a secure channel, comprising a globally
                         unique Ethernet MAC Address and a Port Identifier, unique within the system allocated that address.

SCL signal               SM Bus Clock

SCSI                     Small Computer System Interface is a set of standards for physically connecting and transferring data
                         between computers and peripheral devices. The SCSI standards define commands, protocols, and
                         electrical and optical interfaces. SCSI is most commonly used for hard disks and tape drives, but it can
                         connect a wide range of other devices, including scanners, and optical drives (CD, DVD, etc. From Wiki.

SCTP                     Stream Control Transmission Protocol

SDA signal               SM Bus Data

SDP                      Software-Definable Pins

SecY                     802.1AE specification terminology Security entity

Segment                  Subsections of a packet.

SerDes                   Serializer and De-Serializer Circuit

SFD                      Start Frame Delimiter

SFI                      Serial Flash Interface

SGMII                    Serialized Gigabit Media Independent Interface

SKU                      Subsets of features of a chip that can be disabled for marketing purposes

SMB                      Semaphore Bit

SMBus                    System Management Bus — A bus that carries various manageability components, including the LAN
                         controller, BIOS, sensors and remote-control devices.

SN                       Sequence Number — Contains a counter value that increases by one for each Ethernet frame sent.

SNAP                     Subnetwork Access Protocol

SNMP                     Standard Network Management Protocol

SoL                      Serial Over LAN — A mechanism that enables the input and output of the serial port of a managed
                         system to be redirected via an IPMI (Internet Protocol Multicast Initiative) session over IP.

SPD                      Smart Power Down

SPI                      The Security Parameter Index is an identification tag added to the header while using IPsec for
                         tunneling the IP traffic. This tag helps the kernel discern between two traffic streams where different
                         encryption rules and algorithms may be in use.
                         The SPI (as per RFC 2401) is an essential part of an IPsec SA (Security Association) because it enables
                         the receiving system to select the SA under which a received packet is processed. An SPI has only local
                         significance, since is defined by the creator of the SA; an SPI is generally viewed as an opaque bit
                         string. However, the creator of an SA may interpret the bits in an SPI to facilitate local processing. from
                         Wikipedia

Spoofing                 In computer networking, the term IP Address spoofing is the creation of IP packets with a forged
                         (spoofed) source IP Address with the purpose to conceal the identity of the sender or impersonating
                         another computing system. IP stands for Internet Protocol. from Wiki

SPXB interface           PCI Express Backbone

SR-IOV                   PCI-SIG single-root I/O Virtualization initiative

SW Switch acceleration   Central management of the networking resources by an IOVM or by the VMM. Also known as VMDq2
mode                     mode.

SWIZZLE                  To convert external names, array indices, or references within a data structure into address pointers
                         when the data structure is brought into main memory from external storage (also called pointer
                         swizzling);

Sx                       LAN Connected Device: SMBus Active and PCI Powered down.

SYN Attack               A SYN attack is a form of denial-of-service attack in which an attacker sends a succession of SYN
                         (synchronize) requests to a target's system.

333369-009                                                                                                                      1201
                                    Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Glossary and Acronyms

         Term                                                     Definition

TC                 Traffic Class

TCI                For 802.1q, Tag Header field Tag Control Information (TCI); 2 octets.

TCO                Total Cost of Ownership (Management)

TCP/IP             Transmission Control Protocol/Internet Protocol

TDESC              Transmit Descriptor

TDP                Total Device Power

TDR                Time Domain Reflectometry

TFCS               Transmit Flow Control Status

TLP                Transaction layer Packets

ToS                Type of Service

TPID               For 802.1q, Tag Header field Tag Protocol Identifier; 2 octets.

TPPAC              Transmit Packet Plane Arbitration Control

Transmit latency   Measured from Tail update until the packet is transmitted on the wire. It is assumed that a single packet
                   is submitted for this traffic class and its latency is then measured in presence of traffic belonging to
                   other traffic classes.

TS                 Time Stamp

TSO                TCP or Transmit Segmentation offload — A mode in which a large TCP/UDP I/O is handled to the device
                   and the device segments it to L2 packets according to the requested MSS.

TSS                Transmit Side Scaling

Tx, TX             Transmit

UBWG               User Bandwidth Group

ULP                Upper Layer Protocol

UP                 User Priority

UR                 Error Reporting Unsupported Request Error

VF                 Virtual Function – A part of a PF assigned to a VI

VI                 Virtual Image – A virtual machine to which a part of the I/O resources is assigned. Also known as a VM.

VM                 Virtual Machine

VMDq2              SW switch acceleration mode — Central management of the networking resources by an IOVM or by the
                   VMM.
                   Virtual Machine Devices queue (VMDq) is a mechanism to share I/O resources among several
                   consumers. For example, in a virtual system, multiple OSs are loaded and each executes as though
                   the whole system’s resources were at its disposal. However, for the limited number of I/O devices, this
                   presents a problem because each OS may be in a separate memory domain and all the data movement
                   and device management has to be done by a VMM (Virtual Machine Monitor). VMM access adds latency
                   and delay to I/O accesses and degrades I/O performance. VMDs (Virtual Machine Devices) are designed
                   to reduce the burden of VMM by making certain functions of an I/O device shared and thus can be
                   accessed directly from each guest OS or Virtual Machine (VM). From Nahum

VMM                Virtual Machine Monitor

VPD                Vital Product Data (PCI protocol).

VT                 Virtualization

WB                 Write Back

WC                 Worst Case

WoL                Wake-on-LAN Now called APM Wake-up or Advanced power management Wake-up.

1202                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Glossary and Acronyms

         Term                                                         Definition

WORD alignment          Implies that physical addresses must be aligned on even boundaries; i.e., the last nibble of the address
                        may only end in 0, 2, 4, 6, 8, Ah, Ch, or Eh. For example, 0FECBD9A2h.

WRR                     Weighted Round-Robin

WSP                     Weighted Strict Priority

XAUI                    10 Gigabit Attachment Unit Interface

XFI                     Serial Interface that can connect to other devices supporting XFI

XFP                     10 Gigabit Small Form Factor Pluggable modules

XGMII                   10 Gigabit Media Independent Interface

XGXS                    XGMII Extender Sub layer

XMT                     Transmit

333369-009                                                                                                                  1203
                                   Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                               Glossary and Acronyms

NOTE:   This page intentionally left blank.

1204                                                                                       333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

Appendix A Packet Formats

A.1            Legacy Packet Formats

A.1.1             ARP Packet Formats

A.1.1.1               ARP Request Packet

     Offset      # of Bytes                         Field                         Value             Action

0                    6        Destination Address                                                   Compare

6                    6        Source Address                                                        Stored

    12 E=(0/4/6/8)   Outer Tag (Outer VLAN, E-tag)             0x8100 ****                 Ignore

                                                                        0x893F ************

12 + E            S=(0/4)     Possible VLAN Tag                                                     Stored

12 + E + S           2        Type                                      0x0806                      Compare

14 + E + S           2        Hardware Type                             0001                        Compare

16 + E + S           2        Protocol Type                             0x0800                      Compare

18 + E + S           1        Hardware Size                             06                          Compare

19 + E + S           1        Protocol Address Length                   04                          Compare

20 + E + S           2        Operation                                 0001                        Compare

22 + E + S           6        Sender Hardware Address                   -                           Stored

28 + E + S           4        Sender IP Address                         -                           Stored

32 + E + S           6        Target Hardware Address                   -                           Ignore

38 + E + S           4        Target IP Address                         ARP IP Address              Compare

A.1.1.2               ARP Response Packet

     Offset      # of Bytes                         Field                                 Value

0                    6        Destination Address                      ARP Request Source Address

6                    6        Source Address                           Programmed from NVM or BMC

    12 E=(0/4/6/8)   Outer Tag (Outer VLAN, E-tag)

12 + E            S=(0/4)     Possible VLAN Tag                        From ARP Request

12 + E + S           2        Type                                     0x0806

14 + E + S           2        Hardware Type                            0x0001

16 + E + S           2        Protocol Type                            0x0800

18 + E + S           1        Hardware Size                            0x06

19 + E + S           1        Protocol Address Length                  0x04

333369-009                                                                                                    1205
                                  Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                         Packet Formats

       Offset        # of Bytes                            Field                               Value

20 + E + S               2           Operation                               0x0002

22 + E + S               6           Sender Hardware Address                 Programmed from NVM or BMC

28 + E + S               4           Sender IP Address                       Programmed from NVM or BMC

32 + E + S               6           Target Hardware Address                 ARP Request Sender Hardware Address

38 + E + S               4           Target IP Address                       ARP Request Sender IP Address

A.1.1.3                   Gratuitous ARP Packet

        Offset         # of Bytes                                  Field                                 Value

0                            6         Destination Address                                      Broadcast address.

6                            6         Source Address

    12 E=(0/4/6/8)     Outer Tag (Outer VLAN, E-tag)

12 + E                   S=(0/4)       Possible VLAN Tag

12 + E + S               D=(0/8)       Possible Length + LLC/SNAP Header

12 + E + S + D               2         Type                                                     0x0806

14 + E + S + D               2         Hardware Type                                            0x0001

16 + E + S + D               2         Protocol Type                                            0x0800

18 + E + S + D               1         Hardware Size                                            0x06

19 + E + S + D               1         Protocol Address Length                                  0x04

20 + E + S + D               2         Operation                                                0x0001

22 + E + S + D               6         Sender Hardware Address

28 + E + S + D               4         Sender IP Address

32 + E + S + D               6         Target Hardware Address

38 + E + S + D               4         Target IP Address

A.1.2                  IP and TCP/UDP Headers for TSO
This section outlines the format and content for the IP, TCP and UDP headers. The X550 requires
baseline information from the device driver to construct the appropriate header information during the
segmentation process.
Header fields that are modified by the X550 are highlighted in the figures below.
Note:           The IP header is first shown in the traditional (i.e. RFC 791) representation, and because byte
                and bit ordering is confusing in that representation, the IP header is also shown in Little
                Endian format. The actual data is fetched from memory in Little Endian format.

1206                                                                                                          333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

                                                   1   1   1    1      1   1   1     1     1     1     2    2    2   2    2   2    2    2   2      2   3    3
 0   1     2   3     4   5    6     7    8   9     0   1   2    3      4   5   6     7     8     9     0    1    2   3    4   5    6    7   8      9   0    1

     Version         IP Hdr Length                TYPE of service                              Total length (IP header + payload length)

                               Identification                                      Flags                              Fragment Offset

            Time to Live                         Layer 4 Protocol ID                                            Header Checksum

                                                                     Source Address

                                                                 Destination Address

                                                                           Options

Figure A-1.          IPv4 Header (Traditional Representation - Most Left Byte First On the Wire)

               Byte 3                                  Byte 2                                   Byte 1                                  Byte 0

 7   6     5   4     3   2    1     0    7   6     5   4   3    2      1   0   7     6     5     4     3    2    1   0    7   6    5    4   3      2   1    0

                                  Total length
                                                                                           TYPE of service                    Version       IP Hdr Length
               LSB                                      MSB

                                         R
                                             N     M    Fragment Offset                                           Identification
      Fragment Offset Low                E
                                             F     F         High                                LSB                                      MSB
                                         S

                             Header Checksum
                                                                                         Layer 4 Protocol ID                       Time to Live
               LSB                                      MSB

                                                                     Source Address
               LSB                                                                                                                        MSB

                                                                 Destination Address
               LSB                                                                                                                        MSB

                                                                           Options

Figure A-2.          IPv4 Header (Little Endian Order - Byte 0 First On the Wire)

Identification is increased on each packet.
Flags Field Definitions:
The Flags field is defined below. Note that hardware does not evaluate or change these bits.
 • MF - More Fragments
 • NF - No Fragments
 • Reserved
The X550 does TCP segmentation, not IP Fragmentation. IP Fragmentation may occur in transit through
a network's infrastructure.

                                                   1   1   1    1      1   1   1     1     1     1     2    2    2   2    2   2    2    2   2      2   3    3
 0   1     2   3     4   5    6     7    8   9     0   1   2    3      4   5   6     7     8     9     0    1    2   3    4   5    6    7   8      9   0    1

     Version             Priority                                                              Flow Label

         Payload Length (excluding the IP header length)                                 Next Header Type                              Hop Limit

                                                                     Source Address
               LSB                                                                                                                        MSB

                                                                 Destination Address
               LSB                                                                                                                        MSB

                                                                    Extensions (if any)

Figure A-3.          IPv6 Header (Traditional Representation - Most Left Byte First On the Wire)

333369-009                                                                                                                                                 1207
                                             Did this document help answer your questions?

                                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                                    Packet Formats

                Byte 3                                  Byte 2                                    Byte 1                               Byte 0

 7     6   5    4     3    2    1    0    7    6    5   4   3     2    1     0   7      6     5   4   3    2    1    0   7     6   5   4   3     2   1     0

                                                    Source Address
                                                                                                                             Version            Priority
                 LSB                                                                               MSB

                                                                                            Payload Length (excluding the IP header length)
               Hop Limit                           Next Header Type
                                                                                                  LSB                            MSB

                                                                       Source Address
                LSB                                                                                                                     MSB

                                                                   Destination Address
                LSB                                                                                                                     MSB

                                                                           Extensions

Figure A-4. IPv6 Header (Little Endian Order - Byte 0 First On the Wire)

A TCP or UDP frame uses a 16-bit wide one's complement checksum. The checksum word is computed
on the outgoing TCP or UDP header and payload, and on the Pseudo Header. Details on checksum
computations are provided in Section 7.2.4.6.
Note:          TCP and UDP over IPv6 requires the use of checksum, where it is optional for UDP over IPv4.
Note:          The TCP header is first shown in the traditional (i.e. RFC 793) representation, and because
               byte and bit ordering is confusing in that representation, the TCP header is also shown in
               Little Endian format. The actual data is fetched from memory in Little Endian format.

                                                    1   1   1     1    1     1   1      1     1   1   2    2    2    2   2     2   2   2   2     2   3     3
 0     1   2    3     4    5    6    7    8    9    0   1   2     3    4     5   6      7     8   9   0    1    2    3   4     5   6   7   8     9   0     1

                                 Source Port                                                                   Destination Port

                                                                      Sequence Number

                                                                 Acknowledgment Number

                                                    U   A   P     R    S     F
  TCP Header
                               Reserved             R   C   S     S    Y     I                                      Window
    Length
                                                    G   K   H     T    N     N

                                    Checksum                                                                   Urgent Pointer

                                                                            Options

Figure A-5. TCP Header (Traditional Representation)

                Byte 3                                  Byte 2                                    Byte 1                               Byte 0

 7     6   5    4     3    2    1    0    7    6    5   4   3     2    1     0   7      6     5   4   3    2    1    0   7     6   5   4   3     2   1     0

                               Destination Port                                                                  Source Port

                                                                      Sequence Number
                LSB                                                                                                                     MSB

                                                                 Acknowledgment Number

                                                                                              U   A   P    R    S    F
                                                                                                                         TCP Header
                                    Window                                        RES         R   C   S    S    Y    I                          Reserved
                                                                                                                           Length
                                                                                              G   K   H    T    N    N

                                Urgent Pointer                                                                      Checksum

                                                                            Options

Figure A-6. TCP Header (Little Endian)

1208                                                                                                                                            333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

The TCP header is always a multiple of 32-bit words. TCP options may occupy space at the end of the
TCP header and are a multiple of 8 bits in length. All options are included in the checksum.
The checksum also covers a 96-bit pseudo header prefixed to the TCP Header (see Figure A-7 below).
For IPv4 packets, this pseudo header contains the IP Source Address, the IP Destination Address, the IP
Protocol field, and TCP Length. Software pre-calculates the partial pseudo header sum, that includes
IPv4 SA, DA and protocol types, but NOT the TCP length, and stores this value into the TCP Checksum
field of the packet. For both IPv4 and IPv6, hardware needs to factor in the TCP length to the software
supplied pseudo header partial checksum.
Note:        When calculating the TCP pseudo header, the byte ordering can be tricky. One common
             question is whether the Protocol ID field is added to the “lower” or “upper” byte of the 16-bit
             sum. The Protocol ID field should be added to the least significant byte (LSB) of the 16-bit
             pseudo header sum, where the most significant byte (MSB) of the 16-bit sum is the byte that
             corresponds to the first checksum byte out on the wire.
The TCP Header Length field is the TCP header length including option fields plus the data length in
bytes, which is calculated by hardware on a frame-by-frame basis. The TCP Length does not count the
12 bytes of the pseudo header. The TCP length of the packet is determined by hardware as:
TCP Length = min(MSS,PAYLOADLEN) + L5_LEN
The two flags that may be modified are defined as:
 • PSH — Receiver should pass this data to the app without delay.
 • FIN — Sender is finished sending data.
The handling of these flags is described in Section 7.2.4.7.
“Payload” is normally MSS except for the last packet where it represents the remainder of the payload.

                                                IPv4 Source Address

                                              IPv4 Destination Address

                  Zero                           Layer 4 Protocol ID                TCP/UDP Length

Figure A-7.      TCP/UDP Pseudo Header Content for IPv4 (Traditional Representation)

                                                IPv6 Source Address

                                            IPv6 Final Destination Address

                                               TCP/UDP Packet Length

                                    Zero                                              Next Header

Figure A-8.      TCP/UDP Pseudo Header Content for IPv6 (Traditional Representation)

Notes:       From RFC2460:
      • If the IPv6 packet contains a Routing header, the Destination Address used in the pseudo-
        header is that of the final destination. At the originating node, that address is in the last
        element of the Routing header; at the recipient(s), that address is in the Destination Address
        field of the IPv6 header.
      • The Next Header value in the pseudo-header identifies the upper-layer protocol (e.g., 6 for TCP,
        or 17 for UDP). It differs from the Next Header value in the IPv6 header if there are extension
        headers between the IPv6 header and the upper-layer header.

333369-009                                                                                              1209
                                  Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                                      Packet Formats

 • The Upper-Layer Packet Length in the pseudo-header is the length of the upper-layer header and
   data (e.g., TCP header plus TCP data). Some upper-layer protocols carry their own length
   information (e.g., the Length field in the UDP header); for such protocols, that is the length used in
   the pseudo- header. Other protocols (such as TCP) do not carry their own length information, in
   which case the length used in the pseudo-header is the Payload Length from the IPv6 header, minus
   the length of any extension headers present between the IPv6 header and the upper-layer header.
           • Unlike IPv4, when UDP packets are originated by an IPv6 node, the UDP checksum is not
             optional. That is, whenever originating a UDP packet, an IPv6 node must compute a UDP
             checksum over the packet and the pseudo-header, and, if that computation yields a result of
             zero, it must be changed to hex FFFF for placement in the UDP header. IPv6 receivers must
             discard UDP packets containing a zero checksum, and should log the error.
A type 0 Routing header has the following format:

                                                           Routing Type           Segments Left
       Next Header               Hdr Ext Len
                                                                “0”                   “n”

                                                Reserved

                                                Address[1]

                                                Address[2]

                                                     …

                                      Final Destination Address [n]

Figure A-9. IPv6 Routing Header (Traditional Representation)

 • Next Header — 8-bit selector. Identifies the type of header immediately following the Routing
   header. Uses the same values as the IPv4 protocol field [RFC-1700 et seq.].
 • Hdr Ext Len — 8-bit unsigned integer. Length of the Routing header in 8-octet units, not including
   the first 8 octets. For the Type 0 Routing header, Hdr Ext Len is equal to two times the number of
   addresses in the header.
 • Routing Type — 0.
 • Segments Left — 8-bit unsigned integer. Number of route segments remaining (i.e., number of
   explicitly listed intermediate nodes still to be visited before reaching the final destination). Equal to
   “n” at the source node.
 • Reserved — 32-bit reserved field. Initialized to zero for transmission; ignored on reception.
 • Address[1...n] — Vector of 128-bit addresses, numbered 1 to n.
The UDP header is always 8 bytes in size with no options.

                                                 1   1   1    1   1   1   1   1    1   1   2   2    2    2   2     2   2   2   2   2   3   3
 0     1     2   3   4   5   6    7     8   9    0   1   2    3   4   5   6   7    8   9   0   1    2    3   4     5   6   7   8   9   0   1

                             Source Port                                                           Destination Port

                                 Length                                                                 Checksum

Figure A-10. UDP Header (Traditional Representation)

1210                                                                                                                               333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

             Byte 3                               Byte 2                           Byte 1                            Byte 0

 0   1   2   3   4    5    6    7   0     1   2   3   4    5   6   7   0   1   2   3   4    5   6   7   0    1   2   3   4    5   6    7

                          Destination Port                                                      Source Port

                               Checksum                                                             Length

Figure A-11. UDP Header (Little Endian Order)

UDP pseudo header has the same format as the TCP pseudo header. The pseudo header prefixed to the
UDP header contains the IPv4 source address, the IPv4 destination address, the IPv4 protocol field, and
the UDP length (same as the TCP Length discussed above). This checksum procedure is the same as is
used in TCP.
Unlike the TCP checksum, the UDP checksum is optional (for IPv4). Software must set the TXSM bit in
the TCP/IP Context Transmit Descriptor to indicate that a UDP checksum should be inserted. Hardware
does not overwrite the UDP checksum unless the TXSM bit is set.

A.1.3                 Magic Packet
The Magic Packet is a broadcast frame, but could also be a Multicast or Unicast Ethernet MAC
Addresses. The X550 accepts this packet if it matches any of its pre-programmed Ethernet MAC
Addresses. Magic packet can be sent over a variety of connectionless protocols (usually UDP or IPX).
The Magic packet pattern is composed of the following sequences:
 • Synchronization stream composed of 6 bytes equal to 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF
 • Unique pattern composed of 16 times the end node Ethernet MAC Address. The X550 expect for the
   Ethernet MAC Address stored in the RAL[0] and RAH[0] registers.
The X550 looks for the synchronization pattern and the sequence of 16 Ethernet MAC Addresses. It
does not check the packet content and the length of the header that precedes the magic pattern nor
any data that follows it.

A.2              Packet Types for Packet Split Filtering
The following packet types are supported by the 'Packet Split' feature in the X550. This section
describes the packets from the 'split-header' point of view. This means that when describing the
different fields that are checked and compared, it emphasizes only the fields that are needed to
calculate the header length. This document describes the checks that are done after the decision to
pass the packet to the host memory was done.
Terminology:
 • Compare — The field values are compared and must be exactly equal to the value specified in this
   document.
 • Checked — The field values are checked for calculation (header length …).
 • Ignore — The field values are ignored but the field is counted as part of the header.

333369-009                                                                                                                            1211
                                          Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                       Packet Formats

A.2.1             Type 1.1: Ethernet (VLAN/SNAP) IP packets

A.2.1.1               Type 1.1: Ethernet, IP, Data
This type contains only Ethernet header and IPv4 header while the payload header of the IP is not IPv6/
TCP/UDP.

     Offset   # of Bytes               Field                  Value        Action                Comment

0                 6         Destination Address                            Ignore    MAC Header – Processed by main
                                                                                     address filter, or broadcast.

6                 6         Source Address                                 Ignore

    12 D=(0/4/6/8)   Outer Tag                0x8100 ****           Ignore

                            (Outer VLAN, E-Tag)      0x893F ************

12+D           S=(0/4)      Possible VLAN Tag        0x8100 ****           Compare

12+D+S         D=(0/8)      Possible Length + LLC/                         Compare
                            SNAP Header

12+D+S            2         Type                     0800h                 Compare   IP

                                                         IPv4 Header

14+D+S            1         Version/ HDR length      0x4X                  Compare   Check IPv4 and header length.

15+D+S            1         Type of Service          -                     Ignore

16+D+S            2         Packet Length            -                     Ignore

18+D+S            2         Identification           -                     Ignore

20+D+S            2         Fragment Info            >0 or                  Check    Check that the packet is fragmented.
                                                     MF bit is set

22+D+S            1         Time to live             -                     Ignore

23+D+S            1         Protocol                                       Ignore    Has no meaning if the packet is
                                                                                     fragmented.

24+D+S            2         Header Checksum          -                     Ignore

26+D+S            4         Source IP Address        -                     Ignore

30+D+S            4         Destination IP Address   -                     Ignore

34+D+S            N         Possible IP Options                            Ignore

1212                                                                                                          333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.2.1.2                Type 1.2: Ethernet (SNAP/VLAN), IPv4, UDP
This type contains only Ethernet header, IPv4 header, and UDP header.

     Offset    # of Bytes              Field                  Value        Action                  Comment

0                  6        Destination Address                            Ignore    MAC Header – Processed by main
                                                                                     address filter, or broadcast filter.

6                  6        Source Address                                 Ignore

    12 D=(0/4/6/8)   Outer Tag                0x8100 ****           Ignore

                            (Outer VLAN, E-tag)      0x893F ************

12+D            S=(0/4)     Possible VLAN Tag        0x8100 ****            Check

12+D+S             2        Type                     0x0800                Compare   IP

                                                         IP Header

14+D+S             1        Version/ HDR length      0x4X                  Compare   Check IPv4 and header length.

15+D+S             1        Type of Service          -                     Ignore

16+D+S             2        Packet Length            -                     Ignore

18+D+S             2        Identification           -                     Ignore

20+D+S             2        Fragment Info            (xx00)                Compare
                                                     0x000

22+D+S             1        Time to live             -                     Ignore

23+D+S             1        Protocol                 0x11                  Compare   UDP header.

24+D+S             2        Header Checksum          -                     Ignore

26+D+S             4        Source IP Address        -                     Ignore

30+D+S             4        Destination IP Address   -                     Ignore

34+D+S             N        Possible IP Options                            Ignore

                                                         UDP Header

34+D+S+N           2        Source Port              Not (0x801)            Check    Not NFS packet.

36+D+S+N           2        Destination Port         Not (0x801)            Check    Not NFS packet.

38+D+S+N           2        Length                   -                     Ignore

40+D+S+N           2        Checksum                 -                     Ignore

In this case, the packet is split after (42+D+S+N) bytes.

333369-009                                                                                                              1213
                                     Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                       Packet Formats

A.2.1.3                 Type 1.3: Ethernet (VLAN/SNAP) IPv4 TCP
This type contains only Ethernet header, IPv4 header, and TCP header.

     Offset   # of Bytes               Field                  Value        Action                  Comment

0                 6         Destination Address                            Ignore    MAC Header – Processed by main
                                                                                     address filter, or broadcast filter.

6                 6         Source Address                                 Ignore

    12 D=(0/4/6/8)   Outer Tag                0x8100 ****           Ignore

                            (Outer VLAN, E-tag)      0x893F ************

12+D           S=(0/4)      Possible VLAN Tag        0x8100 ****            Check

12+D+S            2         Type                     0x0800                Compare   IP

                                                         IPv4 Header

14+D+S            1         Version/ HDR length      0x4X                  Compare   Check IPv4 and header length.

15+D+S            1         Type of Service          -                     Ignore

16+D+S            2         Packet Length            -                     Ignore

18+D+S            2         Identification           -                     Ignore

20+D+S            2         Fragment Info            0x00                  Compare

22+D+S            1         Time to live             -                     Ignore

23+D+S            1         Protocol                 0x06                  Compare   TCP header.

24+D+S            2         Header Checksum          -                     Ignore

26+D+S            4         Source IP Address        -                     Ignore

30+D+S            4         Destination IP Address   -                     Ignore

34+D+S            N         Possible IP Options                            Ignore

                                                         TCP Header

34+D+S+N          2         Source Port              Not (0x801)            Check    Not NFS packet.

36+D+S+N          2         Destination Port         Not (0x801)            Check    Not NFS packet.

38+D+S+N          4         Sequence number          -                     Ignore

42+D+S+N          4         Acknowledge number       -                     Ignore

46+D+S+N         1/2        Header Length                                   Check

46.5+D+S+         1.5       Different bits           -                     Ignore
N

48+D+S+N          2         Window size              -                     Ignore

50+D+S+N          2         TCP checksum             -                     Ignore

52+D+S+N          2         Urgent pointer           -                     Ignore

54+D+S+N          F         TCP options              -                     Ignore

In this case, the packet is split after (54+D+S+N+F) bytes.
 • N = (IP HDR length -5) * 4.
 • F = (TCP header length - 5) * 4.

1214                                                                                                            333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.2.1.4                  Type 1.4: Ethernet IPv4 IPv6

A.2.1.4.1                  IPv6 Header Options Processing

This type of processing looks at the next-header field and header length to determine the identity of the
next-header processes, the IPv6 options, and it's length.
If the next header in the IPv6 header is equal to 0x00/0x2B/0x2C/0x3B/0x3c it means that the next
header is an IPv6 option header and this is its structure:

               N e x t H e a d e r (8 b it)   H e a d e r L e n (8 b it)
                                                      O p tio n H e a d e r P a ra m e te rs

Header Len determines the length of the header while the next header field determines the identity of
the next header (should be any IPv6 extension header for another IPv6 header option).

A.2.1.4.2                  IPv6 Next Header Values

When parsing an IPv6 header, the X550 does not parse all possible extension headers. If there is an
extension header that is not supported by the X550, the packet is treated as an unknown payload after
the IPv6 header.

       Value                            Header Type

       0x00            Hop by Hop

       0x2B            Routing

       0x2C            Fragment

       0x3B            No next header (EOL)

       0x3C            Destination option header

The next header in a fragment header is ignored and this extension header is expected to be the last
header.

333369-009                                                                                           1215
                                          Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                            Packet Formats

A.2.1.4.3              Type 1.4.1: Ethernet IPv4 IPv6 Data

This type contains only Ethernet header, IPv4 header, and IPv6 header.

     Offset   # of Bytes               Field                    Value           Action                  Comment

0                 6         Destination Address                                 Ignore    MAC Header – Processed by main
                                                                                          address filter, or broadcast filter.

6                 6         Source Address                                      Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****              Ignore

                            (Outer VLAN, E-tag)        0x893F ************

12+D           S=(0/4)      Possible VLAN Tag          0x8100                    Check

12+D+S            2         Type                       0x0800                   Compare   IP

                                                           IPv4 Header

14+D+S            1         Version/ HDR length        0x4X                     Compare   Check IPv4 and header length.

15+D+S            1         Type of Service            -                        Ignore

16+D+S            2         Packet Length              -                        Ignore

18+D+S            2         Identification             -                        Ignore

20+D+S            2         Fragment Info              0x00                     Compare

22+D+S            1         Time to live               -                        Ignore

23+D+S            1         Protocol                   0x29                     Compare   IPv6

24+D+S            2         Header Checksum            -                        Ignore

26+D+S            4         Source IP Address          -                        Ignore

30+D+S            4         Destination IP Address     -                        Ignore

34+D+S            N         Possible IP Options                                 Ignore

                                                           IPv6 Header

34+D+S+N          1         Version/ Traffic Class     0x6X                     Compare   Check IPv6.

35+D+S+N          3         Traffic Class/Flow Label   -                        Ignore

38+D+S+N          2         Payload Length             -                        Ignore

40+D+S+N          1         Next Header                IPv6 extension headers    Check

41+D+S+N          1         Hop Limit                  -                        Ignore

42+D+S+N          16        Source Address             -                        Ignore

48+D+S+N          16        Destination Address                                 Ignore

74+D+S+N          B         Possible IPv6 Next         -                        Ignore
                            Headers

In this case the packet is split after (74+D+S+N+B) bytes.
 • N = (IP HDR length - 5) * 4.
 • One of the extension headers of the IPv6 packets must be a “fragment header” for the packet to be
   parsed.

1216                                                                                                                 333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.2.1.4.4                Type 1.4.2: Ethernet (VLAN/SNAP) IPv4 IPv6 UDP

This type contains only Ethernet header, IPv4 header, IPv6 header and UDP header.

     Offset     # of Bytes              Field                    Value          Action                  Comment

0                   6        Destination Address                                Ignore    MAC Header – Processed by main
                                                                                          address filter, or broadcast filter.

6                   6        Source Address                                     Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****             Ignore

                             (Outer VLAN, E-tag)        0x893F ************

12+D             S=(0/4)     Possible VLAN Tag          0x8100                   Check

12+D+S              2        Type                       0x0800                  Compare   IP

                                                        IPv4 Header

14+D+S              1        Version/ HDR length        0x4X                    Compare   Check IPv4 and header length.

15+D+S              1        Type of Service            -                       Ignore

16+D+S              2        Packet Length              -                       Ignore

18+D+S              2        Identification             -                       Ignore

20+D+S              2        Fragment Info              0x00                    Compare

22+D+S              1        Time to live               -                       Ignore

23+D+S              1        Protocol                   0x29                    Compare   IPv6

24+D+S              2        Header Checksum            -                       Ignore

26+D+S              4        Source IP Address          -                       Ignore

30+D+S              4        Destination IP Address     -                       Ignore

34+D+S              N        Possible IP Options                                Ignore

                                                        IPv6 Header

34+D+S+N            1        Version/ Traffic Class     0x6X                    Compare   Check IPv6.

35+D+S+N            3        Traffic Class/Flow Label   -                       Ignore

38+D+S+N            2        Payload Length             -                       Ignore

40+D+S+N            1        Next Header                IPv6 extension header    Check    IPv6 extension headers.
                                                        or 0x11

41+D+S+N            1        Hop Limit                  -                       Ignore

42+D+S+N            16       Source Address             -                       Ignore

58+D+S+N            16       Destination Address                                Ignore

74+D+S+N            B        Possible IPv6 Next         -                       Ignore
                             Headers

                                                        UDP Header

74+D+S+N+B          2        Source Port                Not (0x801)              Check    Not NFS packet.

76+D+S+N+B          2        Destination Port           Not (0x801)              Check    Not NFS packet.

78+D+S+N+B          2        Length                     -                       Ignore

80+D+S+N+B          2        Checksum                   -                       Ignore

In this case the packet is split after (82+D+S+N+B) bytes.
N = (IP HDR length - 5) * 4.

333369-009                                                                                                                 1217
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Packet Formats

A.2.1.4.5               Type 1.4.3: Ethernet (VLAN/SNAP) IPv4 IPv6 TCP

This type contain only Ethernet header, IPv4 header, IPv6 header and TCP header.

     Offset   # of Bytes               Field                    Value          Action                  Comment

0                 6         Destination Address                                Ignore    MAC Header – Processed by main
                                                                                         address filter, or broadcast filter.

6                 6         Source Address                                     Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****             Ignore

                            (Outer VLAN, E-tag)        0x893F ************

12+D           S=(0/4)      Possible VLAN Tag          0x8100                   Check

12+D+S            2         Type                       0x0800                  Compare   IP

                                                           IPv4 Header

14+D+S            1         Version/ HDR length        0x4X                    Compare   Check IPv4 and header length

15+D+S            1         Type of Service            -                       Ignore

16+D+S            2         Packet Length              -                       Ignore

18+D+S            2         Identification             -                       Ignore

20+D+S            2         Fragment Info              0x00                    Compare

22+D+S            1         Time to live               -                       Ignore

23+D+S            1         Protocol                   0x2A                    Compare   IPv6

24+D+S            2         Header Checksum            -                       Ignore

26+D+S            4         Source IP Address          -                       Ignore

30+D+S            4         Destination IP Address     -                       Ignore

34+D+S            N         Possible IP Options                                Ignore

                                                           IPv6 Header

34+D+S+N          1         Version/ Traffic Class     0x6X                    Compare   Check IPv6

35+D+S+N          3         Traffic Class/Flow Label   -                       Ignore

38+D+S+N          2         Payload Length             -                       Ignore

40+D+S+N          1         Next Header                IPv6 extension header    Check    IPv6 extension headers
                                                       Or 0x06

41+D+S+N          1         Hop Limit                  -                       Ignore

42+D+S+N          16        Source Address             -                       Ignore

58+D+S+N          16        Destination Address                                Ignore

74+D+S+N          B         Possible IPv6 Next         -                       Ignore
                            Headers

                                                           TCP Header

74+T              2         Source Port                Not (0x801)              Check    Not NFS packet

76+T              2         Destination Port           Not (0x801)              Check    Not NFS packet

78+T              4         Sequence number            -                       Ignore

82+T              4         Acknowledge number         -                       Ignore

86+T             1/2        Header Length                                       Check

86.5+T            1.5       Different bits             -                       Ignore

1218                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

     Offset    # of Bytes            Field                      Value           Action                  Comment

88+T               2        Window size                -                        Ignore

90+T               2        TCP checksum               -                        Ignore

92+T               2        Urgent pointer             -                        Ignore

94+T               F        TCP options                -                        Ignore

In this case the packet is split after (94+D+S+N+B+F) bytes.
 • T = D+S+N+B
 • N = (IP HDR length - 5) * 4.
 • F = (TCP HDR length - 5)*4

A.2.2             Type 2: Ethernet, IPv6

A.2.2.1                 Type 2.1: Ethernet, IPv6 Data
This type contains only an Ethernet header and an IPv6 header while the packet should be a
fragmented packet. If the packet is not fragmented and the Next header is not supported, the header is
not split. The supported packet types for header split are programmed in PSRTYPE register (per VF).

     Offset    # of Bytes            Field                      Value           Action                  Comment

0                  6        Destination Address                                 Ignore    MAC Header – Processed by main
                                                                                          address filter, or broadcast filter.

6                  6        Source Address                                      Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****              Ignore

                            (Outer VLAN, E-tag)        0x893F ************

12+D            S=(0/4)     Possible VLAN Tag          0x8100                    Check

                                                           IPv6 Header

12+D+S             2        Type                       0x86DD                   Compare   IP

14+D+S             1        Version/ Traffic Class     0x6X                     Compare   Check IPv6

15+D+S             3        Traffic Class/Flow Label   -                        Ignore

18+D+S             2        Payload Length             -                        Ignore

20+D+S             1        Next Header                IPv6 next header types    Check    The last header must be fragmented
                                                                                          header for the header to be split.

21+D+S             1        Hop Limit                  -                        Ignore

22+D+S             16       Source Address             -                        Ignore

38+D+S             16       Destination Address                                 Ignore

54+D+S             N        Possible IPv6 Next         -                        Ignore
                            Headers

In this case the packet is split after (54+D+S+N) bytes.
 • The last next header field of the IP section field should not be 0x11/0x06 (TCP/UDP).

333369-009                                                                                                                   1219
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                            Packet Formats

A.2.2.1.1              Type 2.2: Ethernet (VLAN/SNAP) IPv6 UDP

This type contains only Ethernet header, IPv6 header, and UDP header.

     Offset   # of Bytes              Field                     Value           Action                  Comment

0                 6         Destination Address                                 Ignore    MAC Header – Processed by main
                                                                                          address filter, or broadcast filter.

6                 6         Source Address                                      Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****              Ignore

                            (Outer VLAN, E-tag)        0x893F ************

12+D           S=(0/4)      Possible VLAN Tag                                    Check

                                                           IPv6 Header

12+D+S            2         Type                       0x86DD                   Compare   IP

14+D+S            1         Version/ Traffic Class     0x6X                     Compare   Check IPv6.

15+D+S            3         Traffic Class/Flow Label   -                        Ignore

18+D+S            2         Payload Length             -                        Ignore

20+D+S            1         Next Header                IPv6 next header types    Check
                                                       Or
                                                       0x11

21+D+S            1         Hop Limit                  -                        Ignore

22+D+S            16        Source Address             -                        Ignore

38+D+S            16        Destination Address                                 Ignore

54+D+S            N         Possible IPv6 Next         -                        Ignore
                            Headers

                                                           UDP Header

54+D+S+N          2         Source Port                Not (0x801)               Check    Not NFS packet.

56+D+S+N          2         Destination Port           Not (0x801)               Check    Not NFS packet.

58+D+S+N          2         Length                     -                        Ignore

60+D+S+N          2         Checksum                   -                        Ignore

In this case the packet is split after (62+D+S+N) bytes.
 • The last 'next-header' field of the last header of the IP section must be 0x06.

1220                                                                                                                 333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.2.2.2                 Type 2.3: Ethernet (VLAN/SNAP) IPv6 TCP
This type contains only Ethernet header, IPv6 header, and UDP header.

     Offset     # of Bytes            Field                      Value           Action                 Comment

0                   6        Destination Address                                 Ignore    MAC Header – Processed by main
                                                                                           address filter, or broadcast filter.

6                   6        Source Address                                      Ignore

    12 D=(0/4/6/8)   Outer Tag                  0x8100 ****              Ignore

                             (Outer VLAN, E-tag)        0x893F ************

12+D             S=(0/4)     Possible VLAN Tag                                    Check

                                                        IPv6 Header

12+D+S              2        Type                       0x86DD                   Compare   IP

14+D+S              1        Version/ Traffic Class     0x6X                     Compare   Check IPv6

15+D+S              3        Traffic Class/Flow Label   -                        Ignore

18+D+S              2        Payload Length             -                        Ignore

20+D+S              1        Next Header                IPv6 next header types    Check
                                                        Or
                                                        TCP

21+D+S              1        Hop Limit                  -                        Ignore

22+D+S              16       Source Address             -                        Ignore

38+D+S              16       Destination Address                                 Ignore

54+D+S              N        Possible IPv6 Next         -                        Ignore
                             Headers

                                                        TCP Header

54+D+S+N            2        Source Port                Not (0x801)               Check    Not NFS packet

56+D+S+N            2        Destination Port           Not (0x801)               Check    Not NFS packet

58+D+S+N            4        Sequence number            -                        Ignore

62+D+S+N            4        Acknowledge number         -                        Ignore

66+D+S+N           1/2       Header Length                                        Check

66.5+D+S+N          1.5      Different bits             -                        Ignore

68+D+S+N            2        Window size                -                        Ignore

70+D+S+N            2        TCP checksum               -                        Ignore

72+D+S+N            2        Urgent pointer             -                        Ignore

74+D+S+N            F        TCP options                -                        Ignore

In this case the packet is split after (54+D+S+N+F) bytes.
 • F = (TCP header length - 5) * 4.
 • The last 'next-header' field of the last header of the IP section must be 0x11.

A.2.3             Type 3: Reserved
Type 3 used to be iSCSI packets (Header split is not supported for iSCSI packets in the X550).

333369-009                                                                                                                  1221
                                    Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                       Packet Formats

A.2.4           Type 4: Reserved

A.2.5           Type 5: Cloud Packets

A.2.5.1            Type 5.1: Ethernet, IPv4, NVGRE, IPv4/6, TCP/UDP
This type contains an Ethernet header an IPv4 Header, a GRE header an IPv4/6 header and a TCP or
UDP header. The supported packet types for header split are programmed in PSRTYPE register (per VF).

       Offset     # of Bytes               Field                    Value         Action            Comment

0                     6         Destination Address                               Ignore   MAC Header – Processed by
                                                                                           main address filter, or
                                                                                           broadcast filter.

6                     6         Source Address                                    Ignore

    12 D=(0/4/6/8)   Outer Tag                 0x8100 ****             Ignore

                                (Outer VLAN, E-tag)       0x893F ************

12+D               S=(0/4)      Possible VLAN Tag         0x8100                  Check

12+D+S                2         Type                      0x0800                 Compare   IP
                                                                                           Split on outer L2 is done
                                                                                           after this field.

                                                      IPv4 Header

14+D+S                1         Version/ HDR length       0x4X                   Compare   Check IPv4 and header
                                                                                           length.

15+D+S                1         Type of Service           -                       Ignore

16+D+S                2         Packet Length             -                       Ignore

18+D+S                2         Identification            -                       Ignore

20+D+S                2         Fragment Info             0x00                   Compare

22+D+S                1         Time to live              -                       Ignore

23+D+S                1         Protocol                  0x2F                   Compare   GRE

24+D+S                2         Header Checksum           -                       Ignore

26+D+S                4         Source IP Address         -                       Ignore

30+D+S                4         Destination IP Address    -                       Ignore

34+D+S                N         Possible IP Options                               Ignore

                                                      GRE Header

34 + D +S +N          2         Flags/Version             0x2000                 Compare

36 + D +S +N          2         Protocol Type             0x6558                 Compare

38+ D +S +N           3         TNI                                                Store   Used for Flow director.

41 + D +S + N         1         Reserved                  0x0                     Ignore   Split on Cloud header splits
                                                                                           after this field.

                                                   Inner MAC Header

42 + D +S + N         6         Inner Destination                                 Ignore   Used for Flow director.
                                Address

48 + D +S + N         6         Inner Source Address                              Ignore

1222                                                                                                        333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

       Offset        # of Bytes               Field                    Value       Action             Comment

54 + D + S + N         I=(0/4)     Possible Inner VLAN       0x8100                 Store    Used for Flow director.
                                   Tag

54 + D + S + N + I       2         Type                      0x0800/0x86DD         Compare   Split on L2 is done after this
                                                                                             field.

                          IPv4/6 header - as described above                                 Split on L3 is done after
                                                                                             these fields.

                             UDP/TCP - as described above                                    Split on L4 is done after
                                                                                             these fields.

A.2.5.2               Type 5.2: Ethernet, IPv4, VXLAN, MAC, IPv4/6, TCP/
                      UDP
This type contains an Ethernet header an IPv4 Header, a UDP header with a specific UDP destination
port a VXLAN header, an inner MAC header, an IPv4/6 header and a TCP or UDP header. The supported
packet types for header split are programmed in PSRTYPE register (per VF).

       Offset        # of Bytes               Field                    Value       Action             Comment

0                        6         Destination Address                             Ignore    MAC Header – Processed by
                                                                                             main address filter, or
                                                                                             broadcast filter.

6                        6         Source Address                                  Ignore

    12 D=(0/4/6/8)   Outer Tag                 0x8100 ****           Ignore

                                   (Outer VLAN, E-tag)       0x893F ************

12+D                  S=(0/4)      Possible VLAN Tag         0x8100                 Check

12+D+S                   2         Type                      0x0800                Compare   IP
                                                                                             Split on outer L2 is done
                                                                                             after this field

                                                         IPv4 Header

14+D+S                   1         Version/ HDR length       0x4X                  Compare   Check IPv4 and header
                                                                                             length

15+D+S                   1         Type of Service           -                     Ignore

16+D+S                   2         Packet Length             -                     Ignore

18+D+S                   2         Identification            -                     Ignore

20+D+S                   2         Fragment Info             0x00                  Compare

22+D+S                   1         Time to live              -                     Ignore

23+D+S                   1         Protocol                  0x11                  Compare   UDP

24+D+S                   2         Header Checksum           -                     Ignore

26+D+S                   4         Source IP Address         -                     Ignore

30+D+S                   4         Destination IP Address    -                     Ignore

34+D+S                   N         Possible IP Options                             Ignore

                                                         UDP Header

34+D+S+N                 2         Source Port                                     Ignore

36+D+S+N                 2         Destination Port                                Compare   Compare to VXLANCN-
                                                                                             TRL.UDPPORT

38+D+S+N                 2         Length                    -                     Ignore

333369-009                                                                                                               1223
                                   Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                  Packet Formats

       Offset            # of Bytes               Field                      Value              Action               Comment

40+D+S+N                      2         Checksum                   -                                              Ignore

                                                            VXLAN Header

42 + D +S + N                 1         Flags                      0x08                       Compare    VNI exists

43 + D + S + N                3         Reserved                   0x000000                   Compare

46 + D + S + N                3         VNI                                                     Store    Used for flow director

49 + D + S + N                1         Reserved                   0x00                       Compare    Split on Cloud header splits
                                                                                                         after this field.

                                                          Inner MAC Header

50 + D +S + N                 6         Inner Destination                                       Ignore   Used for Flow director
                                        Address

56 + D +S + N                 6         Inner Source Address                                    Ignore

62 + D + S + N             I=(0/4)      Possible Inner VLAN        0x8100                       Store    Used for Flow director
                                        Tag

62 + D + S + N + I            2         Type                       0x0800/0x86DD              Compare    Split on L2 is done after this
                                                                                                         field

                               IPv4/6 header - as described above                                        Split on L3 is done after
                                                                                                         these fields

                                  UDP/TCP - as described above                                           Split on L4 is done after
                                                                                                         these fields

A.3               IPsec Formats Run Over the Wire
This section describes the IPsec packet encapsulation formats run over the wire by IPsec packets
concerned with the off load in either Tx or Rx direction.
The following legend is valid for Figure A-12 through Figure A-17 of this appendix:

Shaded fields correspond to the portion of the data that is protected by the integrity check.

Yellow colored fields are mutable fields that might be changed when traveling between the source and the destination, and are
zeroed when computing ICV or when encrypting/decrypting.

Cyan colored fields correspond to the portion of data that is protected for both integrity and confidentiality.

Non-colored fields are not protected either for integrity or for confidentiality.

1224                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.3.1             AH Formats
 • IPv4 header:
     — IP total length (2 bytes) — Total IP packet length in bytes, including IP header, AH header,
       TCP/UDP header, and TCP/UDP payload.
     — Protocol (1 byte) — AH protocol number, i.e. value 51.
 • IPv6 header:
     — IP payload length (2 bytes) — IP payload length in bytes, including AH header, TCP/UDP
       header, and TCP/UDP payload.
     — Next header (1 byte) — AH protocol number, i.e. value 51.
 • AH header:
     — Next header (1 byte) — Layer4 protocol number, 6 for TCP, 17 for UDP, etc.
     — AH length (1 byte) — Authentication Header length in 32-bit DWords units, minus “2”, i.e. for
       AES-128 its value is 7 for IPv4 and 8 for IPv6.
     — Reserved (2 bytes) — Must be set to zero.
     — SPI (4 bytes) — Arbitrary 32-bit Security Parameters Index allocated by the receiver to identify
       the SA to which the incoming packet is bound. It is required that the local OS allocates SPIs in
       a unique manner per local IP Address.
     — SN (4 bytes) — Unsigned 32-bit Sequence Number that contains a counter value that increases
       by one for each Ethernet frame sent. It is initialized to 0 by the sender (and the receiver) when
       the SA is established, i.e. the first packet sent using a given SA has a sequence number of 1.
     — IV (8 bytes) — Initialization Vector to be used ‘as is’ in the nonce input to AES-128 crypto
       engine, but it must be zeroed prior to using it in the AAD input to the engine.
     — ICV (16 bytes) — Integrity Check Value for this packet, authentication tag output of the AES-
       128 crypto engine. As being part of the AH header, this field is also included in the AAD input to
       the crypto engine, and it should be zeroed prior to the computation.
     — ICV Padding (4 bytes) — Explicit padding bytes appended to the ICV field in IPv6, as it is
       required to maintain the (Authentication) extension header length as a multiple of 64 bits. By
       explicit we mean that these bytes are sent over the wire. It is formed by 4 arbitrary bytes that
       need not be random to achieve security. For TSO, it is replicated from the header provided by
       the driver in every frame.
 • L4 header (for example - TCP/UDP) — Length (in bytes) depend on the protocol.
 • L4 payload (for example - TCP/UDP) — Can be any length in bytes.

333369-009                                                                                            1225
                                 Did this document help answer your questions?

                                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                                         Packet Formats

       0            3   4          7   8                            15   16      18      19                                         31

# 1 Ver              Hlen                    TOS                                              IP total length

# 2 Identification                               flags                         Fragment offset

    3 TTL                         Protocol = AH                                      Header checksum

# 4 Source IPv4 address

# 5 Destination IPv4 address

# 1 Next header                     AH length                                             Reserved

# 2 Security Parameter Index (SPI)

# 3 Sequence Number (SN)

  4
                                                           Initialization Vector (IV)1
  5

  6

  7
                                                          Integrity Check Value (ICV)

  8

  9

  1
                                                             L4 header (TCP/UDP)

                                                            L4 payload (TCP/UDP)

  N

1. IV field has been colored in Yellow as it must be zeroed in the AAD input to AES-128 crypto engine, in spite of this it is NOT
   zeroed in the nonce input to the engine.

Figure A-12. AH Packet Over IPv4

1226                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

       0            3    4            7     8           11   12          15   16                      23   24                    31

# 1 Ver            Traffic Class                                                  Flow label

    2 IP payload length                                             Next hdr = AH              Hop limit

  3

  4
                                                                   Source IPv6 address
  5

  6

  7

  8
                                                                Destination IPv6 address
  9

 10

# 1 Next Header                    AH length                                             Reserved

# 2 Security Parameter Index (SPI)

# 3 Sequence Number (SN)

  4
                                                                Initialization Vector (IV)1
  5

  6

  7
                                                              Integrity Check Value (ICV)
  8

  9

    10 ICV Padding

  1

                                                                  L4 header (TCP/UDP)

                                                                  L4 payload (TCP/UDP)

  N

1. IV field has been colored in Yellow as it must be zeroed in the AAD input to AES-128 crypto engine, in spite of this, it is NOT
   zeroed in the nonce input to the engine.

      Figure A-13. AH Packet Over IPv6

333369-009                                                                                                                      1227
                                            Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Packet Formats

A.3.2              ESP Formats
 • IPv4 header:
       — IP total length (2 bytes) — Total IP packet length in bytes, including IP header, ESP header,
         TCP/UDP header, TCP/UDP payload, ESP trailer, and ESP ICV if present.
       — Protocol (1 byte) — ESP protocol number, i.e. value 50.
 • IPv6 header:
       — IP payload length (2 bytes) — IP payload length in bytes, including ESP header, TCP/UDP
         header, TCP/UDP payload, ESP trailer, and ESP ICV if present.
       — Next header (1 byte) — ESP protocol number, i.e. value 50.
 • ESP header:
       — SPI (4 bytes) — arbitrary 32-bit Security Parameters Index allocated by the receiver to identify
         the SA to which the incoming packet is bound. It is required that the local OS allocated SPIs in
         a unique manner per local IP Address.
       — SN (4 bytes) — unsigned 32-bit Sequence Number that contains a counter value that increases
         by one for each Ethernet frame sent. It is initialized to 0 by the sender (and the receiver) when
         the SA is established, i.e. the first packet sent using a given SA has a sequence number of 1.
       — IV (8 bytes) — Initialization Vector to be used in the nonce input field of the AES-128 crypto
         engine, and for authenticated-only ESP packets it is used also in the AAD input.
 • L4 header (for example - TCP/UDP):
       — Length (in bytes) depend on the protocol.
       — TCP/UDP checksum computed from the TCP/UDP header up to the end of TCP payload,
         excluding ESP trailer.
       — TCP/UDP header is encrypted if ESP encryption is required.
 • L4 payload (for example - TCP/UDP)— Can be any length in bytes. It is encrypted if ESP encryption
   is required.
 • ESP trailer:
       — Padding (0-255 bytes) — unsigned 1-byte integer values, with its content started by 1 and
         making up a monotonically increasing sequence: 1, 2, 3,... Though in Tx it is only 0-15 bytes
         long, in Rx it might be longer, if the sender’s policy is to hide the packet length.
       — Padding length (1 byte) — Number of explicit padding bytes (Padding length and Next header
         bytes excluded) required to get 4-bytes alignment of the ESP header, TCP/UDP header, TCP/
         UDP payload, and ESP trailer. By explicit we mean that these bytes are sent over the wire. A
         remote IPsec implementation may also add more padding bytes (up to 255-bytes) than the
         minimum required for getting the 4-bytes alignment with the aim of hiding the packet length.
       — Next header (1 byte) — Layer4 protocol number, 6 for TCP, 17 for UDP, etc.
       — ESP trailer is encrypted if ESP encryption is required.
 • ESP ICV (16 bytes) — Integrity Check Value for this packet, authentication tag output of the AES-
   128 crypto engine.

1228                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

        0          3   4          7   8                           15    16      18     19             23   24                      31

# 1 Ver           Hlen                     TOS                                            IP total length

# 2 Identification                              flags                         Fragment offset

    3 TTL                         Protocol = ESP                                  Header checksum

# 4 Source IPv4 address

# 5 Destination IPv4 address

# 1 Security Parameter Index (SPI)

# 2 Sequence Number (SN)

    3
                                                          Initialization Vector (IV)
    4

    1

                                                           L4 header (TCP/UDP)

                                                           L4 payload (TCP/UDP)

                                                                             Padding (0-255 bytes)

 N-4                                                                              Padding length                     Next header

 N-3

 N-2
                                                       Integrity Check Value (ICV)
 N-1

   N

Figure A-14. Authenticated Only ESP Packet Over IPv4

333369-009                                                                                                                         1229
                                      Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Packet Formats

       0         3   4          7   8                            15   16      18     19             23   24                      31

# 1 Ver           Hlen                     TOS                                            IP total length

# 2 Identification                              flags                         Fragment offset

    3 TTL                         Protocol = ESP                                  Header checksum

# 4 Source IPv4 address

# 5 Destination IPv4 address

# 1 Security Parameter Index (SPI)

# 2 Sequence Number (SN)

   3
                                                        Initialization Vector (IV)
   4

   1

                                                              TCP/UDP header

                                                           TCP/UDP payload

                                                                           Padding (0-255 bytes)

 N-4                                                                            Padding length                     Next header

 N-3

 N-2
                                                     Integrity Check Value (ICV)
 N-1

   N

Figure A-15. Authenticated & Encrypted ESP Packet Over IPv4

1230                                                                                                                       333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

       0           3   4              7   8                      15    16                           23   24                 31

# 1 Ver           Priority                                              Flow label

    2 IP payload length                                Next hdr = ESP                  Hop limit

   3

   4
                                                           Source IPv6 address
   5

   6

   7

   8
                                                         Destination IPv6 address
   9

  10

# 1 Security Parameter Index (SPI)

# 2 Sequence Number (SN)

   3
                                                         Initialization Vector (IV)
   4

   1

                                                             TCP/UDP header

                                                             TCP/UDP payload

                                                                            Padding (0-255 bytes)

 N-4                                                                           Padding length                 Next header

 N-3

 N-2
                                                        Integrity Check Value (ICV)
 N-1

   N

Figure A-16. Authenticated Only ESP Packet Over IPv6

333369-009                                                                                                                  1231
                                          Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                               Packet Formats

       0         3   4              7   8                      15    16                           23   24                  31

# 1 Ver           Priority                                              Flow label

    2 IP payload length                                Next hdr = ESP                  Hop limit

   3

   4
                                                         Source IPv6 address
   5

   6

   7

   8
                                                       Destination IPv6 address
   9

  10

# 1 Security Parameter Index (SPI)

# 2 Sequence Number (SN)

   3
                                                       Initialization Vector (IV)
   4

   1

                                                           TCP/UDP header

                                                           TCP/UDP payload

                                                                          Padding (0-255 bytes)

 N-4                                                                         Padding length                 Next header

 N-3

 N-2
                                                      Integrity Check Value (ICV)
 N-1

   N

Figure A-17. Authenticated and Encrypted ESP Packet Over IPv6

For authenticated and encrypted ESP packets, though it is used in the Nonce input to the AES-128
crypto engine, the IV field was left non-colored because it is not a part of the ADD or the Plaintext input
fields.

1232                                                                                                                 333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.4              FCoE Framing
Related standards:
 • FC-FS-2 — FRAMING AND SIGNALING-2 (FC-FS-2) Rev 1.00.
 • FCoE — Fibre Channel Backbone - 5 (FC-BB-5), v2.0, 6/4/2009, INCITS 462-2010 Document:
   available from http://www.incits.org/ (09-056v5.pdf).

A.4.1               FCoE Frame Format
FC over Ethernet packets encapsulate FC frames as shown in Figure A-18 and Figure A-19. Maximum
expected FCoE frame size is 2164 bytes. This size does not include FC extension headers (not expected
in FCoE), without optional encapsulation (expected to be off-loaded by the hardware) and without CN
tag (not expected in receive).
All fields in the FCoE frame are treated as any other field in the network. The MS Byte is first on the
wire and the LS bit on each byte is first on the wire. This rule applies for all fields including those ones
that span on non complete byte boundaries such as the FCoE VER field.
Note:        LSB goes first on the wire.

                                                          FC Frame
  Ethernet MAC                 FCoE
                   VLAN Tag                                                            EOF      Ethernet CRC
    Addresses                 Header    FC Header       Optional FC Data     FC CRC

Figure A-18. Ethernet Encapsulation to FC frames

333369-009                                                                                              1233
                                  Did this document help answer your questions?

                                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                                           Packet Formats

            msb..... .    . . . . .....lsb    msb.....         . . . . ....lsb     msb. ....lsb     msb     lsb      msb..........   ..... . . lsb
            31....... . .   . . . .....24     23.. . . . .     . ..... .....16     15........12     11       8       7.............. ... .......0
             First byte on the wire                                                                                   Last byte on the wire

# 0 Destination Ethernet MAC Address

        4

# 8 Source Ethernet MAC Address

       12                                                      802.1Q Tag (VLAN + Priority)

# 16 FCoE Ethernet Type = 0x8906                                  Ver                           Reserved

# 20 Reserved

# 24 Reserved

# 28 Reserved                                                                 SOF

# 32 Routing Control (R_CTL)                                            Destination Identification (D_ID)

# 36 Class Specific Control

                                                                                   Source Identification (S_ID)
                     (CS_CTL)

    40 TYPE                                                          Frame Control (F_CTL)

# 44 Sequence ID (SEQ_ID)           Data Field Control (DF_CTL)                           Sequence Count (SEQ_CNT)

# 48 Originator Exchange ID (OX_ID)                                          Responder Exchange ID (RX_ID)

# 52 Parameter (PARAM)

   0…N
                                        Optional FC Data… always 4 byte align (including optional FC padding)

 56 +N                                                         Fibre Channel CRC (FC_CRC)

   N+8                  EOF                                                                   Reserved

       M                                                                Ethernet CRC

Figure A-19. FCoE Packet Structure

A.4.1.1                    Ethernet MAC Addresses
L2 destination and Source Ethernet MAC Addresses (each of them is 6 bytes long). The Ethernet MAC
Address of the target is assumed to be assigned by the network. It could be done by the FCoE repeater
or LAN administrator. The mechanism that is used for Ethernet MAC Address assignment and Ethernet
MAC Address detection is outside of the scope of this document.

A.4.1.2                    802.1Q Tag
802.1Q tagging is mandatory for FCoE usage. FCoE assumes DCB functionality which provides Priority-
based FC and QCN. These functions require 802.1Q tag presence to define packet priority.

1234                                                                                                                                   333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

A.4.1.3               FCoE Header
The FCoE header is composed of a new FCoE Ethernet type, FCoE version tag and the Start Of Frame
tag.
 • FCoE Ethernet Type — Equals 0x8906
 • Version (Ver) — A 4-bit field that indicates the FCoE protocol version number. The X550 supports
   FCoE version as defined by FCRXCTRL.FCOEVER.
 • Start of Frame (SOF) — The FCoE Start of frame is a subset of the FC-FS-2 SOF codes as defined
   in the Table A-1.

Table A-1.     E_SOF Mapping
   FC SOF       FCoE SOF Code      FC Traffic Class                                 Comment

    SOFf             0x28                   F         Fabric start of frame. Not expected in an FCoE.

    SOFi2            0x2D                   2         Used in the first frames in a sequence.

   SOFn2             0x35                   2         Used in all but first frame in a sequence.

    SOFi3            0x2E                   3         Used in the first frames in a sequence.

   SOFn3             0x36                   3         Used in all but first frame in a sequence.

A.4.1.4               FCoE Packet Encapsulation Trailer
The FCoE trailer is composed of an End of frame, optional padding and Ethernet CRC.
 • End of Frame (EOF) — The FCoE End of frame maps the FC-FS-2 EOF codes as defined in the
   Table A-2.
 • Ethernet Padding — The minimal FC frame length could be as small as 28 bytes long (FC header
   with no data). In such a case, the encapsulated FC frame must include padding so that the total
   Ethernet packet size is not smaller than 64 bytes.
 • Ethernet CRC — The IEEE 802.3 CRC as defined by the following polynomial:
           X32+X26+X23+X22+X16+X12+X11+X10+X8+X7+X5+X4+X2+X+1

Table A-2.     EOF Mapping
   FC EOF       FCoE EOF Code      FC Traffic Class                                 Comment

    EOFn             0x41             2, 3, 4, F      Normal EOF.

    EOFt             0x42             2, 3, 4, F      EOF Terminate used to close a sequence.

    EOFni            0x49             2, 3, 4, F      EOF Invalid indicating that the frame content is invalid.

    EOFa             0x50             2, 3, 4, F      EOF Abort.

333369-009                                                                                                        1235
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                                        Packet Formats

A.4.2                FC Frame Format
Note:        This section is provided as a background on FC and is not required for the hardware
             implementation. For a complete description of the FC fields, refer to FC-FS-2 specification.
The FC frame as defined in FC-FS-2 specification is shown in the Figure A-20 below while relevant fields
are detailed in this section.

             Extended                   Optional
  SOF                    FC Header                       FC Payload (FC Data & optional padding)     FC CRC    EOF
              Header                    Headers

Figure A-20. FC Frame Format

A.4.2.1                 FC SOF and EOF
FC Start of frame (SOF) delimiter and End of frame (EOF) delimiter. In FCoE frames, the SOF and EOF
fields in the FC frame are extracted and reflected in the FCoE encapsulation. The SOF and EOF codes
that are reflected in the FCoE framing are shown in Table A-1 and Table A-2.

A.4.2.2                 FC CRC
The Cyclic Redundancy Check (CRC) is a four byte field that follows the Data Field. It enables end to
end integrity checking on the whole FC frame. The hardware adds this field if the FCoE bit is set in the
transmit context descriptor. The FC CRC off load is described in more detail in Section 7.11.3.2.

A.4.2.3                 FC Header
The FC header fields are provided in the header buffer by the FCoE driver. The FC header includes fields
that are modified by the hardware as part of Large Send off load. These fields are indicated in this
section as “Dynamic” while fields that are not modified by the hardware are indicated as “Static”.
Routing Control (R_CTL)
       The R_CTL is a one-byte Static field that contains routing and information bits to categorize the
       frame function.
Class Specific Control (CS_CTL)
       This is a 1 byte Static field that defines either the Class specific control or priority according to bit
       17 in the Frame control (F_CTL) field.
Destination Identification (D_ID)
       The D_ID is a 3 byte Static field that defines the FC destination address.
Source Identification (S_ID)
       The S_ID is a 3 byte Static field that defines the FC source address.
Data Structure Type (TYPE)
       The TYPE is a 1 byte Static field that identifies the protocol of the frame content for data frames.
Frame Control (F_CTL)
       The F_CTL is a 3 byte Dynamic field that contains control information relating to the frame
       content. The F_CTL is further described in Section A.4.2.3.1. Section 7.11.2.7 describes how the
       F_CTL field is modified during large send.

1236                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

Data Field Control (DF_CTL)
    The DF_CTL is a 1 byte Dynamic field that specifies the presence of optional headers at the
    beginning of the Data_Field. The Optional headers supported by large send are present only on the
    first frame in the FC sequence. Section 7.11.2.7.1 describes how the DF_CTL field is modified
    during large send.
Sequence ID (SEQ_ID)
    The SEQ_ID is a 1 byte Static number associated with a sequence. A sender must assign SEQ_ID
    numbers so that the recipient would always be able to distinguish between consecutive sequences.
    SEQ_ID do not have to be sequential and do not have to be unique even within the same IO
    exchange as long as it is guaranteed that the recipient would be able to distinguish between them.
Sequence Count (SEQ_CNT)
    The SEQ_CNT is a 2 byte Dynamic field that indicates the sequential order of Data frame
    transmission within a single Sequence or multiple consecutive Sequences for the same Exchange.
    The SEQ_CNT of the first Data frame of the first Sequence of the Exchange transmitted by either
    the Originator or Responder is ‘0’. The SEQ_CNT of subsequent Data frames in the Sequence is
    increased by one for each data frame. The SEQ_CNT of the first Data frame in each sequence other
    than the first one can start at ‘0’ or be increased by 1 from the last used SEQ_CNT.
Originator Exchange ID (OX_ID)
    The OX_ID is a two-byte Static field that identifies the Exchange_ID assigned by the Originator. If
    the Originator is enforcing uniqueness via the OX_ID mechanism, it must set a unique value for
    OX_ID other than FFFFh. A value of FFFFh indicates that the OX_ID is unassigned and that the
    Originator is not enforcing uniqueness via the OX_ID. The X550 supports large receive and direct
    data placement only if OX_ID is used to identify uniqueness.
Responder Exchange ID (RX_ID)
    The RX_ID is a two byte Static field assigned by the Responder that must provide a unique, locally
    meaningful exchange identifier at the Responder. The Responder of the Exchange must set a unique
    value for RX_ID other than FFFFh.
Parameter (PARAM)
    The Parameter field is a Dynamic field which is based on frame type. For Data frames with the
    relative offset present bit set to 1, the Parameter field specifies relative offset. The offset defines
    the relative displacement of the first byte of the Payload of the frame from the base address as
    specified by the ULP. Relative offset is expressed in terms of bytes.

A.4.2.3.1              Frame Control (F_CTL)

The Frame Control (F_CTL) is a three-byte field that contains control information relating to the frame
content. If an error in bit usage is detected, the software initiates a reject frame (P_RJT) in response
with an appropriate reason code (FCoE software driver responsibility). The F_CTL format is shown in
Table A-3 below.
When a bit(s) is designated as “Static” it is provided by the FCoE driver as part of the large send
header. The hardware keeps this bit(s) as is in all preceding frames of the large send.
When a bit(s) is designated as “Dynamic” it is provided by the FCoE driver as part of the large send
header. The hardware may change it in some of the packets in the large send as described in
Section 7.11.2.7. Exact setting of these bit(s) is described in the Table A-3 below.
When a bit(s) is designated as meaningful under a set of conditions, that bit must be ignored if those
conditions are not present.

333369-009                                                                                               1237
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                            Packet Formats

Table A-3.        F_CTL Format
       Control Field       Bit(s)     Type                                       Description

Exchange Context            23        Static   0b = Originator of exchange.
                                               1b = Responder of exchange.

Sequence Context            22        Static   0b = Sequence initiator.
                                               1b = Sequence recipient.

First Sequence              21        Static   0b = Sequence other than first of exchange.
                                               1b = first Sequence of exchange.

Last Sequence               20        Static   0b = Sequence other than last of exchange.
                                               1b = last sequence of exchange must be set on the last data frame of the last
                                                    sequence. However it can be set on any preceding frames. Once it is set,
                                                    it must be set on all frames till the last one of that exchange.

End Sequence                19      Dynamic    0b = Data frame other than last of sequence.
                                               1b = last Data frame of sequence.

End Connection              18        Static   Relevant for Class 1 or 6.

CS CTL / Priority Enable    17        Static   Defines the meaning of the CS_CTL byte in the FC header to be either CS_CTL
                                               or Priority indication.
                                                0b = Word 1, Bits 31-24 = CS_CTL
                                                1b = Word 1, Bits 31-24 = Priority

Sequence Initiative         16      Dynamic    This bit is used to transfer initiative from a sender to a recipient. This bit is
                                               meaningful only on the last frame of a sequence (when bit 19 - “End Sequence”
                                               is set).
                                                 0b = Hold sequence initiative.
                                                 1b = Transfer sequence initiative.

X_ID reassigned             15        Static   Obsolete.

Invalidate X_ID             14        Static   Obsolete.

ACK Form                   13:12      Static   ACK Form is meaningful on all Class 1, Class 2, or Class 6 Data frames of a
                                               Sequence and on all connect request frames. ACK_Form is not meaningful on
                                               Class 1, Class 2, or Class 6 Link_Control frames, or any Class 3 frames.
                                                00b = No assistance provided10b = reserved.
                                                01b = Ack_1 Required11b = Ack_0 Required.

Data Compression            11        Static   Obsolete.

Data Encryption             10        Static   Obsolete.

Retransmitted Sequence       9        Static   Meaningful in Class 1 and 6 and only.
                                                0b = Original sequence transmission.
                                                1b = sequence retransmission.

Unidirectional Transmit      8        Static   Relevant for Class 1

Continue Sequence           7:6     Dynamic    Last Data frame - Sequence Initiator
Condition                                        00b = No information.
                                                 01b = Sequence to follow-immediately.
                                                 10b = Sequence to follow-soon.
                                                 11b = Sequence to follow-delayed.
                                               It is meaningful only when the “End Sequence” is set to ‘1’ and the Sequence
                                               Initiative bit is cleared ‘0’.

1238                                                                                                                 333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

Table A-3.         F_CTL Format [continued]
       Control Field           Bit(s)        Type                                                Description

Abort Sequence Condition         5:4         Static         ACK frame - Sequence Recipient
                                                             00b = Continue sequence.
                                                             01b = Abort sequence, perform ABTS.
                                                             10b = Stop Sequence.
                                                             11b = Immediate sequence re-XMT requested.
                                                            Data frame (1st of Exchange) - The Abort Sequence must be set to a value by
                                                            the Sequence Initiator on the first Data frame of an Exchange to indicate that
                                                            the Originator is requiring a specific error policy for the Exchange.
                                                             00b = Abort, discard multiple sequences.
                                                             01b = Abort, discard a single sequence.
                                                             10b = Process policy with infinite buffers.
                                                             11b = Discard multiple sequences with immediate re-XMT.

Relative offset present           3          Static         0b = Parameter field defined for some frames
                                                            1b = Parameter Field = relative offset

Exchange reassembly               2          Static         Reserved for exchange reassembly.

Fill Bytes                       1:0        Dynamic         Defines the number of FC padding bytes to fill in the last frame in the sequence.
                                                            The value of these bytes is 0x00.
                                                            When FCoE offload is enabled (TUCMD.FCoE bit is set in the transmit context
                                                            descriptor), the hardware can pad the FC payload according to the buffer size
                                                            indicated by software (by the PAYLEN field in the transmit data descriptor).

A.4.2.4                   FC Extended Headers
Note:         The following section is provided as a background on FC and is not required for the hardware
              implementation or the software implementation since in FCoE frames, extended headers are
              not expected. The following quote is from the FCoE specification Rev 0.7 “No Extended
              Headers are relevant for the operations of a Reedtown NIC”.
The diagrams in Figure A-21, Figure A-22 and Table A-4 show the Fibre Channel frame structure with
Extended headers and lists the existing headers. Extended headers are identified by the R_CTL value as
shown in the diagrams below. The LAN controller does not support these Extended headers since they
are not expected in FCoE usage.

             FC Frame

       Extended Headers                                       Optional FC
                                       FC Header                                   [optional] FC Data (including optional padding)        FC CRC
           [Optional]                                           Header

Figure A-21. FC Frame format with Extended Headers

        msb..... .     . . . . .....lsb    msb.....             . . . . ....lsb   msb.....         . . . . ....lsb   msb..... .     . . . . .....lsb
        31....... . .  . . . .....24       23.. . . .   .       . ..... .....16   15.. . . . .     . .. ... .....8   7....... . .     . . . .....0
          Last byte on the wire                                                                                        First byte on the wire

# 0 Extended Header Specific Fields                                                        R_CTL

 4…

Figure A-22. Extended Header Format

333369-009                                                                                                                                     1239
                                           Did this document help answer your questions?

                                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                                             Packet Formats

Table A-4.          FC Extended Headers
           R_CTL                                                Extended Header                                                         Length

0x50                        VFT_Header (Virtual Fabric Tagging Header)                                                        8 Bytes

0x51                        IFR_Header (Inter-Fabric Routing Header)                                                          8 Bytes

0x52                        Enc_Header (Encapsulation Header)                                                                 24 Bytes

0x53…0x5F                   Reserved                                                                                          -

A.4.2.5                    FC Optional Headers
Note:        Most of the following section is provided as a background on FC and is not required for the
             hardware implementation. The reader may skip the detailed explanation of the Optional
             headers provided below and concentrate in the tables and figures that follow the text.
FCoE frames may include FC Optional headers. These headers (if they exist) would always show in the
first frame in a sequence. While FC implementation may include the FC Optional headers only on the
first frame in a sequence. In Large send functionality, the FC Optional headers may show only on the
first frame as shown in Figure 7-46 and Table A-5 (in Section 7.11.2.7.1).
The following diagrams Table A-5, Figure A-23 and Figure A-24 show the Fibre Channel frame structure
with Optional headers and lists the Optional headers. The Optional headers (that are present) are
always ordered as shown in Figure A-23 and Figure A-24. Their presence is indicated in the Data Field
Control (DF_CTL) field in the FC Header as indicated in Table A-5
Maximum FC frame size: The sum of the length in bytes of the FC Payload, the number of fill bytes, and
the lengths in bytes of all optional headers must not exceed 2112.

Table A-5.          FC Optional Headers
           DF_CTL                                      Optional Header                                                     Length

bit 6                          ESP Header / ESP Trailer                                               Variable

bit 5                          Network Header                                                         16 Bytes

bit 4                          Association Header                                                     32 Byte

bits 1:0                       Device Header                                                          0, 16, 32, or 64 Bytes

               <- - - - - - - - - - - - - - - - - - - - - - - - - - - - FC Frame - - - - - - - - - - - - - - - - - - - - - - - - - - - ->

                                                        Optional Headers
  Extended                                                                                            [optional] FC Data (including
                    FC Header            Network            Association                                                                       FC CRC
  Headers                                                                     Device Header
                                                                                                            optional padding)
                                         Header               Header

Figure A-23. FC Frame Format with Optional Headers (without ESP Header)

               <- - - - - - - - - - - - - - - - - - - - - - - - - - - FC Frame - - - - - - - - - - - - - - - - - - - - - - - - - - - - ->

  Extended
                    FC Header          ESP Header                                 Cryptic Data                               ESP Trailer      FC CRC
  Headers

Figure A-24. FC Frame Format with Optional Headers (with ESP Header)

1240                                                                                                                                        333369-009
                                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

ESP Header
    This is the first Optional header which covers the whole FC frame other than the FC header which is
    transmitted on the clear (as plain text). When an ESP header is present there is also the ESP trailer.
    If required, the software is responsible for the cryptic calculation and preparing the ESP header and
    trailer. Its presence is indicated by bit 6 in the DF_CTL field being set to one. The hardware does not
    support Large Send off load when ESP Optional header is used. When present, the ESP header and
    trailer are present in all frames of the exchange.
Network Header
    The Network Header, if used, must be present only in the first Data frame of a Sequence. A bridge
    or a gateway node that interfaces to an external Network may use the Network Header. The
    Network Header, is an optional header 16 Bytes long within the FC Data Field content. Its presence
    is indicated by bit 5 in the DF_CTL field being set to one. The Network Header may be used for
    routing between Fibre Channel networks of different Fabric address spaces, or Fibre Channel and
    non-Fibre Channel networks. The Network Header contains Name Identifiers for Network
    Destination Address and Network Source Address.
Association Header
    The Association Header, if used, must be present only in the first Data frame of a Sequence. The
    Association Header is an optional header 32 Bytes long within the Data Field content. Its presence
    is indicated by bit 4 in the DF_CTL field being set to one. The Association Header may be used to
    identify a specific Process or group of Processes within a node associated with an Exchange. When
    an Nx_Port has indicated during Login that an Initial Process Associator is required to communicate
    with it, the Association Header should be used by that Nx_Port to identify a specific Process or
    group of Processes within a node associated with an Exchange. The X550 does not use the
    Association for any filtering purposes but rather uses the OX_ID.
Device Header
    The Device Header, if present, must be present either in the first Data frame or in all Data frames of
    a Sequence. If Large Send off load is used, the Device header, if present, is present only in the first
    frame of the same large send. The Device Header, if present, must be 16, 32, or 64 bytes in size as
    defined by bits 1:0 in the DF_CTL field. The contents of the Device Header are controlled at a level
    above FC-2. Upper layer protocol (ULP) may use a Device Header, requiring the Device Header to be
    supported. The Device Header may be ignored and skipped, if not needed. If a Device Header is
    present for a ULP that does not require it, the related FC-4 may reject the frame with the reason
    code of “TYPE not supported”.

333369-009                                                                                             1241
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                             Packet Formats

A.5                E-tag and S-tag Formats
Note:         S-tags are not supported in the X550.
Packets with S-tag has the following format:

         msb                     lsb   msb                   lsb    msb                     lsb   msb                    lsb
         31                      24    23                    16     15                        8   7                       0
           First byte on the wire                                                                   Last byte on the wire

# 0 Destination MAC Address

     4

# 8 Source MAC Address

                       S-tag Ethernet Type (0x88a8)                                       S-tag Header

                        VLAN EtherType (optional)                                     VLAN Header (optional)

 ...                           Original Type

 ...

 ...                                                      Frame Payload

 ...

The S-tag format is the format defined for S-tags in the IEEE 802.1ad specification as described below:

                                                            1   1         1   1   2                                       3
 0                                                          5   6         8   9   0                                       1

                                                                              D
                              88-a8                                 PCP       E                     S-VID
                                                                              I

Figure A-25. S-tag Format

Packets with E-tag has the following format:

         msb                     lsb   msb                   lsb    msb                     lsb   msb                    lsb
         31                      24    23                    16     15                        8   7                       0
           First byte on the wire                                                                   Last byte on the wire

# 0 Destination MAC Address

     4

# 8 Source MAC Address

    12 E-tag Ethernet Type (0x893F)                                       E-tag Header

    16 E-tag Header (cont.)

 ...                    VLAN EtherType (optional)                                     VLAN Header (optional)

 ...                           Original Type

 ...                                                      Frame Payload

1242                                                                                                              333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Packet Formats

The E-tag format is the format defined in the IEEE 802.1BR specification as described below:

                                                       1   1           1   1   2                             3
 0                                                     5   6           8   9   0                             1

                                                                           D
                     EtherType - 0x893F                        E-PCP       E         Ingress E-CID_base
                                                                           I

 3   3   3   3   3                                     4   4                         5   5                   6
 2   3   4   5   6                                     7   8                         5   6                   3

 RSV     GRP                    E-CID_base                        Ingess_E-CID_ext              E-CID_ext

Figure A-26. E-tag Format

The Ingess_E-CID_ext and E-CID_ext are always zero for endpoints and are effectively reserved.

333369-009                                                                                                  1243
                                   Did this document help answer your questions?

LEGAL

No license (express or implied, by estoppel or otherwise) to any intellectual property rights is granted by this document.
This document (and any related software) is Intel copyrighted material, and your use is governed by the express license under which
it is provided to you. Unless the license provides otherwise, you may not use, modify, copy, publish, distribute, disclose or transmit
this document (and related materials) without Intel's prior written permission. This document (and related materials) is provided as
is, with no express or implied warranties, other than those that are expressly stated in the license.
Intel disclaims all express and implied warranties, including without limitation, the implied warranties of merchantability, fitness for a
particular purpose, and non-infringement, as well as any warranty arising from course of performance, course of dealing, or usage in
trade.
This document contains information on products, services and/or processes in development. All information provided here is subject
to change without notice. Contact your Intel representative to obtain the latest forecast, schedule, specifications and roadmaps.
The products and services described may contain defects or errors which may cause deviations from published specifications.
Copies of documents which have an order number and are referenced in this document may be obtained by calling 1-800-548-4725
or by visiting www.intel.com/design/literature.htm.
Intel and the Intel logo are trademarks of Intel Corporation in the U.S. and/or other countries.
* Other names and brands may be claimed as the property of others.
© 2015-2023 Intel Corporation.

1244                                                                                                                         333369-009
                                         Did this document help answer your questions?
