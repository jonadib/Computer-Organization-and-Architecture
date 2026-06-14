═══════════════════════════════════════════════════════════════════════════════
                           CISC vs RISC ARCHITECTURE
═══════════════════════════════════════════════════════════════════════════════

COMPARISON TABLE
───────────────────────────────────────────────────────────────────────────────
Feature                     │ CISC                              │ RISC
───────────────────────────────────────────────────────────────────────────────
Full Form                   │ Complex Instruction Set Computer  │ Reduced Instruction Set Computer
Number of Instructions      │ Large                             │ Small
Instruction Length          │ Variable                          │ Fixed
Addressing Modes            │ Many                              │ Few
Hardware Cost               │ High                              │ Lower
Instruction Complexity      │ Complex                           │ Simple
Execution Time              │ Multiple clock cycles             │ Usually single clock cycle
Memory Access               │ Directly on memory                │ Mainly on registers
Control Unit                │ Microprogrammed                   │ Hardwired
Examples                    │ Intel x86, Motorola 68000         │ ARM, MIPS, SPARC
───────────────────────────────────────────────────────────────────────────────


═══════════════════════════════════════════════════════════════════════════════
1. CISC (COMPLEX INSTRUCTION SET COMPUTER)
═══════════════════════════════════════════════════════════════════════════════


CORE IDEA
─────────
Provide many powerful instructions so a programmer can perform complex tasks 
with fewer instructions. One complex instruction performs multiple operations.

EXAMPLE
──────
Given:
    X = Memory[2:2]
    Y = Memory[3:3]
    K = X × Y

CISC Approach (Single Instruction):
    MULT 2:2, 3:3

This single instruction:
    • Reads X from memory
    • Reads Y from memory
    • Multiplies them
    • Stores result

The CPU does lots of work in one instruction.


CHARACTERISTICS OF CISC
───────────────────────

1. Large Number of Instructions
   • May have hundreds of instructions
   
   Examples: ADD, SUB, MUL, DIV, MOV, PUSH, POP, and many more

2. Variable-Length Instructions
   • Different instructions have different sizes
   
   Example:
       MOV A,B              → 2 bytes
       MOV AX,[5000H]       → 4 bytes

3. Many Addressing Modes
   • Immediate       • Direct       • Indirect
   • Indexed         • Relative

4. Multiple Cycle Instructions
   • One instruction may take several clock cycles
   
   Example - MUL operation requires:
       • Fetch          • Decode         • Read operands
       • Multiply       • Store

5. Direct Memory Manipulation
   • CPU can directly use memory operands
   
   Example: ADD [500], [600]

6. Microprogrammed Control Unit
   • Uses microcode stored internally


ADVANTAGES vs DISADVANTAGES
───────────────────────────
✓ Advantages:
    • Easier to design
    • Fewer instructions needed per program

✗ Disadvantages:
    • Slower execution
    • Complex hardware design
    • More power consumption


EXAMPLES OF CISC PROCESSORS
───────────────────────────
    • Intel x86
    • Motorola 68000


═══════════════════════════════════════════════════════════════════════════════
2. RISC (REDUCED INSTRUCTION SET COMPUTER)
═══════════════════════════════════════════════════════════════════════════════


CORE IDEA
─────────
Keep instructions simple and execute them very quickly. Instead of one complex 
instruction, use several simple instructions.

EXAMPLE
──────
Given:
    K = X × Y

RISC Approach (Multiple Simple Instructions):
    LOAD A, 2:2
    LOAD B, 3:3
    MUL A, B
    STORE K, A

More instructions are needed, but each instruction is very simple and fast.


CHARACTERISTICS OF RISC
───────────────────────

1. Fewer Instructions
   • Only essential instructions are provided
   • Simplified instruction set

2. Fixed-Length Instructions
   • Every instruction has the same size (e.g., 32 bits each)
   
   Benefits:
       • Faster decoding
       • Simpler hardware

3. Few Addressing Modes
   Usually only:
   • Register           • Immediate           • Base+Offset

4. Single-Cycle Execution
   • Most instructions complete in one clock cycle
   • Increases overall speed and throughput

5. Register-Based Operations
   RISC follows the pattern:
       Memory → Register → Register → Memory
   
   Arithmetic is done only on registers
   
   Example:
       LOAD R1, X
       LOAD R2, Y
       ADD R1, R2
   
   NOT: ADD X, Y

6. Hardwired Control Unit
   • Control signals are generated directly by hardware
   
   Advantages:
       • Faster execution
       • More efficient design


ADVANTAGES vs DISADVANTAGES
───────────────────────────
✓ Advantages:
    • Faster execution
    • Better pipelining capability
    • Lower power consumption
    • Simpler hardware

✗ Disadvantages:
    • More instructions per program
    • Larger program size


EXAMPLES OF RISC PROCESSORS
───────────────────────────
    • ARM (used in smartphones)
    • MIPS
    • SPARC


MEMORY OPERATION DIAGRAM
────────────────────────

Memory Location:
    • X at location 2:2
    • Y at location 3:3

Operation Flow:
    Memory → Registers (RA, RB) → Execution Unit → Result
    
    RA × RB = Result


═══════════════════════════════════════════════════════════════════════════════
3. WHY MODERN CPUs PREFER RISC CONCEPTS
═══════════════════════════════════════════════════════════════════════════════



RISC offers several key advantages:
    ✓ Faster execution          ✓ Better pipelining
    ✓ Lower power consumption   ✓ Simpler hardware

This is why most modern devices use ARM processors (smartphones, tablets, etc.).


═══════════════════════════════════════════════════════════════════════════════
4. EASY MEMORY TRICK
═══════════════════════════════════════════════════════════════════════════════

CISC
────
C = Complex
    • Few instructions written
    • More work per instruction
    • Example: MULT X,Y

RISC
────
R = Reduced
    • More instructions written
    • Less work per instruction
    • Example:
        LOAD X
        LOAD Y
        MUL
        STORE


═══════════════════════════════════════════════════════════════════════════════
5. EXAM SUMMARY
═══════════════════════════════════════════════════════════════════════════════

CISC Architecture
─────────────────
    • Complex instructions
    • Large instruction set
    • Variable instruction length
    • Many addressing modes
    • Multi-cycle execution
    • Microprogrammed control unit
    • Example: Intel x86

RISC Architecture
─────────────────
    • Simple instructions
    • Small instruction set
    • Fixed instruction length
    • Few addressing modes
    • Single-cycle execution
    • Hardwired control unit
    • Examples: ARM, MIPS, SPARC


═══════════════════════════════════════════════════════════════════════════════
6. KEY TAKEAWAY
═══════════════════════════════════════════════════════════════════════════════

"CISC reduces the number of instructions per program,
while RISC reduces the complexity of each instruction."

═══════════════════════════════════════════════════════════════════════════════