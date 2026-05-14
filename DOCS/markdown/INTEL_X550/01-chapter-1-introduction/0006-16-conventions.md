## 1.6 Conventions

### 1.6.1 Terminology and Acronyms

See Section 16, “Glossary and Acronyms”.

### 1.6.2 Byte Ordering

This section defines the organization of registers and memory transfers, as it relates to information
carried over the network:
 • Any register defined in Big Endian notation can be transferred as is to/from Tx and Rx buffers in the
   host memory. Big Endian notation is also referred to as being in network order or ordering.
 • Any register defined in Little Endian notation must be swapped before it is transferred to/from Tx
   and Rx buffers in the host memory. Registers in Little Endian order are referred to being in host
   order or ordering.

44                                                                                                  333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Introduction

Tx and Rx buffers are defined as being in network ordering; they are transferred as is over the network.
Note:        Registers not transferred on the wire are defined in Little Endian notation. Registers
             transferred on the wire are defined in Big Endian notation, unless specified differently.
