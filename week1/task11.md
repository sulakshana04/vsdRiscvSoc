# Task-11: Linker Script 101

To create a minimal linker script that places .text at 0x00000000 and .data at 0x10000000 for RV32IMC.

# Linker Script
```
ENTRY(_start)

SECTIONS
{
  /* Code section (flash) */
  .text 0x00000000 : {
    *(.text*)
    *(.rodata*)     /* Include read-only data like string literals */
  }

  /* Initialized data section (RAM) */
  .data 0x10000000 : {
    *(.data*)
  }

  /* Uninitialized data (BSS) */
  .bss (ALIGN(4)) : {
    *(.bss*)
    *(COMMON)
  }
}
```
## Explanation
```
ENTRY(_start)
```
Tells the linker to begin execution at the _start symbol (your program’s entry point, typically in assembly or C).

```
.text 0x00000000
```
Puts all code (.text*) and read-only data (.rodata*) starting at 0x00000000.

This is typically your flash memory or ROM.
```
.data 0x10000000
```
Initialized data (like global variables with initial values) starts at 0x10000000, assumed to be RAM.

```
.bss
```
This is for uninitialized global/static variables (they are zero-initialized at runtime).

It follows the .data section and is 4-byte aligned for safe access.
