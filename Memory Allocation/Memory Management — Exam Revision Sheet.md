# Memory Management — Exam Revision Sheet

## 1. Don't Confuse These Terms

| Term | Meaning |
|---|---|
| **Page** | A fixed-size piece of virtual memory. |
| **Frame** | A fixed-size piece of physical memory. |
| **Page Fault** | Requested page is not currently in RAM. |
| **Page Replacement** | Choosing which page to remove when RAM is full. |
| **Fragmentation** | Memory space is wasted. |
| **Thrashing** | Too many page faults/swapping cause the system to spend most of its time moving pages instead of executing. |

---

## 2. One Big Diagram

```
                  MEMORY MANAGEMENT
                         │
          ┌──────────────┴──────────────┐
          │                             │
     CONTIGUOUS                  NON-CONTIGUOUS
          │                             │
   Process together              Process scattered
          │                             │
          │                    ┌────────┴────────┐
          │                    │                 │
          │                  Paging         Segmentation
          │                    │                 │
          │              Fixed-size         Variable-size
          │              pages/frames         segments
          │
          └──────────────┐
                         │
                   Fragmentation
                         │
                 ┌───────┴────────┐
                 │                │
             Internal          External
                 │                │
              Inside          Outside
                 │                │
              Paging       Variable partition
                                  │
                              Solution
                                  ↓
                              Compaction
```

---

## 3. Most Important Exam Differences

### Paging vs Segmentation

```
PAGING                       SEGMENTATION
↓                             ↓
Fixed size                   Variable size
↓                             ↓
Page + Frame                 Code/Data/Stack
↓                             ↓
Physical memory oriented     Logical program oriented
```

### Internal vs External Fragmentation

```
INTERNAL                     EXTERNAL
↓                             ↓
Inside                       Outside
↓                             ↓
Allocated block               Between processes
↓                             ↓
Unused space                  Scattered holes
```

### Contiguous vs Non-Contiguous

```
CONTIGUOUS
[P1][P1][P1][P1]

NON-CONTIGUOUS
[P1][P2][P1][P3][P1]
```

---

## 4. All Exam-Ready Short Answers in One Place

**Q: What is contiguous memory allocation?**
> A memory allocation technique in which a process is loaded into one continuous block of physical memory.

**Q: What is non-contiguous memory allocation?**
> Allows different parts of a process to be stored in different locations of physical memory. Paging and segmentation are examples.

**Q: What is internal fragmentation?**
> The unused memory space inside an allocated memory block. Example: a 10 MB partition allocated to a 7 MB process wastes 3 MB.

**Q: What is external fragmentation?**
> Occurs when free memory is divided into many small, non-contiguous holes, making it difficult to allocate a large continuous block.

**Q: How can external fragmentation be reduced?**
> Using compaction (moves allocated blocks together to combine scattered free space) or by using paging, which eliminates external fragmentation entirely.

**Q: What is thrashing?**
> A condition in which the system spends most of its time handling page faults and transferring pages between disk and main memory instead of executing programs.

---

*See the full topic breakdown: [Contiguous vs Non-Contiguous Allocation](01-Contiguous-vs-Non-Contiguous-Allocation.md) · [Fragmentation](02-Fragmentation.md) · [Preemptive vs Non-Preemptive Allocation](03-Preemptive-vs-Non-Preemptive-Allocation.md) · [Thrashing](04-Thrashing.md)*