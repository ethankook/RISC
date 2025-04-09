# RISC Processor
Completed
Overview: This project involved the design and implementation of a custom RISC-style processor with 8 general-purpose registers and a compact instruction set architecture. The goal was to build a minimal yet functional CPU capable of executing arithmetic, logic, and branch instructions, including support for 16-bit integer and 16-bit IEEE-754 floating-point data conversions and addition/subtraction. We used the processor's custom instruction set to write a program in Assembly Language to handle the conversion and computations. A custom compiler for the instruction set, to convert the program from ASM to machine code was also created using C++.

Key Features:

Register-register / Load-store architecture with direct and indirect addressing
Optimized register file design, prioritizing registers 0 to 3 for frequently accessed operations, while 4 to 7 are utilized for storage. Special handling of 0 as the implied destination for certain branch comparisons.
LUT-based conditional branching and control flow, storing up to 32 jump locations
Custom instructions for logical shifts, bit manipulation, and subroutine handling
Logical shigts can span one or two registers.
Support for 16-bit integer and 16-bit IEEE-754 floating-point data types
8-bit wide, 256-byte deep memory, to support indirect addressing during memory access instructions
The ALU also supports a comparison operation. Given two registers (R0 and R1), it will compare the data in these registers and return one of three values..
Control unit to decode the instruction code (op-code) and manage the flow of data across the data path.
Technology Used: Verilog, SystemVerilog, C++, ModelSim, waveform analysis tools, Assembly Language(ASM)

Process: The processor architecture was designed from the ground up, starting with the instruction set and register file. An ALU module was built to support both standard arithmetic and custom bitwise operations. A memory subsystem handled instruction and data memory independently. Testing was performed with custom testbenches and waveform outputs to validate correctness at each stage.

Challenges: Addressing edge cases in floating-point conversion, handling operand ordering in memory instructions, and eliminating infinite loop scenarios in early branch logic prototypes.

Accomplishments: Delivered a functioning RISC processor capable of running multiple programs with clean modularity and real-time branching. Achieved stable signal timing and logic under extensive test conditions.

Instruction Set Overview:

Instruction	Type	Description	Bit Breakdown
and	R	Logical AND between two registers	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0000
or	R	Logical OR between two registers	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0001
lsl	R	Logical shift left	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0010
lsr	R	Logical shift right	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0011
add	R	Add two registers	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0100
sub	R	Subtract one register from another	8: branch (0), 7–6: src, 5–4: dest, 3–0: 1101
neg	R	Negate register value	8: branch (0), 7–6: src, 5–4: dest, 3–0: 0101
ldr	R	Load value from memory	8: branch (0), 7–6: addr, 5–4: dest, 3–0: 0110
str	R	Store register to memory	8: branch (0), 7–6: src, 5–4: addr, 3–0: 0111
mov	R	Move immediate to register	8: branch (0), 7–4: value, 3–0: 1000
mot	R	Move to/from R0	8: branch (0), 7–5: reg, 4: direction, 3–0: 1001
lso	R	1-bit logical shift	8: branch (0), 7–5: reg, 4: L/R, 3–0: 1010
cfb	R	Check first bit	8: branch (0), 7–5: reg, 4: dead, 3–0: 1011
cmp	R	Compare registers	8: branch (0), 7–6: dest, 5–4: src, 3–0: 1100
mbs	R	Move bits	8: branch (0), 7–5: reg, 4: bit count, 3–0: 1110
beq	B	Branch if equal	8: branch (1), 7–6: reg, 5: 0, 4–0: LUT index
bne	B	Branch if not equal	8: branch (1), 7–6: reg, 5: 1, 4–0: LUT index
