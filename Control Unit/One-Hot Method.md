The one-hot method is a technique for representing the states of a control unit.
 
Suppose a controller has 4 states: S0, S1, S2, S3.
 
In one-hot encoding, we use **one flip-flop for each state**.
 
```
S0 → 1000
S1 → 0100
S2 → 0010
S3 → 0001
```
 
Only one bit is 1 at a time. That's why it is called **One-Hot**.
 
---
 
## 8. One-Hot Diagram
 
```
             ┌─────┐
Clock ──────►│ FF0 │──► S0
             └─────┘
 
             ┌─────┐
Clock ──────►│ FF1 │──► S1
             └─────┘
 
             ┌─────┐
Clock ──────►│ FF2 │──► S2
             └─────┘
 
             ┌─────┐
Clock ──────►│ FF3 │──► S3
             └─────┘
```
 
Example — current state = S2:
 
```
FF0 = 0
FF1 = 0
FF2 = 1  ← active
FF3 = 0
```
 
---
 
## 9. Why Use One-Hot Encoding?
 
In ordinary binary encoding, several bits must be decoded.
 
For example, 4 states require 2 bits:
 
```
S0 = 00
S1 = 01
S2 = 10
S3 = 11
```
 
A decoder is needed to determine which state is active.
 
With one-hot:
 
```
S0 = 1000
S1 = 0100
S2 = 0010
S3 = 0001
```
 
The state is immediately obvious.
 
### Advantages
- Simple state decoding
- Simple control logic
- Fast state transitions
### Disadvantage
- Requires more flip-flops
### ⭐ Exam answer
 
> In the one-hot method, each state is represented by a separate flip-flop, and only one flip-flop is set to 1 at any time. It simplifies decoding and control logic but requires more hardware.
 
---
 
## 10. GCD Controller
 
GCD = Greatest Common Divisor
 
Example:
 
```
GCD(12, 8) = 4
```
 
A simple GCD algorithm:
 
```
If A > B:
    A = A - B
Else if B > A:
    B = B - A
Else:
    GCD = A
```
 
For A = 12, B = 8:
 
```
12 > 8  →  A = 12 - 8 = 4
B > A   →  B = 8 - 4 = 4
A = B   →  GCD = 4
```
 
---
 
## 11. GCD Controller as States
 
A controller can represent the algorithm using states — this is basically a **Finite State Machine (FSM)**.
 
```
              START
                │
                ▼
             LOAD A,B
                │
                ▼
             COMPARE
            /    |    \
           /     |     \
       A > B    A = B   B > A
          │       │        │
          ▼       ▼        ▼
       A=A-B    DONE     B=B-A
          │                │
          └──────┬─────────┘
                 │
                 ▼
              COMPARE
```
 
---
 
## 12. Classical Binary vs One-Hot GCD Controller
 
### Binary method
 
Suppose we have 8 states. Number of flip-flops required:
 
$$\lceil \log_2 8 \rceil = 3$$
 
So: 3 flip-flops → 8 possible states. But a decoder is required.
 
### One-hot method
 
For 8 states: 8 states → 8 flip-flops. But no complicated state decoder is needed.
 
### Comparison
 
| Binary | One-Hot |
|---|---|
| Fewer flip-flops | More flip-flops |
| Needs decoding | Little/no state decoding |
| More compact | Simpler control logic |
| More complex logic | Simpler logic |
 
---