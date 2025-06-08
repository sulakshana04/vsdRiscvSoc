# Task-4: Hex Dump & Disassembly
In this task, we are expected to convert our ELF file into raw hex format and also disassemble it for analysis.

## Step1: Convert to Hex
```
riscv32-unknown-elf-objcopy -O ihex hello.elf hello.hex
```

![image](https://github.com/user-attachments/assets/bd3a67cf-3bb0-438b-a8a3-3e0937141f0a)

## Step 2: Disassemble
```
riscv32-unknown-elf-objdump -d hello.elf > hello.dump
cat hello.dump

```
file:///home/sulakshana/Pictures/Screenshots/task4.png![image](https://github.com/user-attachments/assets/49dc6de6-0751-44c5-b60d-2cc081934cc9)


