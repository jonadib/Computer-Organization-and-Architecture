# Cache Mapping — Direct Mapping

## Why Do We Need Mapping?

Main memory is much larger than cache.

```
Main Memory
┌──────────────────────────────┐
│ Block 0                      │
│ Block 1                      │
│ Block 2                      │
│ ...                          │
│ Block 1000                   │
└──────────────────────────────┘


Cache
┌──────────────┐
│ Line 0       │
│ Line 1       │
│ Line 2       │
│ ...          │
│ Line 31      │
└──────────────┘
```

So we need a rule to decide: **where should a main-memory block be placed in cache?**

There are three major methods:

1. **Direct Mapping**
2. Fully Associative Mapping
3. Set-Associative Mapping

This file covers **Direct Mapping**.

---

## 1. Basic Idea

In direct mapping, every main-memory block has **only one possible cache line**.

**Formula:**

$$i = j \bmod m$$

Where:
- *i* = cache line
- *j* = main-memory block
- *m* = number of cache lines

---

## 2. Example

Suppose cache has **m = 4** lines.

Main-memory blocks: 0, 1, 2, 3, 4, 5, 6, 7...

**Mapping:**

```
0 mod 4 = 0
1 mod 4 = 1
2 mod 4 = 2
3 mod 4 = 3
4 mod 4 = 0
5 mod 4 = 1
```

| Memory Block | Cache Line |
|---|---|
| 0 | → 0 |
| 1 | → 1 |
| 2 | → 2 |
| 3 | → 3 |
| 4 | → 0 |
| 5 | → 1 |
| 6 | → 2 |
| 7 | → 3 |

Notice:

```
Block 0  → Line 0
Block 4  → Line 0
Block 8  → Line 0
Block 12 → Line 0
```

They all compete for the same line.

---

## 3. Direct Mapping Address Format

The address is divided into:

```
┌──────────┬──────────┬──────────┐
│   TAG    │   LINE   │  WORD    │
└──────────┴──────────┴──────────┘
```

- **TAG** — Identifies which memory block is currently stored.
- **LINE** — Tells which cache line to look at.
- **WORD** — Tells which word/byte inside that block is needed.

---

## 4. Worked Example

Suppose:
- Cache has 16 lines
- Each block contains 4 words

Since 16 = 2⁴, the **Line field** needs **4 bits**.

Since 4 = 2², the **Word field** needs **2 bits**.

```
┌──────────────┬──────────┬────────┐
│     TAG      │   LINE   │  WORD  │
│              │  4 bits  │ 2 bits │
└──────────────┴──────────┴────────┘
```

The remaining address bits are used as the **Tag**.

---

## 5. Advantages and Disadvantages

### Advantages
- Simple
- Cheap
- Fast
- Easy to implement

### Disadvantage

The major problem is **conflict miss**.

Example:

```
Block 0  → Cache Line 0
Block 16 → Cache Line 0
```

If the CPU repeatedly accesses:

```
0 → 16 → 0 → 16 → 0 → 16
```

the blocks continuously replace each other:

```
Line 0:
Block 0
 ↓
Block 16
 ↓
Block 0
 ↓
Block 16
```

This causes many misses, even though the rest of the cache may be empty.

---

## ⭐ Exam Definition

> **Direct Mapping:** Each main-memory block can be placed in only one specific cache line.

---

*See also: [Cache Memory Basics](01-Cache-Memory-Basics.md), [Fully Associative Mapping](03-Fully-Associative-Mapping.md), [Set-Associative Mapping](04-Set-Associative-Mapping.md)*