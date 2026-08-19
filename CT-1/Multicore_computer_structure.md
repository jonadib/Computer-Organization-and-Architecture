# Multicore Computer Structure

A multicore computer has two or more CPU cores on a single chip (die). Each core works like an independent processor.

It improves performance, speed, and multitasking while using less power than increasing the speed of a single core.

## Main Components of a Core

Each core contains:

- **Registers** — Store temporary data.
- **ALU (Arithmetic Logic Unit)** — Performs calculations and logical operations.
- **Control Unit (CU)** — Controls instruction execution.
- **L1 Cache** — Small, fast memory for quick data and instructions.
- **Pipeline Hardware** — Executes multiple instruction stages efficiently.

## Cache Organization

Cache memory stores frequently used data to speed up processing.

### Dedicated Cache

- Each core has its own L1 (and sometimes L2) cache.
- Faster access for that core.

### Shared L2 Cache

- Multiple cores share one L2 cache.
- Makes sharing data between cores easier.
- Reduces duplicate data.

### Shared L3 Cache

- Each core has its own L1 and L2 cache.
- All cores share a larger L3 cache.
- Common in modern processors.

## On-Chip Management

These units help all cores work together.

- **APIC (Advanced Programmable Interrupt Controller)** — Allows one core to send signals (interrupts) to another core.
- **Power & Thermal Management** — Monitors chip temperature and reduces clock speed if the chip gets too hot.
- **Cache Coherency (SCU)** — Ensures all cores see the same and updated data in memory and prevents data inconsistency.

## External Connectivity

- **Memory Controller** — Built into the processor; provides faster communication with RAM.
- **High-Speed Interconnect** — Connects processors at high speed and allows fast data sharing between processor chips.

## Key Advantages

- Higher performance
- Better multitasking
- Lower power consumption
- Faster processing
- Better resource sharing

## Easy Diagram

```
                Multicore Processor
      +-----------------------------------+
      |           Shared L3 Cache          |
      +-----------------------------------+
          |             |             |
     +---------+   +---------+   +---------+
     | Core 1  |   | Core 2  |   | Core 3  |
     |---------|   |---------|   |---------|
     |Registers|   |Registers|   |Registers|
     |  ALU    |   |  ALU    |   |  ALU    |
     | Control |   | Control |   | Control |
     | L1 Cache|   | L1 Cache|   | L1 Cache|
     +---------+   +---------+   +---------+
            \          |          /
             \         |         /
        Memory Controller & Management
     (APIC, Thermal Control, Cache Coherency)
                    |
                   RAM
```

## Exam Summary (2–3 Marks)

**Multicore Computer Structure:**
A multicore computer contains two or more processor cores on a single chip. Each core has its own registers, ALU, control unit, and L1 cache. Cores may share L2 or L3 cache for efficient data access. Management units such as APIC, thermal control, and cache coherency logic help the cores communicate and work correctly. Modern multicore processors also include an integrated memory controller for faster access to RAM.

## Memory Trick

- **Core** → Does the processing.
- **L1 Cache** → Fast private memory.
- **L2/L3 Cache** → Shared memory.
- **APIC** → Core-to-core communication.
- **SCU** → Keeps cache data consistent.
- **Memory Controller** → Connects CPU to RAM quickly.

## Differences Between Multiprocessor and Multicore

| Feature               | Multiprocessor (SMP)        | Multicore (CMP)                   |
| --------------------- | --------------------------- | --------------------------------- |
| **Processors**        | Multiple separate CPU chips | Multiple cores in one CPU chip    |
| **Location**          | On different chips          | On the same chip (die)            |
| **Communication**     | Through system bus          | Through fast on-chip interconnect |
| **Cache**             | Mainly share main memory    | Often share L2/L3 cache           |
| **Speed**             | Slower communication        | Faster communication              |
| **Power Consumption** | Higher                      | Lower and more efficient          |
| **Main Use**          | Servers and supercomputers  | PCs, laptops, smartphones         |
