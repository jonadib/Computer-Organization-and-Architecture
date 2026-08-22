# Instruction-Level Pipelining

## 1. What is Instruction-Level Pipelining?

Instruction-level pipelining is a technique where the CPU overlaps the execution of multiple instructions.

Think of it like a factory assembly line.

**Without pipelining** — only one instruction is processed at a time:

```
Instruction 1 → Complete
Instruction 2 → Complete
Instruction 3 → Complete
```

**With pipelining** — different stages of different instructions run at the same time:

| Instruction | Cycle 1 | Cycle 2 | Cycle 3 | Cycle 4 | Cycle 5 |
|---|---|---|---|---|---|
| Instruction 1 | FI | DI | CO | FO | EI |
| Instruction 2 |    | FI | DI | CO | FO |
| Instruction 3 |    |    | FI | DI | CO |
| Instruction 4 |    |    |    | FI | DI |

**Main idea:** Different stages of different instructions work at the same time.

---

## 2. Six Stages of the Instruction Pipeline

A common 6-stage pipeline:

```
FI → DI → CO → FO → EI → WO
```

### ① FI — Fetch Instruction
The CPU gets the instruction from memory/cache.

> Example: `ADD R1, R2` — the CPU first fetches this instruction.

**Easy meaning:** FI = Get the instruction

### ② DI — Decode Instruction
The CPU determines:
- What operation is required?
- Which registers are involved?
- What operands are needed?

> For `ADD R1, R2`, the CPU understands: "I need to add the contents of R1 and R2."

**Easy meaning:** DI = Understand the instruction

### ③ CO — Calculate Operands
The CPU calculates the effective address of the required operand when necessary.

> Example: `LOAD R1, 20(R2)`, where R2 = 1000
> Effective Address = 1000 + 20 = 1020

**Easy meaning:** CO = Find/calculate where the operand is

### ④ FO — Fetch Operands
The CPU gets the required operands (from registers, or memory if needed).

> Example: `ADD R1, R2` — gets the values from the registers.

**Easy meaning:** FO = Get the data

### ⑤ EI — Execute Instruction
The actual operation is performed.

> Example: R1 = 10, R2 = 20 → 10 + 20 = 30

**Easy meaning:** EI = Do the operation

### ⑥ WO — Write Operand
The result is stored in the destination register or memory.

> Example: R1 = 30

**Easy meaning:** WO = Store the result

### ⭐ Easy Way to Remember the Six Stages

```
FI → DI → CO → FO → EI → WO
Fetch → Decode → Calculate → Fetch → Execute → Write
```

Or simply: **Get instruction → Understand → Find data → Get data → Calculate → Store**

---

## 3. Pipeline Diagram

Suppose we have four instructions: I1, I2, I3, I4.

**Without pipelining** (each instruction waits for the previous one to finish):

```
I1: FI → DI → CO → FO → EI → WO
I2:                         FI → DI → CO → FO → EI → WO
I3:                                                 FI → DI → CO → FO → EI → WO
```

**With pipelining:**

| Instr | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| I1 | FI | DI | CO | FO | EI | WO |   |   |   |
| I2 |    | FI | DI | CO | FO | EI | WO |   |   |
| I3 |    |    | FI | DI | CO | FO | EI | WO |   |
| I4 |    |    |    | FI | DI | CO | FO | EI | WO |

At **Cycle 4**: I1 → FO, I2 → CO, I3 → DI, I4 → FI

Four instructions are being processed simultaneously, but at different stages.

---

## 4. Pipeline Registers / Latches

Between two stages, we need temporary storage called a **pipeline register/latch**.

```
FI → [Pipeline Register] → DI → [Pipeline Register] → CO
   → [Pipeline Register] → FO → [Pipeline Register] → EI
   → [Pipeline Register] → WO
```

**Why are they needed?**
They hold the result of one stage while the next stage works. Pipeline registers keep the stages synchronized.

---

## 5. Pipeline Performance

Three important performance terms:
- Cycle Time
- Throughput
- Speedup

---

## 6. Cycle Time

The cycle time is the time required for one pipeline stage to complete its work and pass the result to the next stage. It depends on the slowest stage.

**Formula:**

$$\tau = \tau_m + d$$

Where:
- τₘ = maximum/slowest stage delay
- d = pipeline register/latch delay

**Example**

| Stage | Delay |
|---|---|
| Stage 1 | 800 ns |
| Stage 2 | 500 ns |
| Stage 3 | 400 ns |
| Stage 4 | 300 ns |

The slowest stage: τₘ = 800 ns

Ignoring latch delay: **τ = 800 ns**

> **Important:** The slowest stage determines the pipeline speed.

---

## 7. Throughput

**Definition:** How many instructions can be completed per unit of time.

$$\text{Throughput} \approx \frac{1}{\tau}$$

If τ = 800 ns:

$$\text{Throughput} = \frac{1}{800 \times 10^{-9}} = 1.25 \times 10^{6}$$

**Throughput = 1.25 MIPS** (assuming one instruction completes every cycle after the pipeline is full)

---

## 8. Bottleneck

The slowest stage is called the **bottleneck**.

| Stage | Delay | Note |
|---|---|---|
| Stage 1 | 800 ns | ← Bottleneck |
| Stage 2 | 500 ns | |
| Stage 3 | 400 ns | |
| Stage 4 | 300 ns | |

If we improve Stage 1 from 800 ns to 600 ns, the new bottleneck becomes **600 ns**, and the pipeline becomes faster.

---

## 9. Throughput Improvement Example

- Original bottleneck: 800 ns → throughput = 1/800
- New bottleneck: 600 ns → throughput = 1/600

**Percentage increase:**

$$\left(\frac{\frac{1}{600} - \frac{1}{800}}{\frac{1}{800}}\right) \times 100 = \left(\frac{800}{600} - 1\right) \times 100 = 33.33\%$$

**Answer: 33.33% increase**

---

## 10. Speedup

Speedup tells us how much faster the pipelined processor is compared with a non-pipelined processor.

Let:
- k = number of stages
- n = number of instructions
- τ = pipeline cycle time

**Without pipeline** — each instruction passes through all k stages:

$$T_{non\text{-}pipeline} = n \times k \times \tau$$

**With pipeline** — first instruction takes k cycles, then one instruction finishes every cycle:

$$T_{pipeline} = (k + n - 1)\tau$$

**Speedup:**

$$S_k = \frac{T_{non\text{-}pipeline}}{T_{pipeline}} = \frac{nk}{k+n-1}$$

---

## 11. Speedup Example

Suppose k = 6 and n = 100.

- Without pipeline: T = 100 × 6τ = 600τ
- With pipeline: T = (6 + 100 − 1)τ = 105τ

**Speedup:**

$$S = \frac{600}{105} \approx 5.71$$

So the pipeline is approximately **5.71 times faster**.

---

## 12. Maximum Theoretical Speedup

As the number of instructions becomes very large (n → ∞):

$$S_k \rightarrow k$$

For a 6-stage pipeline: **Maximum theoretical speedup ≈ 6**

But in real computers, we usually don't get exactly 6× because of pipeline hazards and other overheads.

---

## 13. Pipeline Hazards

A **pipeline hazard** is a problem that prevents the next instruction from executing in the desired pipeline stage. When a hazard occurs, the pipeline may have to wait/stall, creating a **pipeline bubble** (an empty cycle).

```
Normal:  I1 → I2 → I3 → I4
Hazard:  I1 → I2 → WAIT → I3 → I4
                     ↑
                  Bubble
```

There are three major types: **Structural**, **Data**, and **Control** hazards.

---

## 14. Structural Hazard

**Definition:** Occurs when two instructions need the same hardware resource at the same time.

> Example: Suppose there is only one memory. At the same time, I1 fetches an instruction from memory while I2 writes data to memory. The CPU cannot perform both simultaneously, so one instruction must wait.

**Easy meaning:** Structural hazard = Hardware/resource conflict

---

## 15. Data Hazard

**Definition:** Occurs when one instruction depends on data involved in another instruction.

```
I1: ADD R1, R2
I2: SUB R3, R1
```

I2 needs the new value of R1 produced by I1, but I1 may not have written it yet — so I2 may have to wait.

---

## 16. Three Types of Data Hazards

### ① RAW — Read After Write (true dependency)
Instruction 2 wants to read a value before Instruction 1 has written it.

```
I1: WRITE R1
I2: READ  R1
```
**Easy:** Read before previous Write is finished. This is the most common data hazard.

### ② WAR — Write After Read (anti-dependency)
Instruction 2 wants to write before Instruction 1 has finished reading.

```
I1: READ R1
I2: WRITE R1
```
**Easy:** Write too early

### ③ WAW — Write After Write (output dependency)
Two instructions write to the same location.

```
I1: WRITE R1
I2: WRITE R1
```
If they execute out of order, the final value may be incorrect.

**Easy:** Two writes to the same place

### ⭐ Easy Memory Trick

```
RAW → Read before Write   → True dependency
WAR → Write before Read   → Anti-dependency
WAW → Write before Write  → Output dependency
```

---

## 17. Control Hazard (Branch Hazard)

Occurs when the CPU encounters a branch or jump instruction.

```
I1: ADD
I2: SUB
I3: BEQ LABEL
I4: ?
```

The CPU doesn't immediately know whether the branch will be taken. If the branch is taken, instructions already fetched (I4, I5, I6...) may be wrong and must be **discarded/flushed**, then fetching resumes from LABEL.

**Easy meaning:** Control hazard = Problem caused by branch/jump

---

## 18. Pipeline Bubble

When the pipeline cannot proceed, it inserts an empty cycle.

| Instr | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| I1 | FI | DI | CO | FO | EI | WO |
| I2 |    | FI | DI | -- | FO | EI |
| I3 |    |    | FI | -- | DI | CO |

The `--` represents a stall/bubble.

**Result:** The actual speedup becomes less than the theoretical speedup.

---

## 19. Why Can't We Make Infinite Pipeline Stages?

More stages can potentially increase clock speed, but there are practical limits. Every stage requires:
- Pipeline registers
- Control logic
- Synchronization
- Hazard handling

Each register introduces latching delay, so more pipeline stages **does not** mean unlimited performance. Eventually the overhead becomes significant.

---

## 20. Complete Pipeline Picture

```
Instruction
    │
    ▼
┌─────────┐
│   FI    │  Fetch Instruction
└────┬────┘
     ▼
┌─────────┐
│   DI    │  Decode Instruction
└────┬────┘
     ▼
┌─────────┐
│   CO    │  Calculate Operands
└────┬────┘
     ▼
┌─────────┐
│   FO    │  Fetch Operands
└────┬────┘
     ▼
┌─────────┐
│   EI    │  Execute
└────┬────┘
     ▼
┌─────────┐
│   WO    │  Write Operand
└─────────┘
```

Multiple instructions occupy these stages simultaneously:

| Instr | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| I1 | FI | DI | CO | FO | EI | WO |   |   |
| I2 |    | FI | DI | CO | FO | EI | WO |   |
| I3 |    |    | FI | DI | CO | FO | EI | WO |
| I4 |    |    |    | FI | DI | CO | FO | EI |

---

## 🎯 Exam Revision Sheet

**Definition:** Instruction-level pipelining is a technique in which the execution of multiple instructions is overlapped by dividing instruction execution into several stages.

| Concept | Formula / Value |
|---|---|
| Six stages | FI → DI → CO → FO → EI → WO |
| Cycle time | τ = τₘ + d |
| Throughput | Throughput ≈ 1/τ |
| Non-pipelined time | T_non = nkτ |
| Pipelined time | T_pipe = (k + n − 1)τ |
| Speedup | S = nk / (k + n − 1) |
| Maximum speedup | S → k |

**Three hazards:**

| Hazard | Meaning | Easy memory |
|---|---|---|
| Structural | Hardware resource conflict | Same hardware |
| Data | Data dependency | Need previous data |
| Control | Branch/jump problem | Don't know next instruction |

**Data hazards:** RAW, WAR, WAW
- RAW = Read After Write (true dependency)
- WAR = Write After Read (anti-dependency)
- WAW = Write After Write (output dependency)

**Most important exam sentence:**

> Pipelining improves instruction throughput by allowing different stages of multiple instructions to operate simultaneously, but hazards, stalls, branch penalties, and pipeline-register overhead prevent achieving the theoretical maximum speedup.