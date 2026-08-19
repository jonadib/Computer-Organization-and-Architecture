# Computer Architecture — Topics

## Fundamentals

- Generations of computers
- Architecture vs Organization
- IAS computer
- RISC vs CISC
- Multicore / multiprocessor systems

## CPU Organization

- Accumulator-based, stack-based, and register-based CPU designs
- Register files, status register, stack pointer

## Performance Metrics

- CPI, MIPS, clock speed
- Latency, throughput, execution time

## Instruction Cycle & Addressing Modes

- Instruction cycle overview
- Addressing modes and data-manipulation instructions

## Interrupts

- Types of interrupts
- Priority interrupt handling
- Polling vs interrupt-driven I/O
- Interrupt Service Routine (ISR)
- Vectored and non-vectored interrupts

## Pipelining

- Instruction-level pipelining concepts
- Speedup and throughput considerations

## Number Representation & Adders

- Signed magnitude and two's complement
- Ripple-carry adder, carry-lookahead adder
- Adder-subtractor circuits and overflow detection

## Multiplication, Division & Floating-Point Arithmetic

- Booth's algorithm and binary multipliers
- Floating-point representation and arithmetic

## ALU Design

- Fixed-point ALU
- Bit-sliced ALU (e.g., 2901)
- 74181 ALU and multiport RAM/datapath considerations

## Control Unit Design

- Hardwired vs microprogrammed control
- One-hot method, GCD controller, Wilkes design
- Control signal generation

## Memory

### RAM / DRAM / SRAM Organization

- Destructive vs non-destructive readout
- 2D DRAM, Rambus DRAM, synchronous DRAM
- Interleaved memory

### Cache

- Direct-mapped, fully associative, set-associative mapping
- Hit ratio and cache performance metrics

### Virtual Memory

- Paging and segmentation
- TLB and address translation

### Page Replacement Algorithms

- FIFO, LRU (and others)

### Allocation Policies & Fragmentation

- Contiguous vs non-contiguous allocation
- Preemptive vs non-preemptive allocation
- Internal and external fragmentation, thrashing

## Bus Organization & Arbitration

- Synchronous vs asynchronous buses
- Tri-state logic and bus contention
- Daisy chaining, mezzanine architecture, polling

## I/O Organization & Data Transfer

- I/O processor concepts
- Memory-mapped vs I/O-mapped I/O
- Peripherals and transfer modes (synchronous, asynchronous, strobe)

## DMA Controller

- DMA functions and block diagram
- State transition design and timing calculations
