# Data Manipulation Instructions

## 23. What Are Data Manipulation Instructions?

Data manipulation instructions are instructions that:

> **Move, modify, compare, or perform operations on data.**

They are generally divided into:

1. **Data Transfer**
2. **Arithmetic**
3. **Logical**
4. **Shift/Rotate**

---

# 24. Data Transfer Instructions

These instructions move data from one location to another.

They **normally do not change the value of the data**.

Common instructions:

* `MOV`
* `LOAD`
* `STORE`
* `PUSH`
* `POP`

---

## MOV

Moves data between registers or locations.

Example:

```text id="m7gqwr"
MOV R1, R2
```

If:

```text id="f1r7jc"
R2 = 50
```

Then:

```text id="h6jv0f"
R1 = 50
```

---

## LOAD

Moves data from memory to a register.

```text id="0y0k3x"
LOAD R1, [500]
```

If:

```text id="t2m1n8"
M[500] = 100
```

Then:

```text id="7u8o1k"
R1 = 100
```

---

## STORE

Moves data from a register to memory.

```text id="k7p0de"
STORE R1, [500]
```

If:

```text id="0h2x4f"
R1 = 100
```

Then:

```text id="n4k8zq"
M[500] = 100
```

### Easy Difference

```text id="m6x8t2"
LOAD  → Memory → CPU
STORE → CPU → Memory
```

---

# 25. Arithmetic Instructions

Arithmetic instructions perform mathematical operations.

Common examples:

* `ADD`
* `SUB`
* `MUL`
* `DIV`
* `INC`
* `DEC`

## ADD

```text id="2b3f4v"
ADD R1, R2
```

**R1 = R1 + R2**

---

## SUB

```text id="v7k3s9"
SUB R1, R2
```

**R1 = R1 − R2**

---

## MUL

**R1 = R1 × R2**

---

## DIV

**R1 = R1 / R2**

---

## INC

```text id="r3f7k1"
INC R1
```

**R1 = R1 + 1**

---

## DEC

```text id="a8p2c6"
DEC R1
```

**R1 = R1 − 1**

---

# 26. Logical Instructions

Logical instructions perform **bit-by-bit operations**.

Important ones:

* **AND**
* **OR**
* **NOT**
* **XOR**

---

## AND

Example:

```text id="q9m2wx"
A = 1010
B = 1100
```

Operation:

```text id="1j8k3d"
  1010
  1100
  ----
  1000
```

Result:

```text id="n6f4sz"
1000
```

### AND Rule

A bit is **1 only when both input bits are 1**.

---

## OR

Example:

```text id="r5y7k2"
  1010
  1100
  ----
  1110
```

Result:

```text id="c8v1p4"
1110
```

### OR Rule

A bit is **1 when at least one input bit is 1**.

---

## XOR

XOR gives **1 when the two bits are different**.

Example:

```text id="h3w9q5"
  1010
  1100
  ----
  0110
```

Result:

```text id="b7m2x8"
0110
```

### XOR Rule

**Same = 0**

**Different = 1**

---

## NOT

NOT changes:

```text id="z2c5n7"
0 → 1
1 → 0
```

Example:

```text id="p4v8k1"
NOT 1010
```

Result:

```text id="d6r3m9"
0101
```

---

# 27. Shift Instructions

Shift instructions move bits **left or right**.

Two common types:

* **Logical Shift**
* **Arithmetic Shift**

---

## Logical Shift Left

Example:

```text id="w5n2k8"
1011
```

Shift left:

```text id="e7c4p3"
0110
```

A bit is shifted out and a `0` enters from the right.

For unsigned numbers, a left shift by one position is approximately:

**×2**

---

## Logical Shift Right

Example:

```text id="s9f1d6"
1011
```

Shift right:

```text id="u3k7m2"
0101
```

For unsigned numbers, a right shift by one position is approximately:

**÷2**

---

# 28. Arithmetic Shift

Arithmetic shifts are especially useful for **signed numbers**.

## Arithmetic Right Shift

The **sign bit is preserved**.

Example:

```text id="q6v3x9"
10010100
```

Arithmetic right shift:

```text id="t8m2c5"
11001010
```

Notice that the leftmost `1` is retained.

---

# 29. Rotate Instructions

In rotation, bits shifted out from one side are brought back from the other side.

Example:

```text id="j4p7w1"
10110001
```

Rotate right:

```text id="k9d3s6"
11011000
```

The rightmost bit `1` comes back to the left.

---

# ⭐ Data Manipulation Instruction Summary

| Category          | Examples                    | Purpose                 |
| ----------------- | --------------------------- | ----------------------- |
| **Data Transfer** | MOV, LOAD, STORE, PUSH, POP | Move data               |
| **Arithmetic**    | ADD, SUB, MUL, DIV          | Mathematical operations |
| **Logical**       | AND, OR, XOR, NOT           | Bit manipulation        |
| **Shift**         | SHL, SHR, ASL, ASR          | Shift bits              |
| **Rotate**        | ROL, ROR                    | Rotate bits             |

---

# 🔥 One Complete Example

Suppose we want to calculate:

**C = (A + B) × 2**

Suppose:

```text id="v2q6m8"
A = 10
B = 20
```

One possible sequence:

```text id="r8k3w5"
LOAD R1, A
LOAD R2, B
ADD  R1, R2
SHL  R1, 1
STORE R1, C
```

### Step 1

```text id="e5p1n7"
LOAD R1, A
```

```text id="x3m8q2"
R1 = 10
```

### Step 2

```text id="c7v4d9"
LOAD R2, B
```

```text id="y1k6s3"
R2 = 20
```

### Step 3

```text id="h8q2w5"
ADD R1, R2
```

**R1 = 10 + 20 = 30**

### Step 4

```text id="m4n7p1"
SHL R1, 1
```

Left shift by one:

**30 × 2 = 60**

Therefore:

```text id="b6x3k9"
R1 = 60
```

### Step 5

```text id="d2s8v4"
STORE R1, C
```

Therefore:

**C = 60**

This one example uses:

* **Instruction Cycle**
* **Addressing**
* **LOAD**
* **ADD**
* **SHIFT**
* **STORE**

---

# 🧠 Super Easy Memory Trick

**Data Transfer → Move data**

**Arithmetic → Calculate**

**Logical → Compare/manipulate bits**

**Shift → Move bits left/right**

**Rotate → Move bits around**
