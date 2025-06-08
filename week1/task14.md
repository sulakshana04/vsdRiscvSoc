# Task 14: rv32imac vs rv32imc – What’s the “A”?

## Objective
To explain the ‘A’ (atomic) extension in rv32imac. What instructions are added and why are they useful?

## Concept 
* The __‘A’ extension__ stands for Atomic instructions in the RISC-V ISA, making the difference between rv32imc (integer, multiply, compressed) and rv32imac (integer, multiply, atomic, compressed).
* It adds atomic memory operations such as:
  
__lr.w__ (Load-Reserved Word)

__sc.w__ (Store-Conditional Word)

__amoadd.w__ (Atomic Memory Operation: Add Word)
And other atomic operations like amoswap.w, amoxor.w, amoand.w, amoor.w, amomin.w, amomax.w, etc.
* These instructions allow __atomic read-modify-write sequences__ on memory locations without interruption, which is crucial for:
Implementing __lock-free data structures__ (queues, stacks)

Writing __OS kernels and synchronization primitives__ (mutexes, spinlocks, semaphores)

Ensuring __safe concurrency__ on multi-core or multi-threaded processors
* Without these atomic instructions, software would need to disable interrupts or use heavier synchronization methods, which impact performance and scalability.

