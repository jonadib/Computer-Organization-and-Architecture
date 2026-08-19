# CSE 2231 – Computer Architecture and Organization
### Topic-wise Question Bank (University of Rajshahi, 2018–2024 past papers)

---

## 📋 TOPICS TO MASTER

1. **Fundamentals** – Generations of computers, Architecture vs Organization, IAS computer, RISC vs CISC, multicore/multiprocessor
2. **CPU Organization** – Accumulator-based / stack-based / register-based CPU, register files, status register, stack pointer
3. **Performance Metrics** – CPI, MIPS, clock speed, latency, throughput, execution time
4. **Instruction Cycle, Addressing Modes & Data Manipulation Instructions**
5. **Interrupts** – Types, priority interrupts, polling vs interrupts, ISR, vectored/non-vectored interrupts
6. **Pipelining** – Instruction-level pipelining, speedup, throughput
7. **Number Representation & Adders** – Signed magnitude, 2's complement, ripple-carry adder, carry-lookahead adder, adder-subtractor, overflow detection
8. **Multiplication, Division & Floating-Point Arithmetic** – Booth's algorithm, binary multiplier, floating-point representation & arithmetic
9. **ALU Design** – Fixed-point ALU, bit-sliced ALU (2901), 74181 ALU, multiport RAM/datapath
10. **Control Unit Design** – Hardwired vs microprogrammed, one-hot method, GCD controller, Wilkes design, control signals
11. **Memory – RAM/DRAM/SRAM Organization** – Destructive/non-destructive readout, 2D DRAM, Rambus DRAM, synchronous DRAM, interleaved memory
12. **Memory – Cache** – Direct/associative/set-associative mapping, hit ratio, cache performance
13. **Memory – Virtual Memory, Paging, Segmentation, TLB, Address Translation**
14. **Memory – Page Replacement Algorithms** – FIFO, LRU
15. **Memory – Allocation Policies & Fragmentation** – Contiguous/non-contiguous, preemptive/non-preemptive, internal/external fragmentation, thrashing
16. **Bus Organization & Arbitration** – Synchronous/asynchronous bus, tri-state logic, daisy chaining, mezzanine architecture, polling
17. **I/O Organization & Data Transfer** – I/O processor, memory-mapped vs I/O-mapped I/O, peripherals, synchronous/asynchronous/strobe-controlled transfer
18. **DMA Controller** – Functions, block diagram, state transition design, timing calculations

---

## 1. Fundamentals (Generations, Architecture vs Organization, IAS, RISC vs CISC)

1. [2018] Q1a) Distinguish between computer architecture and computer organization. *(2.75)*
2. [2018] Q1b) Define IAS computer. Discuss the organization of the CPU and main memory of the IAS computer. *(4)*
3. [2018] Q1c) Mention some important features of third generation computers. *(2)*
4. [2018] Q2b) Discuss the architectural extension of recent CPUs compared with a small accumulator-based CPU, with necessary figures. *(4.75)*
5. [2019] Q1a) Define structure and function of computer. Discuss the structural development among different generations of computer in brief. *(4)*
6. [2019] Q1b) Distinguish between RISC and CISC machines. *(1.75)*
7. [2020] Q1a) What is meant by 16-bit computer? Explain how operating system bridges the gap between software and hardware. *(3.00)*
8. [2020] Q8c) Distinguish between CISC and RISC processors. *(2.00)*
9. [2021] Q1a) Define the functional elements of a core. Explain the structure of a multicore computer. *(2.75)*
10. [2021] Q2c) What do you mean by CISC and RISC processors? Mention some features of RISC processors. *(2.75)*
11. [2022] Q1a) Define Multiprocessor and multicore computer. How is cache memory used to speed up memory access? How can a greater performance improvement be obtained by using multiple levels of cache? *(2.75)*
12. [2023] Q1a) How does the IAS computer execute an instruction? Describe the fetch-execute cycle with an example. *(2.75)*
13. [2024] Q1c) What are the differences between RISC and CISC machines? *(2.75)*
14. [2024] Q4a) What are the main components of the extended IAS computer architecture, and how does the control unit in the extended IAS computer manage the execution of instructions? *(3)*

## 2. CPU Organization (Accumulator/Stack/Register-based CPU)

1. [2018] Q4c) Discuss the register-level view of the 74181 4-bit ALU. *(4)* — *(cross-ref with Topic 9)*
2. [2021] Q2a) Draw the structure of a small accumulator-based CPU. Explain the functions of the register files, status register, and stack pointer. *(3)*
3. [2022] Q4a) Draw and discuss the block diagram of a simple accumulator-based CPU. *(3)*
4. [2023] Q3a) Explain the advantages and disadvantages of an accumulator-based CPU. *(3.0)*
5. [2023] Q3b) Compare an accumulator-based CPU with a stack-based CPU and a register-based CPU. *(3.0)*
6. [2024] Q4b) Define clock speed and explain how it affects the performance of a computer system. Why might a processor with a higher clock speed not always perform better than one with a lower clock speed? Explain with an example. *(3)*

## 3. Performance Metrics (CPI, MIPS, Clock Speed, Latency/Throughput)

1. [2020] Q1b) Define latency and throughput. Explain the factors influencing computer speed. *(3.00)*
2. [2020] Q1c) Two processors A and B, clock period 5ns and 10ns respectively; average 5.4 and 4.5 clock cycles per instruction. Compare the performance of the two processors. *(2.75)*
3. [2021] Q1b) Mention the names of registers in the control unit and discuss their functions. Calculate CPI and MIPS for a CPU with 100 MHz frequency executing a benchmark program: ALU (occurrence 38%, cycle/instr 1), LOAD & STORE (occurrence 15%, cycle/instr 3), Others (occurrence 47%, cycle/instr 5). *(3)*
4. [2022] Q1b) How does the control unit execute instructions? How does it interact with other components of a CPU? A 200 MHz processor executes a program with a given instruction mix and clock cycle counts (integer arithmetic, data transfer, floating point, control transfer). Determine the effective CPI, MIPS rate, and execution time. *(4)*
5. [2023] Q1b) Two microprocessors, Machine A and Machine B, are evaluated for a benchmark program with given clock rate, instruction count and CPI. 1) Calculate execution time for each. 2) Determine effective CPI for each. 3) Find MIPS rate for each. 4) Which machine is faster, and by what factor? *(2.0)*
6. [2023] Q1c) A hypothetical microprocessor generates a 16-bit address and has a 16-bit data bus. i) Maximum memory address space if connected to a "16-bit memory"? ii) If connected to an "8-bit memory"? *(2.0)*
7. [2023] Q1d) Why is MIPS not always a reliable metric for comparing different processors? *(2.0)*
8. [2023] Q3c) A CPU with an accumulator executes a sequence where 60% of instructions involve arithmetic operations and the rest involve memory accesses. Arithmetic = 3 cycles, memory access = 2 cycles. Compute the average CPI. *(2.75)*

## 4. Instruction Cycle, Addressing Modes & Data Manipulation Instructions

1. [2018] Q2c) Define instruction pipelining. *(2)* — *(cross-ref Topic 6)*
2. [2018] Q8c) What do you mean by addressing mode? Shortly discuss indirect addressing mode. *(2.75)*
3. [2020] Q2b) Explain instruction cycle with example. *(3.00)*
4. [2020] Q2c) Define addressing mode. Describe the instructions R1←M[B]+R3; R2←M[M[ADR]]+M[PC+H] with respect to addressing mode. *(2.75)*
5. [2020] Q3b) Discuss about different types of data manipulation instructions. *(3.00)*
6. [2020] Q5a) Discuss about program control instructions. *(2.00)*
7. [2020] Q5b) A CPU has only 3 registers connected as input through two multiplexers MUX A and MUX B, and as output through multiplexer MUX D. The CPU supports 4 instructions (ADD, SUB, MUL, DIV). Draw the register organization and write the codewords of the instructions: R3←R2+R1; R1←R3-R2; R2←R1*R3. *(3.75)*
8. [2022] Q1c) A 16-bit hypothetical machine has two I/O instructions: 0011 Load AC from I/O and 0111 Store AC to I/O. The 12-bit address identifies a particular I/O device. Show the program execution (contents of memory and registers in hexadecimal) for: Load AC from device 5, Add contents of memory location 940, Store AC to device 6, given device 5 next value = 3 and location 940 = 2. *(2)*
9. [2024] Q2c) Explain the difference between immediate, direct, and indirect addressing modes. A CPU executes LOAD AC, #30. 1) What value is loaded into the accumulator? 2) If the next instruction is ADD AC, #15, what will be the new value of AC? *(3)*

## 5. Interrupts

1. [2020] Q3a) What is interrupt service routine? Compare vectored and non-vectored interrupts. *(2.75)*
2. [2021] Q1c) Mention the classes of interrupts. How can multiple interrupts be handled? *(3)*
3. [2022] Q2a) Define interrupt. How are interrupts provided primarily as a way to improve processing efficiency? Discuss with necessary diagrams. *(2.75)*
4. [2022] Q2c) Define fetch cycle and execute cycle with and without interrupt. *(2)*
5. [2023] Q2a) If an interrupt occurs during the execution of an instruction, explain the process of saving the processor state and returning to normal execution after the interrupt is serviced. *(3.0)*
6. [2023] Q2b) Define the concept of priority interrupt. A system with sequential and priority interrupts for devices D1–D4 (priorities D1 highest, D4 lowest), each taking 2ms; interrupts arrive at given times. Determine the order of processing and total time required using sequential and priority handling. When is sequential interrupt handling more efficient? *(3.0)*
7. [2023] Q8c) What is interrupt service routine? Distinguish between vectored and non-vectored interrupts with example. *(2.75)*
8. [2024] Q2a) What is an interrupt? Describe the steps a CPU takes when servicing an interrupt. *(3)*
9. [2024] Q2b) A CPU controls a keyboard. Using polling, the CPU checks the keyboard every 1 ms, but the keyboard generates a keypress every 50 ms. Using interrupts, the CPU only responds when a key is pressed. 1) Calculate the wasted CPU checks if polling is used for 1 second. 2) Explain how interrupts reduce wasted CPU cycles in this scenario. 3) Discuss situations where polling might still be preferable to interrupts. *(3)*
10. [2024] Q7c) What is an Interrupt Service Routine? Explain its role in a computer system and describe the steps that occur from the moment an interrupt is generated until the ISR completes execution. *(2.75)*

## 6. Pipelining

1. [2018] Q2c) Define instruction pipelining. *(2)*
2. [2020] Q5c) Explain how pipelining improves performance. A processor with 2.5 GHz clock and 4 blocks for pipelining runs a program with 3×10⁵ instructions where only 45% can be executed through pipelining. Calculate the speedup factor. *(3.00)*
3. [2021] Q2b) Describe instruction-level pipelining with necessary diagram. A minicomputer has a 12-bit address bus; find the address space and the largest possible memory in bytes (memory location = 1 byte). *(3)*
4. [2023] Q2c) How does pipelining increase the speed of computing? Stage delays in a 4-stage pipeline are 800, 500, 400, 300 ns. The first stage is replaced with two stages of 600 and 350 ns. Find the percentage increase in throughput. *(2.75)*
5. [2024] Q4c) What are the main techniques used in modern computers to enhance processing speed? A processor has a 5-stage instruction pipeline, each stage takes 2 ns to complete. Without pipelining, each instruction takes 10 ns. 1) Calculate the execution time for 20 instructions with and without pipelining. 2) Determine the speedup achieved by pipelining. *(2.75)*

## 7. Number Representation & Adders (2's Complement, Ripple-Carry, Carry-Lookahead, Overflow)

1. [2018] Q4a) Define overflow. How is overflow detection logic implemented? *(2)*
2. [2018] Q4b) Draw the overall structure of a high speed adder. *(2.75)*
3. [2019] Q3a) Write the logical expression of a full adder and half adder. Draw the circuit of an n-bit two's complement adder-subtractor. *(3.75)*
4. [2019] Q3b) What is carry lookahead adder? Draw a 2-bit carry lookahead adder in detail. *(5)*
5. [2020] Q4c) Distinguish between Ripple-carry adder and Carry-lookahead adder with diagram. *(2.75)*
6. [2021] Q3a) Mention some drawbacks of signed magnitude representation. Derive the equation of 2's complement representation of signed integers. *(2.75)*
7. [2021] Q3b) Design an 8-bit adder-subtractor with a diagram. *(3)*
8. [2021] Q3c) How is overflow handled in an adder circuit? Discuss the logical expression and logic circuit of overflow detection. *(3)*
9. [2022] Q3a) What is the problem with signed-magnitude representations? How can the 2's complement method be used to solve the problem? How can a full adder be realized using two half-adders? *(3)*
10. [2022] Q3b) Design an 8-bit 2's complement adder-subtractor (using 4-bit adder module) that can perform X-Y, X+Y, Y-X operations. *(3)*
11. [2022] Q3c) Discuss some cases where overflow occurs. Derive the logical expression and draw the logic circuit of overflow detection. *(2.75)*
12. [2022] Q4c) Write the differences between Ripple carry adder and Carry-lookahead adder. *(2)*
13. [2024] Q3a) Explain the main difference between a serial binary adder and a parallel binary adder. How does a carry look-ahead adder improve the speed of addition compared to a ripple carry adder? *(2.75)*
14. [2024] Q3b) What is the difference between carry and overflow in binary addition? A 4-bit binary adder adds A = 1101 and B = 1011. Determine the sum, the carry-out, and whether an overflow occurs if the numbers are treated as signed 2's complement. *(3)*
15. [2024] Q3c) Using a 4-bit adder module, design an 8-bit circuit that can perform X+Y, X-Y, Y-X. In the circuit, show how overflow and zero can be detected. *(3)*

## 8. Multiplication, Division & Floating-Point Arithmetic

1. [2018] Q3a) Design a multiplier that can multiply two fixed-point signed binary numbers. Give the algorithm and flowchart for the multiplication process. *(5.75)*
2. [2018] Q3b) Describe the data processing part of a simple floating-point arithmetic unit with diagram. *(3)*
3. [2019] Q2b) Derive and explain an algorithm for adding and subtracting 2 floating point binary numbers. *(4)*
4. [2019] Q2c) Explain the representation of floating point numbers in detail. *(1.75)*
5. [2021] Q4a) Why does fixed-point multiplication require more hardware than fixed-point addition? Design a 2-bit binary multiplier circuit. *(2.75)*
6. [2021] Q4b) Mention some features of Booth's algorithm in the multiplication process. How does the algorithm work? Explain with an example. *(3)*
7. [2022] Q2b) *(Floating-point part)* Suppose a 16-bit register stores binary floating point numbers, with mantissa (M) as normalized sign-magnitude fraction and exponent (E) in excess-64 form. 1) How many bits are used for the fractional mantissa? 2) What are the bit patterns for (7.5)₁₀ and (-16.125)₁₀? *(part of 2+2)*
8. [2023] Q5a) Define base-mantissa representation and explain its significance in floating-point numbers. *(3.0)*
9. [2023] Q5b) What is two's complement representation? Why is it preferred over signed magnitude for arithmetic operations? *(1.25)*
10. [2023] Q5c) A floating-point system uses 6-bit mantissa and 3-bit exponent. Determine the range of numbers that can be represented in this system. *(1.50)*
11. [2023] Q5d) Two numbers stored in 8-bit signed magnitude format: 01011010 (90) and 10100110 (-38). Perform their binary addition and indicate whether overflow occurs. *(1.50)*
12. [2023] Q5e) A system uses 16-bit two's complement representation. What is the largest positive and smallest negative number that can be represented? *(1.50)*

## 9. ALU Design (Fixed-point, Bit-sliced, 74181, Multiport RAM/Datapath)

1. [2018] Q4c) Discuss the register-level view of the 74181 4-bit ALU. *(4)*
2. [2019] Q4a) Explain spatial and temporal expansion of a bit sliced ALU. Also show the organization of the 2901 4-bit ALU slice. *(4)*
3. [2019] Q4b) Draw the symbol and logic diagram of a three port RAM. Also discuss a generic datapath unit with an ALU and a multiport RAM. *(4.75)*
4. [2020] Q4a) Briefly describe the structure of a fixed point ALU with diagram. *(3.00)*
5. [2020] Q4b) Shortly discuss how a 16-bit bit-sliced ALU is designed by four 4-bit ALU slices. *(3.00)*
6. [2021] Q4c) What is multiport RAM? Draw its symbolic representation. Draw a generic datapath unit for implementing logical and arithmetic operations. *(3)*
7. [2022] Q4b) Discuss how a 16-bit Bit-Sliced ALU is designed by four 4-bit ALU slices. *(3.75)*
8. [2024] Q1a) Describe the structure of a fixed point ALU with proper diagram. *(3)*
9. [2024] Q1b) How can you design a 16-bit bit-sliced ALU by using four 4-bit ALU slices? Explain properly. *(2)*

## 10. Control Unit Design (Hardwired, Microprogrammed, One-Hot, GCD Controller, Wilkes Design)

1. [2018] Q5a) What are the functions of the control unit in a computer system? Discuss the possible control signals generated to implement a subtraction instruction of the form SUB A,B with DP unit figure. *(3.75)*
2. [2019] Q7a) What is the function of control unit? Show the control signals that implement a subtraction instruction of the form SUB A, B. *(3.75)*
3. [2019] Q7b) Design a processor that performs factorial of a positive integer. *(5)*
4. [2020] Q2a) Compare hardwired and microprogrammed controls. How does PC work for branching instructions? *(3.00)*
5. [2020] Q8a) Design a micro-programmed control unit based on Wilkes design. *(4.00)*
6. [2021] Q7a) How can the micro programmed control circuit be designed? Give example. *(2)*
7. [2021] Q7b) Show the basic structure of the hardwired control unit in brief. *(2)*
8. [2021] Q7c) Design the control unit of the GCD processor using the classical method. *(4.75)*
9. [2022] Q7a) Mention different approaches to the design of hardwired control units with benefits and limitations. *(2)*
10. [2022] Q7b) Design the control unit of the GCD controller: draw state transition graph, state table and also logic diagram using the one-hot method. *(4.75)*
11. [2022] Q7c) Draw the structure of a hardwired and microprogrammed control unit. *(2)*
12. [2023] Q7a) How does hardware control differ from microprogrammed control? Discuss the key components of a hardware control unit. *(2.75)*
13. [2023] Q7b) What are the key differences in state management between a One-Hot control unit and a classical binary control unit in a GCD processor? Explain. *(4.0)*
14. [2023] Q7c) How does a microprogrammed control unit work? Discuss with a diagram. *(2.0)*

## 11. Memory – RAM/DRAM/SRAM Organization

1. [2018] Q6a) Define destructive readout (DRO). Give example. *(2)*
2. [2019] Q5a) Define destructive and nondestructive readout. Discuss how restoration is carried out automatically with necessary diagram. *(3)*
3. [2019] Q5b) Draw the organization of 2D DRAM. *(1.75)*
4. [2019] Q5c) How do you increase the data transfer rate between RAM and CPU? Draw the Rambus DRAM interface. *(4)*
5. [2019] Q8b) Explain synchronous DRAM technology in detail. *(3.75)*
6. [2020] Q8b) Explain the concepts of interleaved memories. *(2.75)*
7. [2021] Q5a) Discuss memory restoration in destructive readout memory. Design 16-bit 2-D RAM using dynamic RAM cells and show the RAM addressing scheme. *(2.75)*
8. [2022] Q5a) Discuss any two characteristics that destroy information from memory. Draw the internal structure of the 8×1 DRAM chip. *(2.75)*
9. [2024] Q5b) What are the main components of SRAM and DRAM? Draw the 2D organization of RAM. Given a 16×8 bits RAM IC, design a RAM by increasing the number of words by a factor of 3 (RAM size = 48×8 bits). *(3)*

## 12. Memory – Cache

1. [2018] Q8a) Discuss how cache memory helps to speed up the operation of a computer system. *(3)*
2. [2020] Q7c) Explain the function of cache memory to speed up computer system. 420 of 600 memory references are available in the cache. Calculate the cache performance. *(2.75)*
3. [2021] Q6b) Draw the basic structure of a cache. What are the limitations of direct and associative cache mapping techniques? How are those problems overcome using set-associative mapping? Discuss with an example. *(2.75)*
4. [2022] Q6b) How does set-associative mapping work? Discuss with an example. A digital computer has a memory unit of 64K×16 and a cache memory of 1K words, using direct mapping with a block size of four words. How many bits are there in the tag, index, block and word fields of the address? *(3)*
5. [2023] Q6a) Explain the difference between direct-mapped, associative, and set-associative cache mapping. *(2.75)*
6. [2023] Q6b) A digital computer has byte-addressable Main memory size = 512 MB, Cache size = 2MB and Block size = 256 B. Show physical address split using 2-way and 4-way set associative mapping and state the observations. *(3.0)*
7. [2024] Q6a) Compare different cache mapping techniques in terms of hardware complexity, hit ratio, and speed. Which one provides the best overall performance and why? *(2.75)*
8. [2024] Q6b) A digital computer has a byte-addressable main memory of size 256 MB, a cache of size 1 MB, and a block size of 128 bytes. Show how the physical address is divided using: a) Direct Mapping b) Fully Associative Mapping. Compare and explain the observations for both mapping techniques. *(4)*
9. [2024] Q6c) If the hit ratio is low, what will happen among memory units? Discuss. *(2)*

## 13. Memory – Virtual Memory, Paging, Segmentation, TLB, Address Translation

1. [2018] Q6b) Define address mapping. Discuss the structure of a dynamic address-translation system. *(4)*
2. [2018] Q8b) Explain the concept of virtual memory and interleaved memory. *(3)*
3. [2019] Q6a) What is address mapping? What is the function of address generation logic? Explain. *(1.75)*
4. [2019] Q6b) What is Translation lookaside buffer? Discuss two stage address translation with segments and pages. *(3)*
5. [2020] Q7b) Illustrate the function of virtual memory. A computer system needs 512B RAM and 512B ROM, but only memory chips (RAM and ROM) of size 256B are available. Draw the diagram to illustrate the memory connection. *(3.00)*
6. [2021] Q5b) Discuss the structure of the address-translation system using translation look-aside buffer with the paging hardware. Main memory and TLB access times are 100ns and 60ns respectively; TLB hit ratio is 99%. What is the effective access time? *(3)*
7. [2021] Q6c) Mention some benefits of using virtual memory. Discuss the steps in handling a page fault. Memory access time is 200ns and page fault service time is 8ms; 1 access out of 1000 causes a page fault. Calculate the effective access time. *(3)*
8. [2022] Q5b) How does TLB with the paging hardware speed up the address translation process? Discuss with a necessary figure. A system has logical address = 6 bits, physical address = 5 bits, page size = 16 words. Calculate the number of pages and frames. Also draw the page table. *(3)*
9. [2023] Q4a) How does paging eliminate external fragmentation? A system has a 32-bit virtual address space and a 4 KB page size. How many pages are there in virtual memory? *(3.0)*
10. [2023] Q4b) Given a TLB hit rate of 90% and page table lookup time of 100 ns, what is the effective memory access time if memory access takes 200 ns? *(2.75)*
11. [2023] Q6c) What is virtual memory, and how does it differ from physical memory? Explain the role of the page table in virtual memory management. *(3.0)*
12. [2024] Q8a) What do you mean by address translation? Explain a typical dynamic address translation system. *(5)*

## 14. Memory – Page Replacement Algorithms (FIFO, LRU)

1. [2019] Q6c) Consider a paging system in which M has a capacity of four pages. The execution of a program Q requires references to six distinct pages Pᵢ (i=1..6). The page address stream formed is 2,3,6,2,1,5,2,4,5,6,2,1. Show the action of three replacement policies in a common address trace. *(4)*
2. [2019] Q8a) In a cache-based memory system using FIFO for cache page replacement, the cache hit ratio H is low. Analyze each of the following proposals for its probable impact on H: (i) increase cache page size (ii) increase cache storage capacity (iii) increase main memory capacity (iv) replace FIFO with LRU. *(5)*
3. [2023] Q4c) Why is memory allocation important in computer architecture? Consider a system using the Least Recently Used (LRU) memory replacement policy with 3 frames and reference sequence: 1,2,3,4,1,2,5,1,2,3,4,5. What is the number of page faults? *(3.0)*
4. [2024] Q5c) Discuss where the FIFO and LRU page replacement policies are used. Each process is allocated with four physical memory frames only. Draw the physical memory frames and give the total number of page faults for the page reference string: 7 0 1 2 0 3 0 4 0 3 2 1 7 2 1. *(3)*

## 15. Memory – Allocation Policies & Fragmentation

1. [2018] Q6c) Define preemptive allocation with necessary figure. *(2.75)*
2. [2021] Q5c) What is internal fragmentation? Draw a schematic representation of hardware used for segmentation. *(3)*
3. [2021] Q6a) "Nonpreemptive allocation is not efficient" - why? And how is it solved in the preemptive allocation technique? A processor can support a maximum of 8GB where the memory is word addressable (a word = 4 bytes). What is the minimum size of the address bus of the processor? *(3)*
4. [2022] Q5c) What is internal fragmentation? Draw a schematic representation of hardware used for segmentation. *(3)*
5. [2022] Q6a) What is meant by thrashing? How is the preemptive allocation technique used for dynamic memory allocation? *(2.75)*
6. [2024] Q5a) What is contiguous and non-contiguous memory allocation policy? How do paging and segmentation work? Explain with an example. *(2.75)*

## 16. Bus Organization & Arbitration

1. [2018] Q7a) Distinguish between synchronous and asynchronous buses. Give example. *(2.75)*
2. [2018] Q7b) Discuss bus interfacing using tri-state logic with necessary figure. *(3)*
3. [2018] Q7c) Discuss bus arbitration using daisy chaining. Mention some problems with this scheme. *(3)*
4. [2021] Q8a) Define the term bus arbitration. What are the basic schemes for it? Which one is better in which situation? *(2.75)*
5. [2022] Q2b) How to control the access to and the use of the system bus? Discuss mezzanine architecture with the necessary figure. *(2+2, floating-point sub-part listed under Topic 8)*
6. [2022] Q8b) Define the term bus arbitration. What are the basic schemes for it? Which one is better in which situation? *(3)*
7. [2023] Q8a) How is polling used in bus arbitration? How does polling-based bus arbitration differ in respect of efficiency from other methods, and in what situations might polling be preferable? *(3.0)*
8. [2024] Q7a) Why is bus arbitration required? Justify which method you think is most efficient and explain why. *(3)*
9. [2024] Q8b) Explain the term bus arbitration. What are the basic schemes for it? Which one is better than other in what situation? *(3.75)*

## 17. I/O Organization & Data Transfer

1. [2018] Q2a) What do you mean by memory-mapped I/O and I/O mapped I/O? Give example. *(2)*
2. [2019] Q1c) Draw and briefly discuss the structure of an I/O processor. *(3)*
3. [2019] Q2a) Specify the different I/O transfer mechanisms available. *(3)*
4. [2020] Q3c) Explain I/O configuration with its proper block diagram. *(3.00)*
5. [2020] Q6a) Define peripherals with examples. Mention the requirements for I/O interface. *(2.75)*
6. [2020] Q6b) Compare synchronous and asynchronous data transfer. Explain asynchronous data transfer scheme and mention its advantages. *(3.00)*
7. [2020] Q6c) Discuss about strobe-controlled data transfer system with necessary diagram. *(3.00)*
8. [2021] Q8b) Define isolated I/O. How is the data transfer from the I/O device to the main memory carried out in the programmed I/O method? Discuss with the necessary figure. *(3)*
9. [2022] Q8c) Explain the concept of I/O processor. *(2)*

## 18. DMA Controller

1. [2018] Q5b) Design DMA controller: draw state transition graph, state table and also logic diagram using One-hot design method. *(5)*
2. [2020] Q7a) Mention the advantages of DMA. Illustrate the steps of DMA transfer from I/O to memory. *(3.00)*
3. [2021] Q8c) What are the functions of a DMA controller? Draw circuitry required for a DMA Controller. Which component of the computer system initiated the DMA transfer? Discuss with the necessary block diagram. *(3)*
4. [2023] Q8b) A hard disk with a data transfer rate of 10 MB/sec is continuously transferring data to memory using DMA. The processor operates at 600 MHz and requires 300 clock cycles to initiate the DMA transfer and 900 clock cycles to complete it. Given the transfer size is 10 KB, what percentage of the total time is consumed by the DMA transfer operation? *(3.0)*
5. [2024] Q7b) What are the main functions of a DMA controller? Draw the block diagram of a DMA controller showing its interaction with CPU, memory, and I/O devices. Discuss the advantages of using DMA over CPU-controlled data transfer. *(3)*

---

## 💡 Suggested Revision Strategy

- **Heaviest-weight topics** (appear almost every year, high marks): Cache mapping, Adders/Overflow, Control Unit design (hardwired/microprogrammed/GCD), Bus arbitration, DMA, Address translation/TLB, ALU (bit-sliced).
- **Numerical-heavy topics** to drill with practice problems: CPI/MIPS calculations, cache address splitting, page replacement (FIFO/LRU), pipelining speedup, effective access time (TLB), DMA timing %.
- **Diagram-heavy topics** to practice drawing from memory: fixed-point ALU, bit-sliced ALU, adder-subtractor circuit, GCD control unit (one-hot/classical), DMA controller block diagram, 2D DRAM/Rambus DRAM, cache mapping diagrams.

Want me to generate fully worked solutions (step-by-step) for the numerical questions, topic by topic, starting with any specific section?