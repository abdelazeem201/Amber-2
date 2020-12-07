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

![Figure 1 - Amber 23 Core pipeline stages]


## 2 Amber 23 Pipeline Architecture
The Amber 2 core has a 3-stage pipeline architecture. The best way to think of the
pipeline structure is of a circle. There is no start or end point. The output from each
stage is registered and fed into the next stage. The three stages are;

• Fetch – The cache tag and data RAMs receive an unregistered version of the
address output by the execution stage. The registered version of the address is
compared to the tag RAM outputs one cycle later to decide if the cache hits or
misses. If the cache misses, then the pipeline is stalled while the instruction is
fetched from either boot memory or main memory via the Wishbone bus. The
cache always does 4-word reads so a complete cache line gets filled. In the
case of a cache hit, the output from the cache data RAM goes to the decode
stage. This can either be an instruction or data word.

• Decode - The instruction is received from the fetch stage and registered. One
cycle later it is decoded and the datapath control signals prepared for the next
cycle. This stage contains a state machine that handles multi-cycle instructions
and interrupts.

• Execute – The control signals from the decode stage are registered and passed
into the execute stage, along with any read data from the fetch stage. The
operands are read from the register bank, shifted, combined in the ALU and the
result written back. The next address for the fetch stage is generated.
The following diagram shows the datapath through the three stages in detail. This
diagram closely corresponds to the Verilog implementation. Some details, like the
wishbone interface and coprocessor #15 have been left out so as not to overload the
diagram completely
