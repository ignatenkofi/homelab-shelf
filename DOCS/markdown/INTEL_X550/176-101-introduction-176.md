## 10.1 Introduction

This chapter describes the PHY registers in the X550, which are accessible via the internal MDIO
interface. Refer to Section 3.7.2.
The PHY is internally divided into a series of MDIO Manageable Devices (MMDs), each of which performs
a logical function as per the 10GBASE-T standard:
 • MMD #1 contains the PMA, which is basically the analog front-end of the chip (Section 10.2).
 • MMD #3 contains the PCS, which handles the 10GBASE-T transmission frame coding and decoding,
   including the 128-DSQ and LDPC work (Section 10.3).
 • MMD #7 contains the auto-negotiation function (Section 10.4).
 • MMD #29 contains the controls for the GbE and 100 Mb/s PCS machinery (Section 10.5).
 • MMD# 30 contains the global control functionality for the PHY, including the embedded micro
   controller (Section 10.6).

### 10.1.1 PHY Register Structure

A map of these regions is shown in Table 10-1.

Table 10-1. MMD Device Addresses
 5-bit Device Address
                                     MMD Name
         (Hex)

# 0 Reserved

    1 PMA/PMD (128 DSQ)

# 2 Reserved

    3 PCS (64/65B coder/decoder)

# 4 Reserved

        56                            Reserved

# 7 Auto-negotiation

       8  1C                          Reserved

         1D                       Clause 22 Extension

          1E                            Global

          1F                           Reserved

Any attempt to read from the reserved MMD addresses returns a value of 0x00, and any writes to these
addresses have no effect.

333369-009                                                                                         861
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.1.2 Format and Nomenclature

PHY registers within the device are referenced in the format:
      Region.Register.Bit
where Region corresponds to the MMD region being addressed, Register corresponds to the register
within the MMD region, and Bit is the bit within the register. All registers within the MDIO register space
are 16 bits. The address of the register is the 16 bit MDIO address.
All read and write operation are word based, which means that the entire 16 bit register is read or
written (versus individual bits). Within the MDIO register space, there are several different bit types. A
list of these bit types are listed in Table 10-2.

Table 10-2. Field Types within the MDIO Register Space
      Type                                                          Description

LL              Latching Low
                If the condition the bit is monitoring goes low, this bit latches low, generates a maskable interrupt, and stays low
                until read. Reading this bit resets it to one. This bit is read-only.

LH              Latching High
                If the condition the bit is monitoring goes high, this bit latches high, generates a maskable interrupt, and stays
                high until read. Reading this bit resets it to zero. This bit is read-only.

LRF             Latch Rising or Falling
                Set high on either a rising or falling edge. If a transition occurs, this bit latches high, generates a maskable
                interrupt, and stays high until read. Reading this bit resets it to zero. This bit is read-only.

PD              Provisionable Defaults
                Indicates that the default value associated with this field is provisionable.

RO              Read-Only
                Read-only field. Writes are ignored.

ROS             Read Only Static
                Read-only static field. The same value is always returned. Writes are ignored.

RSV             Reserved
                Reserved for future use.

RW              Read/Write
                Field can be both read from and written to.

SC              Self-Clearing
                A read/write register which resets itself upon completion of an action.

SCT             Saturating Counter
                A read-only counter that saturates at the limit, and is cleared on read.

SCTL            Saturating Counter LSW
                The Least Significant Word of a Saturating Counter. This register clears the pair to zero on read and snapshots the
                mate MSW to shadow memory, awaiting read.

SCTM            Saturating Counter MSW
                The Most Significant Word of a Saturating Counter. Reading this completes the read process of the register pair.

862                                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.1.3 Structure

The following structure is used for registers:
1. All Clause 45 registers (registers defined in Clause 45) are placed in their respective areas within
   the MMDs as specified.
2. Intel specific registers associated with each of the Clause 45 MMDs are placed in the Intel specific
   area beginning at 0xC000, according to the register map listed in Table 10-3.

    Table 10-3. Register Layout
        Base Offset (Hex)                                                  Description

               C000              Tx & Overall MMD Control

               C400              Tx & Overall MMD Provisioning

               C800              Tx & Overall MMD State

               CC00              Tx & Overall MMD Alarms

               D000              Standard Interrupt Mask

               D400              Tx & Overall MMD Interrupt Mask

               D800              Tx & Overall MMD Debug

               DC00              Reserved

               E000              Rx Control

               E400              Rx Provisioning

               E800              Rx State

               EC00              Rx Alarms

               F000              Standard Interrupt Mask

               F400              Rx Interrupt Mask

               F800              Rx Debug

               FC00              Global Interrupt Flags

    The table is split into a transmit portion, and a receive portion, with the transmit portion also
    containing any overall Intel specific registers for the MMD. In this table, the following definitions
    apply:

    Table 10-4. Terms Used within the Register Layout
                    Term                                                        Definition

     Control                          Action bits that affect the operation of the MMD, such as reset.

     Provisioning                     Static provisioning bits that control the behavior of the MMD.

     State                            Bits that reflect the state of the MMD.

     Alarm                            Bits that can generate maskable interrupts.

     Standard Interrupt Mask          Interrupt masks for alarm bits defined in the Clause 45 register set.

     Intel Specific Interrupt Mask    Interrupt masks for Intel Specific alarms.

333369-009                                                                                                    863
                                     Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                  PHY Registers

3. Interrupts are handled in an hierarchical fashion, with the PHY top level interrupt indication being
   reported in the EICR register. Below this are two maskable interrupt trees: one composed of
   standard interrupts, and one composed of Intel defined interrupts. The top level summary register
   for these trees resides at the end of the register space in MMD #30 - the Global PHY Standard
   Interrupt Flags (1E.FC00). Feeding this are interrupt registers from each of the individual MMDs.
      a. The standard interrupt tree is designed so that the source of any interrupt can be determined in
         a maximum of two MDIO reads.
      b. The Intel defined interrupt tree requires at most three MDIO reads to determine the source of
         an interrupt.
      c. All interrupts are maskable, whether they are from the Standard interrupt tree, or from the Intel
         Specific interrupt tree.

### 10.1.4 PHY Registers and Documentation

The PHY registers for X550 are provided in the following tables, listed by the numerical order of their
MMD address.

864                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers
