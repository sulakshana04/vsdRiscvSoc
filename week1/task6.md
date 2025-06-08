# Task-6: Stepping with GDB
we'll explore how we can run our elf file on a simulator (could be built in or external like qemu and spike) and also go through the debugging processing by using breakpoints and stepping.

## Step 1: Open GDB
```
riscv32-unknown-elf-gdb hello.elf
```

## Step 2: Inside GDB
```
(gdb) target sim
(gdb) break main
(gdb) run
(gdb) info reg a0
(gdb) disassemble
(gdb) quit
```
This simulates RISC-V CPU and shows instruction-level execution.
file:///home/sulakshana/Pictures/Screenshots/task6a.png![image](https://github.com/user-attachments/assets/ca0c6419-f8b7-454a-85e4-f99cb639ac4a)

## Info registers and disassemble
file:///home/sulakshana/Pictures/Screenshots/task6b![image](https://github.com/user-attachments/assets/1a723816-2a1d-48d9-963a-7e4d605412f4)
