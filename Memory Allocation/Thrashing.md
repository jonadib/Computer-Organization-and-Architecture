# Thrashing

This is very important for exams.

## 1. Simple Definition

> **Thrashing** occurs when the computer spends most of its time moving pages between RAM and disk instead of executing programs.

```
CPU
 ↓
Needs Page 1
 ↓
Page 1 not in RAM
 ↓
Page Fault
 ↓
Get Page 1 from Disk
 ↓
Needs Page 2
 ↓
Page 2 not in RAM
 ↓
Page Fault
 ↓
Get Page 2 from Disk
 ↓
Again...
```

The CPU spends almost all its time dealing with page faults instead of doing useful work.

---

## 2. Why Does Thrashing Happen?

Suppose a program needs these pages frequently: P1, P2, P3, P4, P5.

But RAM has only **2 frames**:

```
RAM

┌──────┬──────┐
│ P1   │ P2   │
└──────┴──────┘
```

Now the CPU needs P3. P1 or P2 must be removed:

```
P1 P2
 ↓
P3
```

Then the CPU needs P1 again:

```
P3 P2
 ↓
P1
```

Then P2:

```
P1 P2
 ↓
P3
```

**Constant replacement occurs:**

```
Disk ↔ RAM ↔ Disk ↔ RAM ↔ Disk
```

This is thrashing — the working set of pages the program actually needs doesn't fit in the frames available, so pages keep getting swapped in and out.

---

## 3. Connection Between Page Fault and Thrashing

Remember this chain:

```
Page not in RAM
       ↓
   Page Fault
       ↓
OS loads page from Disk
       ↓
Maybe another page is removed
       ↓
Too many page faults
       ↓
Very little actual CPU work
       ↓
     THRASHING
```

---

## ⭐ Exam-Ready Answer

**Q: What is thrashing?**
> Thrashing is a condition in which the system spends most of its time handling page faults and transferring pages between disk and main memory instead of executing programs.

---

*See also: [Contiguous vs Non-Contiguous Allocation](01-Contiguous-vs-Non-Contiguous-Allocation.md), [Fragmentation](02-Fragmentation.md), [Preemptive vs Non-Preemptive Allocation](03-Preemptive-vs-Non-Preemptive-Allocation.md), [Exam Revision Sheet](05-Memory-Management-Exam-Revision.md)*