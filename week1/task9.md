# Task-9: Inline Assembly Basics
We have to write a c program that reads the cycle count of RISCV cycle counter using CSR (control status and register) using inline assembly

## Step 1: Write c code
```
vim read_cycle.c

unsigned int read_cycle() {
     unsigned int cycle;
     asm volatile("csrr %0, cycle": "=r"(cycle));
     return cycle;
}
```
## Generation of assembly
```
riscv32-unknown-elf-gcc -o read_cycle.s -S read_cycle.c
```
![image](https://github.com/user-attachments/assets/1a344856-bae8-4e21-8fc6-90e5231dc42b)

* asm volatile(...)

This tells the compiler to insert inline assembly into the C code.
asm: keyword for GCC-style inline assembly.
volatile: tells the compiler not to optimize away or reorder this assembly instruction.
Without volatile, the compiler might remove or move this line if it thinks it has no side effects (since the output c is not guaranteed to be used immediately).

* "csrr %0, cycle"

This is the RISC-V assembly instruction that reads the cycle CSR (0xC00).
csrr: Control and Status Register Read instruction
%0: placeholder for the first output operand (in this case, c)
It tells the assembler: “substitute this with a register that will hold the output.”

* "=r"(c)

This is the output operand constraint, which tells the compiler:
=: This is write-only (output-only). The value of c is written by the instruction.
r: Use a general-purpose register to hold the value of the cycle.
(c): Bind this output to the C variable c.
