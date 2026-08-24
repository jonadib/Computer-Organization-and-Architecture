# Fragmentation — Internal and External

## What is Fragmentation?

Fragmentation simply means: **memory space is wasted.**

There are two types:

1. Internal fragmentation
2. External fragmentation

---

## 1. Internal Fragmentation

*Internal* = **inside**

Memory is wasted **inside** the allocated area.

### Example

Suppose a partition has size **10 MB**, but a program needs **7 MB**.

```
Partition
┌──────────────────────────┐
│     Program = 7 MB       │
│                          │
│     Wasted = 3 MB        │
└──────────────────────────┘
```

That 3 MB is wasted *inside* the allocated partition.

> **Internal fragmentation = wasted space inside an allocated block.**

### Easy memory trick

```
Internal → Inside
```

---

## 2. External Fragmentation

*External* = **outside**

Suppose memory looks like this:

```
┌────┬────┬────┬────┬────┬────┬────┬────┐
│ P1 │Free│ P2 │Free│ P3 │Free│ P4 │Free│
└────┴────┴────┴────┴────┴────┴────┴────┘
```

There is free memory, but it is divided into many small pieces.

Suppose: `Free = 2 MB + 3 MB + 4 MB`

Total free memory:

$$2 + 3 + 4 = 9 \text{ MB}$$

A new program needs **8 MB**. You technically have 9 MB free — but there is **no single continuous 8 MB block**. Therefore the program cannot fit in contiguous allocation.

**This is external fragmentation.**

### Definition

> External fragmentation is the wasted free space outside allocated blocks, where free memory is scattered into small holes.

### Memory trick

```
Internal → Inside allocated block
External → Outside, scattered holes
```

---

## 3. Internal vs External Fragmentation

| Feature | Internal | External |
|---|---|---|
| Meaning | Waste inside allocated space | Waste outside allocated space |
| Location | Inside partition/block | Between allocated blocks |
| Example | 10 MB allocated, 7 MB used | 2 + 3 + 4 MB scattered free |
| Common with | Fixed-size allocation | Variable-size allocation |
| Memory trick | Inside | Outside |

```
INTERNAL                    EXTERNAL
↓                            ↓
Inside                       Outside
↓                            ↓
Allocated block              Between processes
↓                            ↓
Unused space                 Scattered holes
```

---

## 4. How to Solve External Fragmentation?

### Method 1: Compaction

The OS moves processes together.

**Before:**

```
[P1][Free][P2][Free][P3][Free]
```

**After compaction:**

```
[P1][P2][P3][Free][Free][Free]
```

Now all free space is together.

**Problem?** Moving programs takes time.

> Compaction reduces external fragmentation but is expensive/time-consuming.

### Method 2: Paging

Paging doesn't require a process to occupy one continuous area. For example:

```
Page 0 → Frame 2
Page 1 → Frame 7
Page 2 → Frame 1
Page 3 → Frame 5
```

So the free spaces don't need to be combined.

> **Paging eliminates external fragmentation.**

However, paging can have small **internal** fragmentation, especially in the last page (if the process doesn't perfectly fill its final page).

---

## ⭐ Exam-Ready Short Answers

**Q: What is internal fragmentation?**
> Internal fragmentation is the unused memory space inside an allocated memory block. Example: A 10 MB partition is allocated to a 7 MB process, so 3 MB is wasted.

**Q: What is external fragmentation?**
> External fragmentation occurs when free memory is divided into many small, non-contiguous holes, making it difficult to allocate a large continuous block.

**Q: How can external fragmentation be reduced?**
> External fragmentation can be reduced using compaction, which moves allocated blocks together and combines scattered free spaces into one large free block. Paging can eliminate external fragmentation entirely.

---

*See also: [Contiguous vs Non-Contiguous Allocation](01-Contiguous-vs-Non-Contiguous-Allocation.md), [Preemptive vs Non-Preemptive Allocation](03-Preemptive-vs-Non-Preemptive-Allocation.md), [Thrashing](04-Thrashing.md), [Exam Revision Sheet](05-Memory-Management-Exam-Revision.md)*