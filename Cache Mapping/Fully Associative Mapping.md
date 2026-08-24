# Cache Mapping — Fully Associative Mapping

Also called **Associative Mapping**.

## 1. Basic Idea

Any memory block can go into **any** cache line.

```
Memory Block 5   ───► Any Cache Line
Memory Block 25  ───► Any Cache Line
Memory Block 100 ───► Any Cache Line
```

There is no fixed line.

### Diagram

```
             Main Memory
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
     Block 5   Block 20   Block 50
       │         │         │
       └─────────┼─────────┘
                 ↓
        ┌─────────────────┐
        │      CACHE      │
        ├─────────────────┤
        │ Line 0           │
        │ Line 1           │
        │ Line 2           │
        │ ...              │
        └─────────────────┘


       Any block → Any line
```

---

## 2. Address Format

There is **no line field**.

```
┌────────────────────┬────────────┐
│        TAG         │    WORD    │
└────────────────────┴────────────┘
```

The cache compares the tag with **all** cache lines.

---

## 3. Worked Example

Suppose the requested tag is:

```
101101
```

Cache checks:

```
Line 0 → 100010
Line 1 → 101101  ✓ HIT
Line 2 → 001100
Line 3 → 111000
```

So the data is found in **Line 1**.

---

## 4. Advantages and Disadvantages

### Advantages
- Very flexible
- Any block can go anywhere
- Avoids direct-mapping conflict problems
- Usually gives a better hit ratio

### Disadvantages
- Expensive
- Complex hardware
- Must compare the tag with many/all cache lines

---

## ⭐ Exam Sentence

> In fully associative mapping, any main-memory block can be placed in any cache line, providing flexibility at the cost of more complex and expensive hardware.

---

*See also: [Cache Memory Basics](01-Cache-Memory-Basics.md), [Direct Mapping](02-Direct-Mapping.md), [Set-Associative Mapping](04-Set-Associative-Mapping.md)*