# Task-10: Memory-Mapped I/O Demo
In this we are going to write a bare-metal c snippet to toggle a gpio register located at 0x10012000 and we'll also see how we can prevent the compiler from optimizting the store away.

## code
```
cat <<EOF > task10_gpio.c
#include <stdint.h>

int main() {
    volatile uint32_t *gpio = (uint32_t*)0x10012000;
    *gpio = 0x1;
    return 0;
}
EOF
```

## Explanation
* #define GPIO_ADDR 0x10012000 defines a macro that holds the gpio register address

* void toggle_gpio() - function declaration that returns nothing

* volatile uint32_t* gpio = (volatile uint32_t*)GPIO_ADDR;

(volatile uint32_t*) is typecasting the integer stored in GPIO_ADDR macro into a 32-bit unsigned integer data types whose value is volatile
volatile uint32_t* gpio declares a pointer to gpio of type unsigned integer of 32 bit whose data value is volatile. Note: The data that this pointer points to is volatile and not the pointer itself. In that case, the code would've been unint32_t* volatile gpio
*gpio ^= 0x1 toggles/flips the value stored in gpio pointer. The operation being performed here is read-modify-write. Here the value of gpio is first read, then it is toggled by doing XOR with 1 and then written back to it.

file:///home/sulakshana/Pictures/Screenshots/task10a.png![image](https://github.com/user-attachments/assets/a03421a5-dcd0-48b6-b7cc-16e98a412cc3)

file:///home/sulakshana/Pictures/Screenshots/task10b.png![image](https://github.com/user-attachments/assets/5ed3527f-b545-4a17-995e-a6b1532e2f00)
