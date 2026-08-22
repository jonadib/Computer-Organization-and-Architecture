# What is an Instruction?

An **instruction** is a binary command given to the CPU telling it **what operation to perform**.

For example:

```text
ADD R1, R2
```

means:

> Add the contents of R1 and R2.

An instruction generally contains:

```text
┌───────────────┬────────────────────┐
│    Opcode     │      Operand       │
└───────────────┴────────────────────┘
```

### Opcode

**Opcode = Operation code**

It tells the CPU **what to do**.

Examples:

* ADD
* SUB
* LOAD
* STORE
* AND
* OR
* JUMP

### Operand

An operand tells the CPU **what data or location to operate on**.

Example:

```text
ADD R1, R2
    ↑     ↑
 Operand  Operand
```

---

# What is an Instruction Cycle?

The **instruction cycle** is the complete process used by the CPU to:

> **Fetch → Decode → Execute an instruction.**

The basic cycle is:

```text
        ┌───────────────┐
        │     FETCH     │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │     DECODE    │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │    EXECUTE    │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │   INTERRUPT   │
        │    CHECK      │
        └───────┬───────┘
                │
                ↓
             FETCH
```

The first three are the essential stages. An **interrupt check** may follow execution before the next fetch.

---

# 1. Main Stages of Instruction Cycle

There are usually four conceptual stages:

1. **Fetch**
2. **Decode**
3. **Execute**
4. **Interrupt check**

---

# 2. Fetch Cycle

The CPU first needs to get the instruction from memory.

The **Program Counter (PC)** contains the address of the next instruction.

Suppose:

```text
PC = 1000
```

and memory location 1000 contains:

```text
ADD R1, R2
```

### Step 1

The address from PC is transferred to MAR.

```text
PC → MAR
```

So:

```text
MAR = 1000
```

### Step 2

The CPU sends the address to memory.

```text
MAR → Memory
```

### Step 3

Memory returns the instruction.

```text
Memory → MBR/MDR
```

### Step 4

The instruction is transferred to IR.

```text
MBR → IR
```

### Step 5

PC is updated to point to the next instruction.

```text
PC ← PC + 1
```

## Fetch Diagram

```text
             CPU
      ┌─────────────────┐
      │                 │
      │       PC        │
      │        │        │
      │        ↓        │
      │       MAR ──────────────┐
      │                         │
      │       MBR/MDR ←─────────┤
      │          │              │
      │          ↓              │
      │         IR              │
      │                         │
      └─────────────────────────┘
                 ↕
        ┌─────────────────┐
        │      Memory     │
        │                 │
        │ 1000: ADD R1,R2 │
        └─────────────────┘
```

---

# 3. Decode Cycle

Now the instruction is inside the **Instruction Register (IR)**.

The Control Unit examines the instruction.

For example:

```text
ADD R1, R2
```

The Control Unit determines:

* Operation = ADD
* Source operands = R1 and R2
* Destination = according to instruction format

The decoder generates appropriate **control signals**.

```text
              IR
              │
              ↓
       ┌─────────────┐
       │ Instruction │
       │   Decoder   │
       └──────┬──────┘
              │
       Control Signals
       ┌──────┼───────┐
       ↓      ↓       ↓
      ALU   Registers Memory
```

---

# 4. Execute Cycle

Now the CPU actually performs the operation.

Suppose:

```text
R1 = 10
R2 = 20
```

Instruction:

```text
ADD R1, R2
```

The ALU performs:

```text
10 + 20 = 30
```

The result is stored in the appropriate destination register.

For example:

```text
R1 ← R1 + R2
```

Therefore:

```text
R1 = 30
```

---

# 5. Interrupt Check

After execution, the CPU checks whether an interrupt is waiting.

An **interrupt** is a signal requesting the CPU's attention.

For example:

* Keyboard input
* Timer
* I/O device
* Network device

If there is no interrupt:

```text
→ Fetch next instruction
```

If there is an interrupt:

```text
→ Save current context
→ Execute Interrupt Service Routine (ISR)
→ Return to previous program
```

---

# 6. Complete Instruction Cycle

```text
                     ┌─────────────┐
                     │    START    │
                     └──────┬──────┘
                            ↓
                     ┌─────────────┐
                     │    FETCH    │
                     │             │
                     │ PC → MAR    │
                     │ Memory → IR │
                     │ PC = PC + 1 │
                     └──────┬──────┘
                            ↓
                     ┌─────────────┐
                     │    DECODE   │
                     │             │
                     │ Identify    │
                     │ opcode &    │
                     │ operands    │
                     └──────┬──────┘
                            ↓
                     ┌─────────────┐
                     │   EXECUTE   │
                     │             │
                     │ ALU / Memory│
                     │ / Register  │
                     └──────┬──────┘
                            ↓
                     ┌─────────────┐
                     │  INTERRUPT? │
                     └──────┬──────┘
                       Yes ↙   ↘ No
                    ┌──────┐    │
                    │ ISR  │    │
                    └──┬───┘    │
                       └────┬───┘
                            ↓
                     FETCH NEXT
                     INSTRUCTION
```

---

# 7. Example of Complete Instruction Cycle

Consider:

```text
ADD R1, R2
```

Suppose:

```text
R1 = 10
R2 = 15
PC = 100
```

Memory:

```text
Address       Instruction
-------------------------
100           ADD R1,R2
101           SUB R3,R4
```

### Fetch

```text
PC = 100

PC → MAR
MAR → Memory
Memory → MBR
MBR → IR
PC = 101
```

Now:

```text
IR = ADD R1,R2
```

### Decode

Control Unit recognizes:

```text
Opcode = ADD
Operands = R1, R2
```

### Execute

```text
R1 = 10
R2 = 15
```

ALU:

```text
10 + 15 = 25
```

Result:

```text
R1 = 25
```

Then CPU goes back to:

```text
FETCH instruction at address 101
```

---

# 🧠 Super Easy Memory Trick

**Instruction = What the CPU should do**

**Opcode = What operation to perform**

**Operand = What data to use**

**Fetch = Get the instruction**

**Decode = Understand the instruction**

**Execute = Perform the operation**

**Interrupt Check = Check if something needs CPU attention**

### Main Cycle

> **FETCH → DECODE → EXECUTE → INTERRUPT CHECK → FETCH**
