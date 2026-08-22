## Comparison of Three CPU Organizations

| Feature          | Accumulator | Stack                | Register        |
| ---------------- | ----------- | -------------------- | --------------- |
| Instruction      | 1-address   | 0-address            | 2/3-address     |
| Main storage     | Accumulator | Stack                | Registers       |
| Operand location | AC + memory | Top of stack         | Registers       |
| Example          | IAS         | Stack machines       | Modern CPUs     |
| Main advantage   | Simple      | Good for expressions | Fast & flexible |

## Super easy memory trick

**Accumulator → 1 address**
**Stack → 0 address**
**Register → 2/3 addresses**
