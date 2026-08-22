What is an Interrupt?

An interrupt is a signal that tells the CPU:

“Stop your current work for a moment and handle this important task.”

The CPU temporarily pauses the current program and executes a special routine called an Interrupt Service Routine (ISR).

After the ISR finishes, the CPU returns to the previous program and continues from where it stopped.

Simple Example: Keyboard
        Normal Program
              ↓
        CPU is working
              ↓

The external hardware must provide the information needed to identify the interrupt service operation.

11. Priority Order

This is very important for exams.

        TRAP
         ↓
      RST 7.5
         ↓
      RST 6.5
         ↓
      RST 5.5
         ↓
        INTR

Therefore:

TRAP>RST7.5>RST6.5>RST5.5>INTR
	​


Where > means higher priority than.

12. Complete Comparison Table
Interrupt	Hardware	Vectored	Maskable	Priority	Vector
TRAP	✓	✓	✗	1	0024H
RST 7.5	✓	✓	✓	2	003CH
RST 6.5	✓	✓	✓	3	0034H
RST 5.5	✓	✓	✓	4	002CH
INTR	✓	✗	✓	5	Non-vectored
13. Don't Confuse These Two Classifications

This is extremely important.

Vectored vs Non-Vectored asks:

“Does the CPU already know the ISR address?”

Vectored
→ Yes, address is fixed


Non-vectored
→ No, external hardware provides the information
Maskable vs Non-Maskable asks:

“Can the interrupt be disabled?”

Maskable
→ Yes, can be disabled


Non-maskable
→ No, cannot normally be disabled

So they are not the same classification.

14. Example of Combining Both
TRAP
TRAP
 │
 ├── Hardware ✓
 ├── Vectored ✓
 ├── Non-maskable ✓
 └── Highest priority ✓
RST 7.5
RST 7.5
 │
 ├── Hardware ✓
 ├── Vectored ✓
 ├── Maskable ✓
 └── 2nd priority
INTR
INTR
 │
 ├── Hardware ✓
 ├── Non-vectored ✓
 ├── Maskable ✓
 └── Lowest priority
⭐ 15. Super Easy Memory Trick

Just memorize these three:

TRAP

T = Top priority + Tough to disable

TRAP
→ Highest
→ Vectored
→ Non-maskable
→ 0024H
RST 7.5, 6.5, 5.5

All are Vectored + Maskable

RST 7.5 → 003CH
RST 6.5 → 0034H
RST 5.5 → 002CH
INTR

I = Lowest + external Information needed

INTR
→ Lowest
→ Non-vectored
→ Maskable
🎯 Exam-Oriented Final Answer

If a question asks "Discuss 8085 interrupts", you can write:

An interrupt is a signal that temporarily stops the current execution of the CPU and causes it to execute an Interrupt Service Routine (ISR). After servicing the interrupt, the CPU returns to the original program.

The 8085 has five hardware interrupts: TRAP, RST 7.5, RST 6.5, RST 5.5 and INTR. Their priority order is:

TRAP>RST7.5>RST6.5>RST5.5>INTR
	​


TRAP is the highest-priority, non-maskable and vectored interrupt. RST 7.5, RST 6.5 and RST 5.5 are maskable and vectored interrupts. INTR is the lowest-priority, maskable and non-vectored interrupt.

Vectored interrupts have predefined ISR addresses, whereas non-vectored interrupts require external hardware to provide the required information. Maskable interrupts can be disabled by software, whereas non-maskable interrupts cannot normally be disabled.

One-line revision:

TRAP = Highest + Vectored + Non-maskable
RST 7.5/6.5/5.5 = Vectored + Maskable
INTR = Lowest + Non-vectored + Maskable