# Performance Metrics — Easy Exam Notes

Performance metrics are used to **measure how fast and efficient a computer/CPU is**.

## 1. Clock Speed

**Clock Speed** tells us how many clock cycles the CPU performs per second.

Measured in:

* **Hz** = cycles/second
* **MHz** = million cycles/second
* **GHz** = billion cycles/second

**Example:**
3 GHz = **3 billion clock cycles per second**

**Remember:** Higher clock speed generally means faster processing, but it does not always mean a faster CPU because CPI, architecture, memory, etc. also matter.

---

## 2. CPI — Cycles Per Instruction

CPI tells us:

> **How many clock cycles are needed on average to execute one instruction.**

### Formula

**CPI = Total Clock Cycles / Instruction Count**

**Example:**

* Instructions = 100
* Clock cycles = 200

CPI = 200 / 100 = **2**

So, each instruction takes an average of **2 clock cycles**.

**Remember:** Lower CPI = better performance, assuming other factors are comparable.

---

## 3. Execution Time

Execution time means:

> **The total time required by the CPU to execute a program.**

### Formula

**CPU Time = (Instruction Count × CPI) / Clock Rate**

**Example:**

* Instruction count = 1,000,000
* CPI = 2
* Clock rate = 2 GHz

CPU Time = (1,000,000 × 2) / (2 × 10⁹)
= **0.001 seconds = 1 ms**

### To reduce execution time:

* Reduce instruction count
* Reduce CPI
* Increase clock rate

---

## 4. MIPS

MIPS means:

> **Million Instructions Per Second**

It tells us approximately how many millions of instructions a processor executes per second.

### Formula

**MIPS = Clock Rate / (CPI × 10⁶)**

If clock rate is in MHz:

**MIPS = Clock Rate (MHz) / CPI**

**Example:**

* Clock rate = 2 GHz = 2000 MHz
* CPI = 2

MIPS = 2000 / 2 = **1000 MIPS**

So the CPU executes approximately **1000 million instructions/second**.

---

## 5. Latency

Latency means:

> **The time required to complete one operation or respond to one request.**

**Remember:**

> **Latency = Time for one task**

**Example:**
A memory request takes 100 ns → latency = **100 ns**

---

## 6. Throughput

Throughput means:

> **How much work can be completed in a given amount of time.**

**Remember:**

> **Throughput = Work completed per unit time**

**Example:**
A server processes 10,000 requests/second → throughput = **10,000 requests/s**

---

## ⭐ Latency vs Throughput

| Latency                         | Throughput                             |
| ------------------------------- | -------------------------------------- |
| Time required for one task      | Amount of work completed per unit time |
| Lower is better                 | Higher is better                       |
| Example: 10 ms/request          | Example: 1000 requests/sec             |
| Focuses on individual operation | Focuses on overall workload            |

### Easy Memory Trick

> **Latency = How long?**

> **Throughput = How many?**

---

# ⭐ All Metrics Together

| Metric             | Meaning                   | Better Performance      |
| ------------------ | ------------------------- | ----------------------- |
| **Clock Speed**    | Cycles per second         | Higher generally better |
| **CPI**            | Cycles per instruction    | Lower                   |
| **Execution Time** | Time to execute program   | Lower                   |
| **MIPS**           | Million instructions/sec  | Higher                  |
| **Latency**        | Time for one operation    | Lower                   |
| **Throughput**     | Work completed per second | Higher                  |

---

# ⭐ Most Important Formulas

### 1. Clock Cycle Time

**Clock Cycle Time = 1 / Clock Rate**

### 2. CPU Execution Time

**CPU Time = (Instruction Count × CPI) / Clock Rate**

### 3. CPI

**CPI = Total Clock Cycles / Instruction Count**

### 4. MIPS

**MIPS = Clock Rate / (CPI × 10⁶)**

---

# 🧠 One Example Connecting Everything

Suppose a CPU has:

* Clock speed = **2 GHz**
* Instruction count = **1 billion**
* CPI = **2**

### Execution Time

T = (1 × 10⁹ × 2) / (2 × 10⁹)

T = **1 second**

### MIPS

MIPS = 2000 / 2

MIPS = **1000 MIPS**

So this CPU executes approximately:

> **1000 million instructions per second**

---

# 🎯 Exam Shortcut

**Execution Time = (Instruction Count × CPI) / Clock Rate**

Remember:

* **Higher clock rate → lower execution time**
* **Lower CPI → lower execution time**
* **Lower latency → faster individual response**
* **Higher throughput → more work per second**
* **MIPS → million instructions per second**

## 🧠 Easiest Way to Remember All Six

* **Clock Speed →** How fast the clock runs
* **CPI →** How many cycles/instruction
* **Execution Time →** How long the program takes
* **MIPS →** How many million instructions/second
* **Latency →** How long one task takes
* **Throughput →** How much work per second
