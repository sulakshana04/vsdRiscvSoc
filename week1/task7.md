# Task7: Running Under an Emulator
This task demonstrates how to boot a bare-metal ELF and print to the UART console using QEMU.

## Step1: Install qemu
```
sudo apt update
sudo apt install qemu-system-misc
```
## Step 2: Run ELF:
```
qemu-system-riscv32 -nographic -kernel hello.elf
```
qemu-system-riscv32: Full system emulation for RISC-V 32-bit
-nographic: Disables graphical output, redirects console to terminal
-kernel hello_bm.elf: Loads ELF as kernel image for bare-metal execution


file:///home/sulakshana/Pictures/Screenshots/task7.png![image](https://github.com/user-attachments/assets/40b53325-2d16-4be2-9b15-704d641ba3ab)
