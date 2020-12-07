## Introduction
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
