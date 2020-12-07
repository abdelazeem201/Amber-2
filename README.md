## 1. Introduction
The Amber processor core is an ARM-compatible 32-bit RISC processor. The Amber
core is fully compatible with the ARM® v2a instruction set architecture (ISA) and is
therefore supported by the GNU toolset. This older version of the ARM instruction
set is supported because it is not covered by patents so can be implemented without a
license from ARM. The Amber project provides a complete embedded system
incorporating the Amber core and a number of peripherals, including UARTs, timers
and an Ethernet MAC.

There are two versions of the core provided in the Amber project. The Amber 23 has
a 3-stage pipeline, a unified instruction & data cache, a Wishbone interface, and is
capable of 0.8 DMIPS per MHz. 

The Amber 23 core is a very small 32-bit core that provides good performance.
Register based instructions execute in a single cycle, except for instructions involving
multiplication. Load and store instructions require three cycles. The core's pipeline is
stalled either when a cache miss occurs, or when the core performs a wishbone
access.

## 1.1 Amber 23 Features
• 3-stage pipeline. 

• 32-bit Wishbone system bus.

• Unified instruction and data cache, with write through and a read-miss
replacement policy. The cache can have 2, 3, 4 or 8 ways and each way is 4kB.

• Multiply and multiply-accumulate operations with 32-bit inputs and 32-bit
output in 34 clock cycles using the Booth algorithm. This is a small and slow
multiplier implementation.

• Little endian only, i.e. Byte 0 is stored in bits 7:0 and byte 3 in bits 31:24.


The following diagram shows the data flow through the 3-stage core.
