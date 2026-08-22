# 10. What is an Addressing Mode?

An **addressing mode** specifies:

> **How the CPU finds the operand of an instruction.**

For example:

```text
LOAD R1, 500
```

Where is the data?

Is `500`:

* The actual data?
* A memory address?
* An address stored in another register?

The addressing mode tells us the answer.

---

# 11. Why Do We Need Addressing Modes?

Different programs need different ways to access data.

### Constant

```text
MOV R1, 10
```

### Register

```text
MOV R1, R2
```

### Memory

```text
MOV R1, [500]
```

### Array

```text
MOV R1, [R2 + 4]
```

Therefore, different addressing modes provide **flexibility and efficiency**.

---

# 12. Important Addressing Modes

The most important addressing modes for exams are:

1. **Immediate**
2. **Direct**
3. **Indirect**
4. **Register**
5. **Register Indirect**
6. **Displacement**
7. **Stack**
8. **Relative**
9. **Auto-increment**
10. **Auto-decrement**

---

# 13. Immediate Addressing

In **immediate addressing**, the operand is directly included in the instruction.

Example:

```text
MOV R1, #25
```

Here:

```text
R1 ← 25
```

There is no need to access memory to obtain the value.

### Diagram

```text
Instruction
┌────────┬────────┐
│  MOV   │   25   │
└────────┴────────┘
              ↓
             R1
```

### Advantage

Very fast.

### Disadvantage

The constant is limited by the size of the instruction's operand field.

### Remember

> **Immediate = value is inside the instruction**

---

# 14. Direct Addressing

In direct addressing, the instruction contains the **memory address of the operand**.

Example:

```text
LOAD R1, 500
```

If:

```text
M[500] = 25
```

Then:

```text
R1 ← M[500]
```

Therefore:

```text
R1 ← 25
```

### Diagram

```text
Instruction
┌────────┬─────────┐
│  LOAD  │   500   │
└────────┴────┬────┘
              ↓
         Memory[500]
              ↓
             25
              ↓
             R1
```

### Remember

> **Direct = instruction directly gives the memory address**

---

# 15. Indirect Addressing

In indirect addressing, the address field points to a memory location that contains the **actual address** of the operand.

Suppose:

```text
Instruction: LOAD R1, 500

M[500] = 800
M[800] = 25
```

First:

```text
500 → 800
```

Then:

```text
800 → 25
```

Therefore:

```text
R1 = 25
```

### Diagram

```text
Instruction
     │
     │ address = 500
     ↓
Memory[500]
     │
     │ contains 800
     ↓
Memory[800]
     │
     │ contains 25
     ↓
    R1
```

### Remember

> **Indirect = address of an address**

---

# 16. Register Addressing

The operand is stored in a CPU register.

Example:

```text
ADD R1, R2
```

Suppose:

```text
R1 = 10
R2 = 20
```

Then:

```text
R1 ← R1 + R2
```

```text
R1 ← 30
```

### Diagram

```text
R1 = 10 ──┐
          ├──→ ALU → 30
R2 = 20 ──┘
```

### Advantage

Very fast because registers are inside the CPU.

### Remember

> **Register = operand is in a register**

---

# 17. Register Indirect Addressing

Here the register contains the **memory address** of the operand.

Suppose:

```text
R2 = 500
M[500] = 25
```

Instruction:

```text
LOAD R1, (R2)
```

Means:

```text
R1 ← M[R2]
```

Therefore:

```text
R1 ← M[500]
```

```text
R1 ← 25
```

### Diagram

```text
R2
 │
 │ contains 500
 ↓
Memory[500]
 │
 │ contains 25
 ↓
R1
```

### Remember

> **Register Indirect = register contains the address**

---

# 18. Displacement Addressing

Displacement addressing combines:

> **Register + Constant**

### Formula

**Effective Address = Register + Displacement**

### Example

Suppose:

```text
R2 = 1000
Displacement = 20
```

Using the formula:

**EA = Register + Displacement**

**EA = 1000 + 20**

**EA = 1020**

So:

```text
LOAD R1, 20(R2)
```

means:

```text
R1 ← M[1020]
```

### Common Uses

* Arrays
* Records
* Structures

### Remember

> **Displacement = Register + Constant**

---

# 19. Relative Addressing

In relative addressing, the effective address is calculated using the **Program Counter (PC)** and a displacement.

### Formula

**Effective Address = PC + Displacement**

### Example

Suppose:

```text
PC = 1000
Displacement = 50
```

Using the formula:

**EA = PC + Displacement**

**EA = 1000 + 50**

**EA = 1050**

This is commonly used in:

* Branch instructions
* Jump instructions

Example:

```text
BEQ +50
```

This means branch relative to the current PC.

### Remember

> **Relative = PC + Displacement**

---

# 20. Auto-Increment Addressing

The register contains the address.

After accessing the operand, the register is automatically increased.

### Example

Suppose:

```text
R1 = 1000
M[1000] = 50
```

Instruction:

```text
LOAD R2, (R1)+
```

First:

```text
R2 ← M[1000]
```

Then:

```text
R1 ← R1 + 1
```

Therefore:

```text
R2 = 50
R1 = 1001
```

### Use

Very useful for processing arrays.

### Remember

> **Auto-increment = Use address, then increase register**

---

# 21. Auto-Decrement Addressing

The register is first decreased, then used as the address.

### Example

Suppose:

```text
R1 = 1000
```

Instruction:

```text
LOAD R2, -(R1)
```

First:

```text
R1 ← R1 - 1
```

Therefore:

```text
R1 = 999
```

Then:

```text
R2 ← M[999]
```

### Use

Useful for stack operations.

### Remember

> **Auto-decrement = Decrease register, then use address**

---

# 22. Stack Addressing

The operand is implicitly located at the **top of the stack**.

Example:

```text
PUSH A
PUSH B
ADD
```

The `ADD` instruction does not specify the operands.

It automatically takes operands from the stack.

```text
       Stack
     ┌─────┐
Top →│  B  │
     ├─────┤
     │  A  │
     └─────┘
        ↓
       ADD
        ↓
       A+B
```

This is a **zero-address instruction**.

### Remember

> **Stack = operand is taken from the top of the stack**

---

# ⭐ Quick Comparison

| Addressing Mode       | Main Idea                           |
| --------------------- | ----------------------------------- |
| **Immediate**         | Value is inside instruction         |
| **Direct**            | Instruction contains memory address |
| **Indirect**          | Address points to another address   |
| **Register**          | Operand is in a register            |
| **Register Indirect** | Register contains memory address    |
| **Displacement**      | Register + Constant                 |
| **Relative**          | PC + Displacement                   |
| **Auto-increment**    | Use address → increase register     |
| **Auto-decrement**    | Decrease register → use address     |
| **Stack**             | Operand is at top of stack          |

# 🧠 Super Easy Memory Trick

**Immediate → Value**

**Direct → Address**

**Indirect → Address of address**

**Register → Value in register**

**Register Indirect → Address in register**

**Displacement → Register + Constant**

**Relative → PC + Constant**

**Auto-increment → Use → Increase**

**Auto-decrement → Decrease → Use**

**Stack → Top of stack**
