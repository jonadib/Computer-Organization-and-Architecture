### Definition
 
A hardwired control unit generates control signals using physical electronic circuits such as:
 
- AND gates
- OR gates
- NOT gates
- Flip-flops
- Decoders
### Simple diagram
 
```
             Instruction
                 │
                 ▼
          ┌─────────────┐
          │ Instruction │
          │   Decoder   │
          └──────┬──────┘
                 │
                 ▼
          ┌─────────────┐
Clock ───►│ Control     │
Flags ───►│ Logic       │
          └──────┬──────┘
                 │
                 ▼
        Control Signals
```
 
### Easy example
 
Suppose the instruction is:
 
```
ADD R1, R2
```
 
The hardware control logic recognizes the instruction and generates:
 
```
R1out
R2out
ALU_ADD
R1in
```
 
### Advantages
- Very fast
- Good for simple instruction sets
- No control memory required
### Disadvantages
- Difficult to modify
- Difficult to design for complex CPUs
- Adding new instructions may require changing hardware
> **Exam sentence:** Hardwired control is fast but difficult to modify.
 
---