# DMA Controller (Direct Memory Access Controller) — Complete Notes

## Table of Contents

1. [DMA — Basics and Functions](#dma--basics-and-functions)
2. [DMA — Transfer Process and Handshaking Signals](#dma--transfer-process-and-handshaking-signals)
3. [DMA — Transfer Modes](#dma--transfer-modes)
4. [DMA vs Other I/O Methods](#dma-vs-other-io-methods)
5. [DMA — State Machine and One-Hot Design](#dma--state-machine-and-one-hot-design)
6. [DMA — Timing and Numerical Example](#dma--timing-and-numerical-example)
7. [DMA — Exam Revision Sheet](#dma--exam-revision-sheet)

---

## DMA — Basics and Functions

### 1. What is DMA?

**DMA (Direct Memory Access)** is a technique that allows an I/O device to transfer data **directly to or from main memory without the CPU handling every byte/word of the transfer**.

A **DMA Controller (DMAC)** is the hardware unit that manages this transfer.

#### Simple idea

**Normally:**

```
I/O Device → CPU → Main Memory
```

**With DMA:**

```
I/O Device ─────────→ Main Memory
                 ↑
            DMA Controller
```

The CPU only initializes the DMA operation. After that, the DMA controller manages the actual data transfer.

---

### 2. Why is DMA Needed?

Suppose a disk needs to transfer 10,000 bytes to memory.

#### Without DMA

The CPU may have to handle every byte:

```
Read byte from I/O
       ↓
CPU register
       ↓
Write byte to memory
       ↓
Repeat 10,000 times
```

This consumes a large number of CPU cycles.

#### With DMA

The CPU tells the DMA controller:

```
Starting memory address = 5000
Transfer size = 10,000 bytes
Direction = I/O → Memory
```

Then the DMA controller performs the transfer:

```
I/O Device ─────────────→ Memory
             DMA
```

The CPU is free to perform other work, except when it temporarily loses control of the bus.

---

### 3. Definition of DMA Controller

#### Exam Definition

> A Direct Memory Access Controller (DMAC) is a hardware device that controls the direct transfer of data between an I/O device and main memory without requiring the CPU to handle each individual data transfer.

#### Short Definition

> DMA allows I/O devices to transfer data directly to or from main memory with minimum CPU intervention.

---

### 4. Basic DMA System

The three main components involved, alongside memory, are:

- CPU
- DMA Controller
- I/O Device
- Main Memory

A simplified organization:

```
                    SYSTEM BUS
        ┌─────────────────────────────────┐
        │ Address Bus                     │
        │ Data Bus                        │
        │ Control Bus                     │
        └─────────────────────────────────┘
             ↑          ↑          ↑
             │          │          │
        ┌────┴───┐  ┌───┴────┐  ┌──┴────────┐
        │  CPU   │  │  DMA   │  │   Main    │
        │        │  │Controller│ │  Memory   │
        └────────┘  └───┬────┘  └───────────┘
                         │
                         │
                    ┌────┴─────┐
                    │ I/O Device│
                    └──────────┘
```

The DMA controller becomes the **bus master** during the actual DMA transfer.

---

### 5. Main Functions of DMA Controller

A DMA controller performs several important functions.

#### 5.1 Store Starting Address

The DMA controller stores the starting memory address in an **Address Register**.

```
Starting address = 5000
Address Register = 5000
```

After each transfer, it increments automatically:

```
5000 → 5001 → 5002 → 5003 → ...
```

#### 5.2 Store Transfer Count

The DMA controller needs to know how much data must be transferred. This is stored in the **Data Count Register**.

```
Transfer size = 1000 bytes
Data Count Register = 1000
```

After each transfer:

```
1000 → 999 → 998 → 997 → ...
```

When the count becomes zero, the DMA operation is complete.

#### 5.3 Control the Direction of Transfer

DMA must know the direction of data movement.

**I/O → Memory** (I/O Device → Memory): the DMA controller performs `IOR + MEMW`

```
IOR  = I/O Read
MEMW = Memory Write
```

**Memory → I/O** (Memory → I/O Device): the DMA controller performs `MEMR + IOW`

```
MEMR = Memory Read
IOW  = I/O Write
```

#### 5.4 Request the System Bus

Since the CPU normally controls the system bus, the DMA controller must request it. It sends `HRQ / HOLD` to the CPU. The CPU then temporarily releases the bus.

#### 5.5 Receive Bus Acknowledgment

The CPU responds with `HLDA` (Hold Acknowledge). This tells the DMA controller that it can use the bus.

#### 5.6 Generate Control Signals

The DMA controller generates signals such as `MEMR`, `MEMW`, `IOR`, `IOW` to control the actual data transfer.

#### 5.7 Update Address and Count

After each transfer:

```
Address Register = Address Register + 1
Count Register    = Count Register - 1
```

For word transfers, the address may increase by the word size rather than by 1.

#### 5.8 Generate Interrupt

When the entire block has been transferred (`Count = 0`), the DMA controller can generate an **Interrupt Request** to notify the CPU.

---

### 6. Important DMA Registers

| Register | Purpose |
|---|---|
| Address Register | Stores the memory address |
| Data Count Register | Stores number of bytes/words remaining |
| Control Register | Stores transfer mode/direction information |
| Status Register | Stores DMA status |
| Data Register | May temporarily hold data in some DMA architectures |

---

## DMA — Transfer Process and Handshaking Signals

### 1. DMA Transfer Process

The complete DMA operation can be divided into several steps.

#### Step 1: CPU Initializes DMA

The CPU provides:

```
Starting address
Transfer count
Transfer direction
DMA mode
```

Example:

```
Address = 5000
Count = 1000
Direction = I/O → Memory
```

#### Step 2: I/O Device Requests DMA

When the I/O device is ready, it sends **DREQ** (DMA Request):

> "DMA controller, I need a DMA transfer."

#### Step 3: DMA Requests Bus

The DMA controller sends **HRQ / HOLD** to the CPU:

> "CPU, please release the system bus."

#### Step 4: CPU Releases Bus

The CPU finishes its current bus operation and releases the bus. It sends **HLDA** (Hold Acknowledge):

> "DMA controller, you may use the bus."

#### Step 5: DMA Acknowledges I/O Device

The DMA controller sends **DACK** (DMA Acknowledge) to the requesting I/O device:

> "Your DMA request has been accepted."

#### Step 6: Data Transfer

The DMA controller places the required memory address on the address bus.

**For I/O → Memory:** `I/O Device → Data Bus → Memory`, using control signals `IOR + MEMW`

**For Memory → I/O:** `Memory → Data Bus → I/O Device`, using control signals `MEMR + IOW`

#### Step 7: Update Registers

After one transfer:

```
Address = Address + 1
Count   = Count - 1
```

#### Step 8: Check Count

- If `Count > 0` → another transfer occurs.
- If `Count = 0` → the DMA operation is finished.

#### Step 9: Release Bus

DMA deasserts `HRQ`. The CPU can regain control of the system bus.

#### Step 10: Interrupt CPU

The DMA controller may generate `INT` to tell the CPU:

> "The DMA transfer is complete."

---

### 2. DMA Handshaking Signals

| Signal | Meaning | Direction |
|---|---|---|
| DREQ | DMA Request | I/O → DMA |
| DACK | DMA Acknowledge | DMA → I/O |
| HRQ/HOLD | Hold Request | DMA → CPU |
| HLDA | Hold Acknowledge | CPU → DMA |
| MEMR | Memory Read | DMA → Memory |
| MEMW | Memory Write | DMA → Memory |
| IOR | I/O Read | DMA → I/O |
| IOW | I/O Write | DMA → I/O |
| INT | Interrupt | DMA → CPU |

---

### 3. DMA Block Diagram

```
                         SYSTEM BUS
       ┌──────────────────────────────────────────────┐
       │                                              │
       │ Address Bus                                  │
       │ Data Bus                                     │
       │ Control Bus                                  │
       │                                              │
       └──────────────────────────────────────────────┘
             ↑              ↑                 ↑
             │              │                 │
       ┌─────┴─────┐  ┌─────┴────────┐  ┌────┴───────┐
       │    CPU    │  │     DMA      │  │   MAIN     │
       │           │  │  Controller  │  │   MEMORY   │
       └───────────┘  └──────┬───────┘  └────────────┘
                              │
                              │ DREQ / DACK
                              │
                       ┌──────┴──────┐
                       │ I/O DEVICE  │
                       └─────────────┘
```

---

### 4. Internal Structure of DMA Controller

A simplified DMA controller contains:

```
                 DMA CONTROLLER
        ┌─────────────────────────────┐
        │                             │
        │    Address Register         │
        │                             │
        │    Data Count Register     │
        │                             │
        │    Control Register        │
        │                             │
        │    Status Register         │
        │                             │
        │    Control Logic           │
        │                             │
        │    Bus Control Logic        │
        │                             │
        └─────────────────────────────┘
```

- **Address Register** — Stores the memory address.
- **Count Register** — Stores the number of remaining transfers.
- **Control Register** — Stores transfer direction, DMA mode, channel information.
- **Status Register** — Indicates DMA active, DMA completed, terminal count, errors.
- **Control Logic** — Controls the entire DMA operation.

---

### 5. DMA Timing Sequence

For an I/O → Memory transfer:

```
       T1       T2       T3       T4
       │        │        │        │
       ↓        ↓        ↓        ↓


DREQ   ────────┐
               └──────────────────


HRQ    ─────────────┐
                    └─────────────


HLDA             ───┐
                    └─────────────


DACK               ─┐
                     └────────────


IOR                 ────────┐
                             └────


MEMW                ────────┐
                             └────


DATA                [ DATA TRANSFER ]
```

The exact timing depends on the particular DMA controller and system architecture.

---

### 6. Worked Example — Full Transfer Sequence

Suppose:

```
Starting address = 1000
Transfer count   = 4
Direction        = I/O → Memory
```

Initially: `Address Register = 1000`, `Count Register = 4`

| Step | Operation | Address after | Count after |
|---|---|---|---|
| Transfer 1 | I/O → Memory[1000] | 1001 | 3 |
| Transfer 2 | I/O → Memory[1001] | 1002 | 2 |
| Transfer 3 | I/O → Memory[1002] | 1003 | 1 |
| Transfer 4 | I/O → Memory[1003] | 1004 | 0 |

Now `Count = 0` → **Terminal Count = 1** → DMA completes the operation.

---

### 7. DMA and Bus Arbitration

DMA needs the system bus to communicate with memory and I/O devices — but the CPU also needs the bus. Therefore, **bus arbitration** is required to determine who controls the bus.

Typical sequence:

```
CPU owns bus
     ↓
DMA requests bus
     ↓
CPU releases bus
     ↓
DMA owns bus
     ↓
DMA transfers data
     ↓
DMA releases bus
     ↓
CPU gets bus again
```

### 8. DMA and Tri-State Logic

When DMA takes control of the bus, the CPU must stop driving the bus. The CPU's bus outputs enter **High-Z** (high-impedance) state.

```
CPU → High-Z
DMA → Drives bus
```

This prevents two devices from driving the same bus simultaneously.

---

## DMA — Transfer Modes

There are several DMA transfer modes.

### 1. Burst Mode

In burst mode, the DMA controller takes control of the bus and transfers an entire block continuously.

```
CPU
 ↓
DMA gets bus
 ↓
Transfer block
 ↓
DMA releases bus
 ↓
CPU gets bus
```

**Example:**

```
1000 bytes
↓
DMA transfers all 1000 bytes continuously
```

**Advantage:** Very fast block transfer.

**Disadvantage:** CPU may have to wait for the entire DMA block.

---

### 2. Cycle Stealing Mode

In cycle stealing, DMA takes the bus for **one transfer at a time**.

```
CPU → DMA → CPU → DMA → CPU → DMA
```

The DMA controller "steals" individual bus cycles from the CPU.

**Advantage:** CPU is not completely blocked.

**Disadvantage:** CPU execution becomes slower because some bus cycles are taken by DMA.

---

### 3. Transparent DMA

In transparent DMA, the DMA controller transfers data **only when the CPU is not using the system bus**.

```
CPU using bus
      ↓
DMA waits


CPU not using bus
      ↓
DMA transfers
```

**Advantage:** Very little interference with CPU.

**Disadvantage:** Transfer may be slow because DMA has to wait for free bus cycles.

---

### 4. Burst vs Cycle Stealing vs Transparent

| Feature | Burst | Cycle Stealing | Transparent |
|---|---|---|---|
| Bus usage | Continuous | One cycle at a time | Only when CPU doesn't need bus |
| CPU interruption | High | Moderate | Very low |
| DMA speed | Very high | Moderate | Low |
| CPU performance | Reduced during burst | Slightly reduced | Almost unaffected |

---

### 5. Fly-By DMA

In a fly-by DMA transfer, the DMA controller does **not** necessarily store the transferred data in an internal data register.

Instead:

```
I/O → Bus → Memory
```

or:

```
Memory → Bus → I/O
```

The DMA controller mainly controls: address, control signals, timing, and count.

**Example:**

```
I/O Device
     │
     │ Data
     ↓
Data Bus ─────────────→ Memory
     ↑
     │
 DMA Controller
(control only)
```

This is called **fly-by** because data effectively flies directly between the I/O device and memory, without stopping inside the DMA controller.

---

### ⭐ Exam Definitions

**Cycle Stealing**
> A DMA technique in which the DMA controller temporarily takes individual bus cycles from the CPU to transfer data.

**Burst Mode**
> A DMA technique in which the DMA controller retains control of the bus and transfers an entire block of data continuously.

**Fly-By DMA**
> A DMA technique in which data is transferred directly between an I/O device and memory through the system bus, while the DMA controller mainly provides address, control, and timing signals.

---

## DMA vs Other I/O Methods

### 1. DMA vs Programmed I/O

#### Programmed I/O

CPU handles the transfer directly:

```
I/O → CPU → Memory
```

The CPU must repeatedly check and transfer data.

#### DMA

DMA controller handles the transfer:

```
I/O ─────────→ Memory
       DMA
```

The CPU only initializes the transfer and receives a completion notification.

#### Comparison

| Feature | Programmed I/O | DMA |
|---|---|---|
| CPU involvement | Very high | Low |
| Transfer speed | Lower | Higher |
| CPU cycles | Many | Few |
| Hardware complexity | Low | Higher |
| Suitable for | Small/simple transfers | Large/high-speed transfers |

---

### 2. DMA vs Interrupt-Driven I/O

#### Interrupt-Driven I/O

The device interrupts the CPU:

```
I/O → Interrupt → CPU
             ↓
         Transfer data
```

The CPU still participates in transferring the data itself — it's just notified rather than polling.

#### DMA

```
I/O ─────────→ Memory
       DMA
```

The CPU is mostly removed from the data-transfer path entirely.

> **Therefore:** DMA is more suitable for high-speed and block-oriented data transfers.

---

### 3. Important Concept — DMA and CPU Are Not Completely Independent

A common misconception is:

> "DMA completely removes the CPU from the transfer."

This is **not exactly correct**. The CPU still:

1. Initializes the DMA controller.
2. Gives the starting address.
3. Gives the transfer count.
4. Specifies the transfer direction/mode.
5. May receive an interrupt when the transfer finishes.

The CPU is mainly removed from the **individual data-transfer operations**, not from the process as a whole.

---

## DMA — State Machine and One-Hot Design

### 1. DMA State Machine

A DMA controller can be designed as a **finite state machine (FSM)**.

A simple design can contain:

```
S0 = IDLE
S1 = BUS REQUEST
S2 = BUS ACKNOWLEDGE
S3 = DATA TRANSFER
S4 = UPDATE
S5 = COMPLETE
```

---

### 2. DMA State Transition Diagram

```
                    DREQ = 0
                 ┌─────────────┐
                 │             │
                 ↓             │
              ┌──────┐         │
              │ S0   │─────────┘
              │ IDLE │
              └──┬───┘
                 │
             DREQ = 1
                 ↓
          ┌──────────────┐
          │ S1           │
          │ BUS REQUEST  │
          └──────┬───────┘
                 │
             HLDA = 1
                 ↓
          ┌──────────────┐
          │ S2           │
          │ DACK         │
          └──────┬───────┘
                 ↓
          ┌──────────────┐
          │ S3           │
          │ DATA TRANSFER│
          └──────┬───────┘
                 ↓
          ┌──────────────┐
          │ S4           │
          │ UPDATE       │
          └──────┬───────┘
                 │
          ┌──────┴─────────────┐
          │                    │
       Count > 0            Count = 0
          │                    │
          ↓                    ↓
     S3 / S0              ┌─────────┐
                          │ S5      │
                          │ COMPLETE│
                          └────┬────┘
                               │
                               ↓
                              S0
```

---

### 3. DMA State Transition Table

| Present State | Condition | Next State | Main Operation |
|---|---|---|---|
| S0 IDLE | DREQ = 0 | S0 | Wait |
| S0 IDLE | DREQ = 1 | S1 | Request bus |
| S1 BUS REQUEST | HLDA = 0 | S1 | Keep requesting |
| S1 BUS REQUEST | HLDA = 1 | S2 | Bus acquired |
| S2 DACK | — | S3 | Acknowledge I/O |
| S3 TRANSFER | — | S4 | Transfer data |
| S4 UPDATE | Count > 0 | S3 | Next transfer |
| S4 UPDATE | Count = 0 | S5 | Complete |
| S5 COMPLETE | — | S0 | Release bus / interrupt |

---

### 4. One-Hot DMA Controller Design

In the **One-Hot method**, each state has its own flip-flop.

Suppose there are six states:

```
S0 = IDLE
S1 = BUS REQUEST
S2 = DACK
S3 = TRANSFER
S4 = UPDATE
S5 = COMPLETE
```

Then six flip-flops are used: `Q0 Q1 Q2 Q3 Q4 Q5`. Only one is 1 at a time.

**Examples:**

```
IDLE:          Q0 Q1 Q2 Q3 Q4 Q5
                1  0  0  0  0  0

BUS REQUEST:    0  1  0  0  0  0

TRANSFER:       0  0  0  1  0  0

COMPLETE:       0  0  0  0  0  1
```

---

### 5. Why One-Hot is Useful for DMA

One-Hot encoding makes control logic simple. Instead of decoding a binary value like `0101` to determine the current state, the flip-flop itself identifies the state.

For example: `Q3 = 1` directly means **TRANSFER STATE**.

> One-Hot design simplifies state decoding and can provide fast control logic.

---

### 6. DMA Control Signals by Case

The control unit generates signals depending on the operation.

#### Case 1: I/O → Memory

Suppose a disk sends data to RAM.

```
Disk → Memory
```

Required signals: `IOR = 1`, `MEMW = 1`

```
IOR  → Read from I/O
MEMW → Write to Memory
```

```
Disk
 ↓
IOR
 ↓
Data Bus
 ↓
MEMW
 ↓
Memory
```

#### Case 2: Memory → I/O

Suppose memory sends data to a printer.

```
Memory → Printer
```

Required signals: `MEMR = 1`, `IOW = 1`

```
MEMR → Read from Memory
IOW  → Write to I/O
```

---

## DMA — Timing and Numerical Example

### 1. DMA Timing Calculation

DMA problems often give:

- Data transfer rate
- Transfer size
- CPU frequency
- CPU cycles for initialization
- CPU cycles for completion

The basic formulas are very important.

#### Formula 1: Transfer Time

If $R$ = data transfer rate and $D$ = amount of data:

$$T_{transfer} = \frac{D}{R}$$

#### Formula 2: CPU Clock Period

If CPU frequency is $f$:

$$T_{clock} = \frac{1}{f}$$

#### Formula 3: CPU Overhead Time

If the CPU uses $C$ clock cycles:

$$T_{overhead} = C \times T_{clock} = \frac{C}{f}$$

#### Formula 4: Total Time

$$T_{total} = T_{transfer} + T_{overhead}$$

#### Formula 5: CPU Overhead Percentage

$$\text{CPU overhead \%} = \frac{T_{overhead}}{T_{total}} \times 100$$

---

### 2. Numerical Example

#### Problem

A hard disk has a transfer rate of **10 MB/s**. A block of **10 KB** is transferred using DMA. The processor operates at **600 MHz**. The CPU requires **300 cycles** for initialization and **900 cycles** for completion.

**Find the percentage of total time consumed by CPU overhead.**

---

#### Step 1: Calculate Transfer Time

Given:
```
R = 10 MB/s
D = 10 KB
```

Using decimal units:
```
10 MB = 10 × 10^6 bytes
10 KB = 10 × 10^3 bytes
```

$$T_{transfer} = \frac{D}{R} = \frac{10 \times 10^3}{10 \times 10^6} = 10^{-3} \text{ s} = 1 \text{ ms}$$

#### Step 2: Calculate Total CPU Cycles

```
Initialization = 300 cycles
Completion     = 900 cycles

Total cycles = 300 + 900 = 1200 cycles
```

#### Step 3: Calculate CPU Clock Period

```
f = 600 MHz = 600 × 10^6 Hz
```

$$T_{clock} = \frac{1}{f} = \frac{1}{600 \times 10^6} \approx 1.667 \text{ ns}$$

#### Step 4: Calculate CPU Overhead

$$T_{overhead} = 1200 \times 1.667 \text{ ns} \approx 2000 \text{ ns} = 2 \, \mu s$$

#### Step 5: Calculate Total Time

```
Transfer time = 1 ms   = 1000 μs
CPU overhead  = 2 μs
```

$$T_{total} = 1000 + 2 = 1002 \, \mu s$$

#### Step 6: Calculate Percentage

$$\text{CPU overhead \%} = \frac{2}{1002} \times 100 \approx 0.20\%$$

#### ✅ Answer

**CPU overhead ≈ 0.20%**

This demonstrates one of the major advantages of DMA:

> A large amount of data can be transferred while consuming only a small percentage of CPU time.

---

## DMA — Exam Revision Sheet

### 1. Terminal Count (TC)

**Terminal Count** means the DMA controller has completed the requested number of transfers.

Example:

```
Count = 5

Transfer 1 → 4
Transfer 2 → 3
Transfer 3 → 2
Transfer 4 → 1
Transfer 5 → 0

TC = 1
```

When `Count = 0`, the DMA operation terminates.

---

### 2. Advantages of DMA

- Reduces CPU workload
- High-speed data transfer
- Efficient for block transfers
- Allows CPU and I/O operations to overlap
- Reduces number of CPU instructions required
- Useful for disks, network interfaces, audio/video devices, etc.

### 3. Disadvantages of DMA

- Requires additional hardware
- DMA and CPU compete for the system bus
- DMA may temporarily slow down the CPU
- Bus arbitration is required
- Hardware/control logic is more complex
- Cache coherence can become an issue in systems with caches, if DMA writes memory behind the CPU's cache

### 4. Advantages vs Disadvantages

| Advantages | Disadvantages |
|---|---|
| Low CPU involvement | Extra hardware |
| Fast block transfer | Bus contention |
| Efficient for large transfers | More complex design |
| Reduces CPU overhead | Can slow CPU during bus ownership |
| Direct I/O–memory transfer | Cache-coherence issues may arise |

---

### 5. Exam Definitions

**DMA**
> Direct Memory Access (DMA) is a technique in which data is transferred directly between an I/O device and main memory without requiring the CPU to handle each individual data transfer.

**DMA Controller**
> A DMA Controller is a hardware unit that manages direct data transfers between I/O devices and main memory by controlling the system bus.

**DREQ**
> DREQ (DMA Request) is a signal generated by an I/O device to request a DMA transfer.

**DACK**
> DACK (DMA Acknowledge) is a signal generated by the DMA controller to acknowledge an I/O device's DMA request.

**HOLD / HRQ**
> HOLD or HRQ is a signal generated by the DMA controller to request control of the system bus from the CPU.

**HLDA**
> HLDA (Hold Acknowledge) is a signal from the CPU indicating that it has released the system bus for the DMA controller.

**Terminal Count**
> The condition indicating that the DMA controller has completed the specified number of data transfers.

**Cycle Stealing**
> A DMA technique in which the DMA controller temporarily takes individual bus cycles from the CPU to transfer data.

**Burst Mode**
> A DMA technique in which the DMA controller retains control of the bus and transfers an entire block of data continuously.

**Fly-By DMA**
> A DMA technique in which data is transferred directly between an I/O device and memory through the system bus, while the DMA controller mainly provides address, control, and timing signals.

---

### 6. Very Important Exam Questions

#### Short Questions
- What is DMA?
- What is a DMA controller?
- Why is DMA required?
- What is DREQ?
- What is DACK?
- What is HOLD/HRQ?
- What is HLDA?
- What is Terminal Count?
- What is cycle stealing?
- What is burst mode?
- What is fly-by DMA?
- What is the function of the DMA address register?
- What is the function of the DMA count register?

#### Broad Questions
- Explain the operation of a DMA controller with a block diagram.
- Explain the functions of a DMA controller.
- Describe the DMA transfer sequence.
- Explain the handshaking signals used in DMA.
- Compare DMA with programmed I/O.
- Compare DMA with interrupt-driven I/O.
- Explain burst mode and cycle stealing.
- Design a state transition diagram for a DMA controller.
- Design a DMA controller using the One-Hot method.
- Solve a DMA timing/performance calculation.

---

### 7. Quick Revision Sheet

```
DMA
│
├── Direct I/O ↔ Memory transfer
│
├── CPU initializes DMA
│
├── I/O → DREQ
│
├── DMA → HRQ/HOLD
│
├── CPU → HLDA
│
├── DMA → DACK
│
├── Transfer data
│
├── Address++
│
├── Count--
│
├── Count = 0?
│      │
│      ├── NO → Continue
│      │
│      └── YES → Terminal Count
│                    ↓
│                 Interrupt
│                    ↓
│                 Release bus
│
├── Modes
│   ├── Burst
│   ├── Cycle Stealing
│   └── Transparent
│
└── Important registers
    ├── Address Register
    ├── Count Register
    ├── Control Register
    └── Status Register
```

---

### 8. The 5 Things You MUST Understand

If you have very little background knowledge, focus on these five ideas first:

#### ① DMA means direct transfer

```
I/O ─────────→ Memory
```

instead of:

```
I/O → CPU → Memory
```

#### ② CPU initializes DMA

The CPU tells DMA:

```
WHERE?     → Address
HOW MUCH?  → Count
WHICH WAY? → Direction
```

#### ③ DMA must get the bus

```
DMA → HRQ/HOLD → CPU
CPU → HLDA     → DMA
```

#### ④ DMA transfers the data

```
For I/O → Memory:  IOR + MEMW
For Memory → I/O:  MEMR + IOW
```

#### ⑤ DMA stops when Count = 0

```
Count = Count - 1

Count = 0
   ↓
Transfer complete
   ↓
Interrupt CPU
   ↓
Release bus
```

---

### 9. One-Line Memory Trick

> "Request → Get Bus → Acknowledge → Transfer → Update → Finish."

```
DREQ
 ↓
HRQ
 ↓
HLDA
 ↓
DACK
 ↓
TRANSFER
 ↓
ADDRESS++ / COUNT--
 ↓
COUNT = 0
 ↓
INTERRUPT
```

This sequence is the most important part for an exam.

---

### ⚠️ One Correction to Keep in Mind

The exact signal names and timing can vary between DMA implementations. For example, **HRQ/HOLD and HLDA** are common terminology in certain CPU/DMA architectures, while other systems use different names. In an exam, use the signal names given in your course's diagram or textbook.