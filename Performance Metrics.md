# Performance Metrics — Easy Exam Notes

These are used to **measure how fast and efficient a computer/CPU is**.

The most important metrics are:

1. **Clock Speed**
2. **CPI**
3. **Execution Time**
4. **MIPS**
5. **Latency**
6. **Throughput**

---

## 1. Clock Speed

Clock speed tells us **how many clock cycles the CPU performs per second**.

It is measured in:

* **Hz**
* **MHz** = million cycles/second
* **GHz** = billion cycles/second

### Example

If CPU clock speed = **3 GHz**

Using:

**1 GHz = 10⁹ Hz**

Therefore:

**3 GHz = 3 × 10⁹ Hz**

So the CPU has:

> **3 billion clock cycles per second.**

### Important

Higher clock speed **generally** means faster processing, but it does **not always mean a faster CPU** because CPI, architecture, memory, etc. also matter.

---

## 2. CPI — Cycles Per Instruction

**CPI = Cycles Per Instruction**

It tells us:

> **How many clock cycles are needed on average to execute one instruction.**

### Formula

**CPI = Total Clock Cycles / Instruction Count**

### Example

Suppose:

* Instruction Count = **100**
* Total Clock Cycles = **200**

Using the formula:

**CPI = Total Clock Cycles / Instruction Count**

**CPI = 200 / 100**

**CPI = 2**

So:

> Each instruction takes an average of **2 clock cycles**.

### Important

**Lower CPI = Better performance**, assuming other factors are comparable.

---

## 3. Execution Time

Execution time means:

> **The total time required by the CPU to execute a program.**

This is one of the **most important performance formulas**.

### Formula

**CPU Time = Instruction Count × CPI × Clock Cycle Time**

Since:

**Clock Cycle Time = 1 / Clock Rate**

Therefore:

**CPU Time = (Instruction Count × CPI) / Clock Rate**

### Example

Suppose:

* Instruction Count = **1,000,000**
* CPI = **2**
* Clock Rate = **2 GHz**

First convert the clock rate:

**2 GHz = 2 × 10⁹ Hz**

Using the formula:

**CPU Time = (Instruction Count × CPI) / Clock Rate**

**CPU Time = (1,000,000 × 2) / (2 × 10⁹)**

**CPU Time = 2,000,000 / 2,000,000,000**

**CPU Time = 0.001 seconds**

Therefore:

> **Execution Time = 1 ms**

### Remember

To make execution time smaller:

* Reduce instruction count
* Reduce CPI
* Increase clock rate

---

## 4. MIPS

MIPS means:

> **Million Instructions Per Second**

It tells us approximately how many **millions of instructions** a processor executes per second.

### Formula

**MIPS = Clock Rate / (CPI × 10⁶)**

If clock rate is expressed in MHz:

**MIPS = Clock Rate (MHz) / CPI**

### Example

Suppose:

* Clock Rate = **2 GHz**
* CPI = **2**

First convert GHz to MHz:

**2 GHz = 2000 MHz**

Using the formula:

**MIPS = Clock Rate (MHz) / CPI**

**MIPS = 2000 / 2**

**MIPS = 1000**

Therefore:

> **MIPS = 1000 million instructions per second**

---

## 5. Latency

Latency means:

> **The time required to complete one operation or respond to one request.**

Think:

**"How long do I have to wait for one task?"**

### Example

Suppose a memory request takes:

**100 ns**

Therefore:

> **Latency = 100 ns**

### Simple Example

You click:

**Open file → 0.5 seconds → file opens**

The **0.5 seconds** is the latency.

### Remember

> **Latency = Time for one task**

---

## 6. Throughput

Throughput means:

> **How much work can be completed in a given amount of time.**

Think:

**"How many tasks can I complete per second?"**

### Example

A server processes:

**10,000 requests/second**

Therefore:

> **Throughput = 10,000 requests/s**

Another example:

Factory A produces **100 products/hour**.

Factory B produces **200 products/hour**.

Therefore:

> **Factory B has higher throughput.**

---

# ⭐ Latency vs Throughput

This is very important.

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

# 🔥 All Metrics Together

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

* Clock Speed = **2 GHz**
* Instruction Count = **1 billion**
* CPI = **2**

### Step 1: Convert Clock Speed

**2 GHz = 2 × 10⁹ Hz**

### Step 2: Calculate Execution Time

Using:

**CPU Time = (Instruction Count × CPI) / Clock Rate**

Substitute the values:

**CPU Time = (1 × 10⁹ × 2) / (2 × 10⁹)**

**CPU Time = 2 × 10⁹ / 2 × 10⁹**

**CPU Time = 1 second**

Therefore:

> **Execution Time = 1 second**

### Step 3: Calculate MIPS

First convert:

**2 GHz = 2000 MHz**

Using:

**MIPS = Clock Rate (MHz) / CPI**

Substitute the values:

**MIPS = 2000 / 2**

**MIPS = 1000**

Therefore:

> **MIPS = 1000 million instructions per second**

---

# 🎯 Important Exam Points

Remember:

**Execution Time = (Instruction Count × CPI) / Clock Rate**

> **Higher clock rate → Lower execution time**

> **Lower CPI → Lower execution time**

> **Lower latency → Faster individual response**

> **Higher throughput → More work per second**

> **MIPS → Million instructions per second**

---

# 🧩 Easiest Way to Remember All Six

**Clock Speed → How fast the clock runs**

**CPI → How many cycles/instruction**

**Execution Time → How long the program takes**

**MIPS → How many million instructions/second**

**Latency → How long one task takes**

**Throughput → How much work per second**
