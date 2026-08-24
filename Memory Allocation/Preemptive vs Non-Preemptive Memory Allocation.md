# Preemptive vs Non-Preemptive Memory Allocation

This part can be confusing because these terms are more commonly associated with CPU scheduling. In the memory-allocation context, think about the question: **can the OS take memory away from a process before that process gives it up voluntarily?**

---

## 1. Non-Preemptive Allocation

Once memory is allocated:

```
Process P1
     ↓
Gets memory
     ↓
Keeps memory
     ↓
Releases/terminates
     ↓
Memory becomes free
```

The OS does **not** reclaim it before the process releases it.

### Problem

Suppose:

```
RAM
┌────┬────┬────┬────┐
│ P1 │ P2 │ P3 │ P4 │
└────┴────┴────┴────┘
```

But all processes are waiting for I/O. The CPU may have nothing useful to execute — and no memory is being freed up to let a *different*, ready process in.

---

## 2. Preemptive Allocation

The OS **can** temporarily take resources/memory from a process. A common idea is **swapping**.

```
RAM                         Disk
┌────┬────┬────┐            ┌─────┐
│ P1 │ P2 │ P3 │   ←→       │ P4  │
└────┴────┴────┘            └─────┘
```

The OS can move a blocked process from RAM to disk. Then another ready process can be brought into RAM.

### Simple flow

```
Process blocked
      ↓
OS swaps it out
      ↓
Memory becomes free
      ↓
Another process enters
      ↓
CPU continues working
```

---

## ⭐ Quick Comparison

| | Non-Preemptive | Preemptive |
|---|---|---|
| Can OS reclaim memory early? | No | Yes |
| Memory released when? | Only when process finishes/releases it | Can be taken while process is still alive (e.g., swapped out) |
| Typical mechanism | Simple fixed allocation | Swapping |
| Risk | CPU may idle while memory sits unused by blocked processes | Overhead of moving processes to/from disk |

---

*See also: [Contiguous vs Non-Contiguous Allocation](01-Contiguous-vs-Non-Contiguous-Allocation.md), [Fragmentation](02-Fragmentation.md), [Thrashing](04-Thrashing.md), [Exam Revision Sheet](05-Memory-Management-Exam-Revision.md)*