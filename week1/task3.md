# Task-3: From C to Assembly
In this task, we will generate the assembly file for our simple C program and explain the meaning of prologue and epilogue.

## Step 1: Generate Assembly File
Use the following command to generate the assembly file:

```
riscv32-unknown-elf-gcc -S -O0 hello.c
```
or 

```
riscv32-unknown-elf-gcc -S -O0 -march=rv32imc -mabi=ilp32 hello.c -o hello.s
```
file:///home/sulakshana/Pictures/Screenshots/task3.png![image](https://github.com/user-attachments/assets/fda4da2c-04f5-443c-af11-ae1b23c3d973)


## Prologue 
The prologue is the code at the start of a function. It:

Allocates stack space
Saves callee-saved registers (like s0, ra)
Sets up the frame pointer (s0)

## Epilogue
The epilogue is the code at the end of the function. It:

Restores saved registers
Deallocates stack
Returns to the caller
