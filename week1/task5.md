# Task-5: ABI & Register Cheat-Sheet
This is a complete list of the 32 integer registers in RISC-V RV32 architecture, with their:

Register numbers (x0 to x31)
ABI (Application Binary Interface) names
Typical role under the standard calling convention

![image](https://github.com/user-attachments/assets/8d2177c0-1eca-48e9-9019-a3fc69fa9e83)

## Calling Convention Summary
Caller-saved (t0–t6, a0–a7): Must be saved by the calling function if needed after a call.
Callee-saved (s0–s11): Must be preserved by the called function.
sp: Stack pointer — managed according to stack frame layout.
ra: Stores return address for function calls (jalr).
zero: Hardwired to 0 — always safe to read.

```
nano reg-cheatsheet.txt
```
file:///home/sulakshana/Pictures/Screenshots/task5.png![image](https://github.com/user-attachments/assets/13907f5e-72b1-4b5a-983a-1da6e89ac1e0)


file:///home/sulakshana/Pictures/Screenshots/task5b.png![image](https://github.com/user-attachments/assets/628b9e01-0f38-4cee-85e1-e56e9519ab92)
