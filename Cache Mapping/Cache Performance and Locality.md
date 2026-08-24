# Cache Performance and Locality

## 1. Cache Performance — Key Factors

The most important factors are:

- Cache access time
- Main memory access time
- Hit ratio
- Miss ratio

Let:
- $H$ = Hit ratio
- $1 - H$ = Miss ratio

---

## 2. Average Memory Access Time

A common simplified formula is:

$$T_{avg} = T_c + (1 - H)T_m$$

Where:
- $T_c$ = cache access time
- $T_m$ = additional main-memory access time on a miss
- $H$ = hit ratio

### Example

Suppose:
- $T_c = 10$ ns
- $T_m = 100$ ns
- $H = 90\% = 0.9$

$$T_{avg} = 10 + (1 - 0.9)(100) = 10 + 10 = 20 \text{ ns}$$

So although main memory takes 100 ns, the average access time is only **20 ns** because most accesses are cache hits.

> **Note:** Some textbooks define $T_m$ as the *total* miss-service time including the cache check. In that convention, the formula is often written $T_{avg} = HT_c + (1-H)T_m$. Always follow the definition given in your question.

### Another Numerical Example

Suppose:
- Cache access time = 5 ns
- Main memory time = 50 ns
- Hit ratio = 95%

$$T_{avg} = T_c + (1-H)T_m = 5 + (1 - 0.95)(50) = 5 + 2.5 = 7.5 \text{ ns}$$

---

## 3. How to Improve Cache Performance?

### ① Increase Cache Size

Larger cache can store more data.

$$\text{Larger cache} \rightarrow \text{fewer capacity misses}$$

Therefore hit ratio generally increases. But a very large cache can have a longer access time.

### ② Increase Block Size

Suppose the CPU accesses:

```
100
101
102
103
```

If block 100 is loaded along with 100, 101, 102, 103, then future accesses may become hits. This is called **spatial locality**.

But excessively large blocks are bad because fewer blocks can fit into the cache.

---

## 4. Locality of Reference

Cache works mainly because programs show **locality of reference**.

### Temporal Locality

If something was recently used, it is likely to be used again.

**Example:**

```c
for (i = 0; i < 100; i++)
    sum += a[i];
```

The loop instructions are repeatedly used.

### Spatial Locality

If one memory location is accessed, nearby locations are likely to be accessed soon.

**Example:**

```
Array:
A[0]
A[1]
A[2]
A[3]
A[4]
```

After accessing A[0], A[1] and A[2] may be accessed soon.

---

## 5. Replacement Policies

When the cache is full, something must be removed. Common policies include:

### FIFO — First In, First Out

Remove the block that entered first.

```
Oldest → Remove
```

### LRU — Least Recently Used

Remove the block that has not been used for the longest time.

```
Recently used       → Keep
Least recently used → Remove
```

LRU often performs well because it exploits temporal locality.

---

## 🎯 Final Revision Sheet

```
CACHE
│
├── Hit
│    └── Data found in cache
│
├── Miss
│    └── Data not found → Main Memory
│
├── Hit Ratio
│    └── Hits / Total Accesses
│
├── Miss Ratio
│    └── 1 - Hit Ratio
│
└── Mapping
     │
     ├── Direct
     │    └── One block → One line
     │
     ├── Fully Associative
     │    └── One block → Any line
     │
     └── Set Associative
          └── One block → One set
                       → Any line in that set
```

### ⭐ Formulas to Memorize

| Formula | Meaning |
|---|---|
| $i = j \bmod m$ | Direct mapping |
| $i = j \bmod v$ | Set-associative mapping |
| $H = \dfrac{\text{Hits}}{\text{Total accesses}}$ | Hit ratio |
| $M = 1 - H$ | Miss ratio |
| $T_{avg} = T_c + (1-H)T_m$ | Simplified average access time |

**One-line memory trick:**

> Direct = fixed place, Associative = anywhere, Set-associative = anywhere inside one set.

---

*See also: [Cache Memory Basics](01-Cache-Memory-Basics.md), [Direct Mapping](02-Direct-Mapping.md), [Fully Associative Mapping](03-Fully-Associative-Mapping.md), [Set-Associative Mapping](04-Set-Associative-Mapping.md)*