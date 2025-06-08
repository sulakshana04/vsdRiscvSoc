# Objective
# To enable the machine-timer interrupt (MTIP) and write a simple handler in C

# What is the Machine Timer Interrupt (MTIP)?
# The Machine Timer Interrupt (MTIP) is a fundamental interrupt in the RISC-V privileged architecture. It is triggered by the machine timer, which uses two special memory-mapped registers:

# mtime: A continuously incrementing 64-bit timer register representing the current time.
# mtimecmp: A 64-bit comparator register. When mtime equals or exceeds mtimecmp, the machine timer interrupt is triggered.
# These registers are usually implemented in the CLINT (Core Local Interruptor) hardware block of the RISC-V system. 

//MTIP handler in C










#include <stdint.h>
#include <stddef.h>

#define UART_BASE        0x10000000
#define MSTATUS_MIE      (1 << 3)
#define MIE_MTIE         (1 << 7)
#define MTIMECMP_DELAY   500000

#define CLINT_MTIME      (*(volatile uint64_t *)(0x200bff8))
#define CLINT_MTIMECMP   (*(volatile uint64_t *)(0x2004000))

// UART output helper
void uart_puts(const char *s) {
    volatile char *uart = (volatile char *)UART_BASE;
    while (*s) {
        *uart = *s++;
    }
}
// Timer interrupt handler
volatile int count = 0;

void timer_isr(void) {
    if (count < 5) {
        uart_puts(">> Timer Interrupt Triggered\n");
        count++;
        CLINT_MTIMECMP = CLINT_MTIME + MTIMECMP_DELAY;
    }
}
void main(void) {
    uart_puts("== Timer Interrupt Example ==\n");

    timer_isr();  // Initial test call

    // Set mtvec to point to the trap handler
    extern void trap_handler(void);
    uintptr_t trap_addr = (uintptr_t)&trap_handler;
    asm volatile("csrw mtvec, %0" :: "r"(trap_addr));

    // Set first timer interrupt
    CLINT_MTIMECMP = CLINT_MTIME + MTIMECMP_DELAY;

    // Enable machine timer interrupt and global interrupt
    asm volatile("csrs mie, %0" :: "r"(MIE_MTIE));
    asm volatile("csrs mstatus, %0" :: "r"(MSTATUS_MIE));

    while (1) {
        asm volatile("wfi");
    }
}
