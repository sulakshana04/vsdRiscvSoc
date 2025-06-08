# Task-2: Compile "Hello, RISC-V"

## step1: Create project directory
```
mkdir -p ~/riscv-project/week1
cd ~/riscv-project/week1
```
## step2: write a hello world code
```
nano hello.c
```
Paste the following code into hello.c:

```
#include <stdio.h>

int main() {
    printf("Hello, RISC-V!\n");
    return 0;
}
```
## step3: compile the hello world code 
```
riscv32-unknown-elf-gcc -o hello.elf hello.c
```
## step4: verify
```
file hello.elf
```
file:///home/sulakshana/Pictures/Screenshots/task2.png![image](https://github.com/user-attachments/assets/b8412eb2-5f07-4601-a597-0e7392c251b2)

