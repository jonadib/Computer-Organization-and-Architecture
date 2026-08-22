📨 Performance assessment is the process of measuring and comparing how well a processor or computer system performs.

When designing or buying a processor, performance is considered along with:

☑️ Cost
☑️ Size
☑️ Security
☑️ Reliability
☑️ Power consumption

📨 System Clock

The system clock controls all operations inside the CPU.
It sends regular electrical pulses that tell the processor when to perform each operation.

Examples of operations:

☑️ Fetch instruction
☑️ Decode instruction
☑️ Execute instruction
☑️ Store data

👉 Every operation starts with a clock pulse.

Clock Speed

Clock speed is the number of clock cycles per second.
It is measured in Hertz (Hz).

Examples:

☑️ 1 MHz = 1 million cycles/second
☑️  GHz = 1 billion cycles/second

👉 A 1 GHz processor receives 1 billion clock pulses every second.

Clock Cycle (Clock Tick)

A clock cycle (or clock tick) is one pulse of the system clock.

1 pulse = 1 clock cycle
Cycle Time

Cycle time is the time between two clock pulses.

Formula:

🔴 Cycle Time= 1 / Clock Speed
	​

	​


Example:

Clock speed = 2 GHz
Cycle time = 1 / 2 × 10⁹ = 0.5 ns
How is the Clock Generated?

The clock signal is produced by a quartz crystal.

Steps:

Quartz crystal creates a steady wave.
The wave is converted into digital pulses.
These pulses are sent continuously to the CPU.
Why Do We Need a Clock?

Signals inside the processor need time to travel between different parts.

The clock:

Synchronizes all CPU operations.
Ensures every signal becomes stable before the next operation starts.
One Instruction Needs Multiple Clock Cycles

An instruction is not completed in one clock cycle.

It usually goes through several steps:

Fetch instruction
Decode instruction
Load data
Execute operation
Store result

Therefore, one instruction may require multiple clock cycles.

Simple instructions → few cycles
Complex instructions → many cycles
Does Higher Clock Speed Always Mean Better Performance?

No.

A higher clock speed does not always mean a faster processor because performance also depends on:

CPU architecture
Number of cycles per instruction (CPI)
Pipeline design
Cache memory
Compiler and software optimization


🔴 MFLOPS vs MIPS

| MIPS                                | MFLOPS                                        |
| ----------------------------------- | --------------------------------------------- |
| Million Instructions Per Second     | Million Floating-Point Operations Per Second  |
| Counts **all machine instructions** | Counts only **floating-point calculations**   |
| Used for general-purpose programs   | Used for scientific and graphics applications |
| Depends on instruction set          | Focuses on numerical computation performance  |
