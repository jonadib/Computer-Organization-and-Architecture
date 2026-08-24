# Cache Memory Basics

## 1. What is Cache Memory?

Cache memory is a small and very fast memory placed between the CPU and main memory. Its main purpose is to **reduce the time required by the CPU to access data**.

### Basic structure

```
             CPU
              │
              │ Fast access
              ▼
        ┌─────────────┐
        │   CACHE     │
        │ Small/Fast  │
        └──────┬──────┘
               │
               │ Slower
               ▼
        ┌─────────────┐
        │ Main Memory │
        │ Large/Slow  │
        └─────────────┘
```

### Why do we need cache?

CPU is much faster than main memory.

**Without cache:**

```
CPU → Main Memory → CPU
       ↑
     Slow
```

**With cache:**

```
CPU → Cache → CPU
      ↑
    Fast
```

If the required data is already in cache, the CPU gets it quickly.

---

## 2. Memory Hierarchy

Computer memory can be arranged according to speed, size, and cost.

```
             Faster
               ↑
        ┌─────────────┐
        │ Registers   │
        ├─────────────┤
        │ Cache       │
        ├─────────────┤
        │ Main Memory │
        ├─────────────┤
        │ SSD/HDD     │
        └─────────────┘
               ↓
             Larger
```

### General rule

**Going up:**
- Faster
- Smaller
- More expensive per bit

**Going down:**
- Slower
- Larger
- Cheaper per bit

---

## 3. What is a Cache Hit?

Suppose the CPU needs **Data X**.

**If X is already in cache → Cache Hit**

```
CPU
 ↓
Cache
 ↓
Data found ✓
```

**If X is not in cache → Cache Miss**

```
CPU
 ↓
Cache
 ↓
Not found ✗
 ↓
Main Memory
 ↓
Get data
 ↓
Cache
 ↓
CPU
```

---

## 4. Hit Ratio

Hit ratio tells us how many memory accesses are successfully served by the cache.

$$H = \frac{\text{Number of Cache Hits}}{\text{Total Memory Accesses}}$$

### Example

Suppose the CPU makes **1000** memory accesses, and the cache successfully handles **950** of them.

$$H = \frac{950}{1000} = 0.95$$

**H = 95%**

---

## 5. Miss Ratio

Miss ratio tells us how many accesses miss the cache.

$$\text{Miss Ratio} = 1 - H$$

If H = 95%:

$$\text{Miss Ratio} = 1 - 0.95 = 0.05 = 5\%$$

```
Hit ratio  = 95%
Miss ratio = 5%
```

---

## ⭐ Most Important Exam Definitions

**Cache Memory**
> Cache is a small, high-speed memory located between the CPU and main memory that stores frequently or recently used data and instructions.

**Cache Hit**
> A cache hit occurs when the requested data is found in the cache.

**Cache Miss**
> A cache miss occurs when the requested data is not found in the cache and must be obtained from a lower level of memory.

**Hit Ratio**

$$H = \frac{\text{Cache Hits}}{\text{Total Accesses}}$$

**Miss Ratio**

$$M = 1 - H$$

---

## Quick Numerical Example

**Question:** A cache has 1000 memory accesses and 900 hits. Find the hit and miss ratio.

**Solution:**

Hit ratio:

$$H = \frac{900}{1000} = 0.9 = 90\%$$

Miss ratio:

$$1 - H = 1 - 0.9 = 10\%$$

---

*See also: [Direct Mapping](02-Direct-Mapping.md), [Fully Associative Mapping](03-Fully-Associative-Mapping.md), [Set-Associative Mapping](04-Set-Associative-Mapping.md), [Cache Performance and Locality](05-Cache-Performance-and-Locality.md)*