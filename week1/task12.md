# Task 12: Start-up Code & crt0

crt0 stands for C runtime 0. In a typical bare-metal RISC-V program, there is no operating system to initialize the system before our main code runs.

So, we use a startup assembly file (crt0.s) that sets up the basic runtime environment for our code. It is the first code that runs after reset.

## Where can we get one?
* We can write our own based on the example below
* Or we can use one from:
Newlib
riscv-pk (proxy kernel)
Minimal RISC-V templates by SiFive
Embedded frameworks like RIOT OS, Zephyr RTOS, etc.

```
.section .text
.globl _start

_start:
    # Set up stack pointer (end of SRAM)
    la sp, _stack_top

    # Clear .bss section
    la a0, __bss_start
    la a1, __bss_end
    li a2, 0
bss_clear:
    bge a0, a1, bss_done
    sw a2, 0(a0)
    addi a0, a0, 4
    j bss_clear
bss_done:

    # Copy .data section from Flash to RAM
    la a0, _data_lma      # load memory address (Flash)
    la a1, _data_start    # virtual memory address (RAM)
    la a2, _data_end
copy_data:
    bge a1, a2, data_done
    lw t0, 0(a0)
    sw t0, 0(a1)
    addi a0, a0, 4
    addi a1, a1, 4
    j copy_data
data_done:

    # Call main
    call main

hang:
    j hang  # Loop forever
```

## Linker Script 
```
ENTRY(_start)

MEMORY
{
    FLASH (rx)  : ORIGIN = 0x00000000, LENGTH = 512K
    SRAM  (rwx) : ORIGIN = 0x10000000, LENGTH = 64K
}

SECTIONS
{
    .text : {
        *(.text*)
        *(.rodata*)
    } > FLASH

    .data : AT (ADDR(.text) + SIZEOF(.text)) {
        _data_lma = LOADADDR(.data);
        _data_start = .;
        *(.data*)
        _data_end = .;
    } > SRAM

    .bss : {
        __bss_start = .;
        *(.bss*)
        *(COMMON)
        __bss_end = .;
    } > SRAM

    .stack (NOLOAD) : {
        . = ALIGN(4);
        _stack_top = . + 0x1000;  /* 4KB stack */
    } > SRAM
}
```
