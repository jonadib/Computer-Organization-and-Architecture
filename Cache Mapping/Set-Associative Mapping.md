# Cache Mapping — Set-Associative Mapping

This is a **combination of direct and associative mapping**.

## 1. Basic Idea

The cache is divided into **sets**. Each set contains multiple lines.

For example, a **2-way set-associative cache**:

```
             CACHE


Set 0 ┌──────────────┐
      │ Line 0       │
      │ Line 1       │
      └──────────────┘


Set 1 ┌──────────────┐
      │ Line 2       │
      │ Line 3       │
      └──────────────┘


Set 2 ┌──────────────┐
      │ Line 4       │
      │ Line 5       │
      └──────────────┘
```

Each set has 2 lines, so it is called **2-way** set-associative.

---

## 2. Worked Example — Finding the Sets

Suppose:
- Cache has **8 lines**
- **2 lines per set**

Then:

$$\text{Number of sets} = \frac{8}{2} = 4$$

```
Set 0 → Lines 0, 1
Set 1 → Lines 2, 3
Set 2 → Lines 4, 5
Set 3 → Lines 6, 7
```

**Formula:**

$$i = j \bmod v$$

Where:
- *j* = memory block
- *v* = number of sets

---

## 3. Worked Example — Mapping a Block

Suppose *j* = 10 and *v* = 4:

$$10 \bmod 4 = 2$$

Therefore: **Block 10 → Set 2**

But because Set 2 has two lines, Block 10 can occupy **either line** in Set 2:

```
Block 10
    │
    ▼
  Set 2
  ┌───────┐
  │Line 4 │ ← possible
  │Line 5 │ ← possible
  └───────┘
```

---

## 4. Address Format

```
┌──────────┬──────────┬──────────┐
│   TAG    │   SET    │   WORD   │
└──────────┴──────────┴──────────┘
```

The **SET** field identifies the set. Then the tag is compared with the tags of the lines inside that set only (not the whole cache).

---

## 5. Direct vs Fully Associative vs Set-Associative

| Feature | Direct | Fully Associative | Set-Associative |
|---|---|---|---|
| Block location | One fixed line | Any line | Any line within selected set |
| Hardware | Simple | Complex | Medium |
| Cost | Low | High | Medium |
| Speed | Fast | Potentially slower due to comparisons | Medium |
| Conflict misses | High | Very low | Lower |
| Flexibility | Low | Very high | Medium |
| Example | Block 5 → fixed line | Block 5 → any line | Block 5 → any line in its set |

### 🧠 Easy memory trick

```
DIRECT
↓
One fixed place


ASSOCIATIVE
↓
Anywhere


SET-ASSOCIATIVE
↓
One set → several possible places
```

---

## ⭐ Exam Definition

> **Set-Associative Mapping:** A main-memory block maps to one particular set but can be placed in any line within that set.

---

*See also: [Cache Memory Basics](01-Cache-Memory-Basics.md), [Direct Mapping](02-Direct-Mapping.md), [Fully Associative Mapping](03-Fully-Associative-Mapping.md)*