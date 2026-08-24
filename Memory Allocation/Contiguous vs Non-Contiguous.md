# Memory Management — Contiguous vs Non-Contiguous Allocation

## 0. Starting Idea

Before these topics, remember one basic idea:

> **Memory** = a large collection of storage locations where programs and data are kept while running.

Imagine RAM like a long row of rooms:

```
RAM
┌────┬────┬────┬────┬────┬────┬────┬────┐
│    │    │    │    │    │    │    │    │
└────┴────┴────┴────┴────┴────┴────┴────┘
```

When a program comes into memory, the OS must decide: **"Where should I put this program?"**

That is what **memory allocation** is about.

---

## 1. Contiguous Memory Allocation

### Meaning

*Contiguous* = together / side by side.

A process must occupy **one continuous area** of physical memory.

Suppose a program needs 4 MB. The OS finds:

```
RAM

┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ OS  │     │     │ P   │ P   │ P   │ P   │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
                  ←── Program ──→
```

The four blocks are next to each other.

### Easy example

Suppose memory has:

```
[ OS ][ Free ][ Free ][ Free ][ P1 ][ P1 ][ P1 ][ Free ]
```

If another program needs 3 blocks, it needs three **adjacent** free blocks:

```
[ ][ ][ ]
```

---

## 2. Non-Contiguous Memory Allocation

Here, a program **doesn't have to stay together**. Its parts can be scattered around memory.

```
RAM

┌────┬────┬────┬────┬────┬────┬────┬────┐
│ P1 │ P2 │ P1 │ P3 │ P1 │ P4 │ P2 │ P3 │
└────┴────┴────┴────┴────┴────┴────┴────┘
```

Parts of the same program can be in different locations.

Two important techniques implement this:

1. **Paging**
2. **Segmentation**

---

## 3. Paging (Quick Overview)

Suppose a program is:

```
Program
┌──────┬──────┬──────┬──────┐
│Page 0│Page 1│Page 2│Page 3│
└──────┴──────┴──────┴──────┘
```

The program is divided into equal-size pieces called **pages**. Physical memory is also divided into equal-size pieces called **frames**.

```
Virtual Memory             Physical Memory


┌──────┐                   ┌──────┐
│Page 0│ ────────────────→ │Frame 5│
├──────┤                   ├──────┤
│Page 1│ ────────────────→ │Frame 2│
├──────┤                   ├──────┤
│Page 2│ ────────────────→ │Frame 7│
├──────┤                   ├──────┤
│Page 3│ ────────────────→ │Frame 1│
└──────┘                   └──────┘
```

Notice:

```
Page 0 → Frame 5
Page 1 → Frame 2
Page 2 → Frame 7
Page 3 → Frame 1
```

They are scattered. A **page table** remembers these mappings.

**Remember:**
- Page = virtual/logical memory
- Frame = physical/RAM memory

---

## 4. Segmentation (Quick Overview)

Segmentation divides a program according to its **logical parts**.

```
Program
│
├── Code
├── Data
├── Stack
└── Other information
```

These become different **segments**. Unlike pages, segments can have **different sizes**.

Example:

```
Code  = 10 KB
Data  = 5 KB
Stack = 8 KB
```

| Paging | Segmentation |
|---|---|
| Fixed-size pages | Variable-size segments |
| Page = fixed size | Segment = different size |
| Based mainly on physical organization | Based on logical program structure |

### Easy memory trick

```
Paging        → Pieces of equal size
Segmentation  → Sections of a program
```

---

## 5. Contiguous vs Non-Contiguous — Exam Answer

**Contiguous**
> In contiguous memory allocation, a process is loaded into a single continuous area of physical memory.

**Non-contiguous**
> In non-contiguous memory allocation, a process can be divided into parts and these parts can be stored in different locations of physical memory.

**Examples:**

```
Contiguous:
[P1][P1][P1][P1]

Non-contiguous:
[P1][P2][P1][P3][P1]
```

---

## ⭐ Exam-Ready Short Answers

**Q: What is contiguous memory allocation?**
> Contiguous memory allocation is a memory allocation technique in which a process is loaded into one continuous block of physical memory.

**Q: What is non-contiguous memory allocation?**
> Non-contiguous memory allocation allows different parts of a process to be stored in different locations of physical memory. Paging and segmentation are examples.

---

*See also: [Fragmentation](02-Fragmentation.md), [Preemptive vs Non-Preemptive Allocation](03-Preemptive-vs-Non-Preemptive-Allocation.md), [Thrashing](04-Thrashing.md), [Exam Revision Sheet](05-Memory-Management-Exam-Revision.md)*