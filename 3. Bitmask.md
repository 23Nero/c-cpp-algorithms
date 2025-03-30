# Bitmask in C/C++

## Introduction
Bitmask is a technique used to store and manipulate flags or states using bits. It allows setting, clearing, and checking specific bits in a word efficiently. Bitmask is commonly used for memory optimization, performing logical operations on bit groups, and managing states, access permissions, or other properties of an object.

## Bitwise Operations
### NOT Bitwise
Performs a bitwise NOT operation, flipping all bits in a number.
```c
int result = ~num;
```

### AND Bitwise
Performs a bitwise AND operation between corresponding bits of two numbers.
```c
int result = num1 & num2;
```

### OR Bitwise
Performs a bitwise OR operation between corresponding bits of two numbers.
```c
int result = num1 | num2;
```

### XOR Bitwise
Performs a bitwise XOR operation between corresponding bits of two numbers.
```c
int result = num1 ^ num2;
```

### Shift Left and Shift Right Bitwise
Shifts bits left or right by a specified amount.
```c
int resultLeftShift = num << shiftAmount;
int resultRightShift = num >> shiftAmount;
```

## Example: Feature Management Using Bitmask
This example demonstrates how to enable, disable, and check features using bitmask.
```c
#include <stdio.h>
#include <stdint.h>

#define GENDER 1 << 0  // Bit 0: Gender (0 = Female, 1 = Male)
#define TSHIRT 1 << 1  // Bit 1: T-Shirt (0 = No, 1 = Yes)
#define HAT 1 << 2     // Bit 2: Hat (0 = No, 1 = Yes)
#define SHOES 1 << 3   // Bit 3: Shoes (0 = No, 1 = Yes)

void enableFeature(uint8_t *features, uint8_t feature) {
    *features |= feature;
}

void disableFeature(uint8_t *features, uint8_t feature) {
    *features &= ~feature;
}

int isFeatureEnabled(uint8_t features, uint8_t feature) {
    return (features & feature) != 0;
}

int main() {
    uint8_t options = 0;
    enableFeature(&options, TSHIRT | SHOES);
    printf("T-Shirt enabled: %d\n", isFeatureEnabled(options, TSHIRT));
    return 0;
}
```

## Example: LED Control Using Bitmask
This example controls LEDs using bitmask operations.
```c
#include <stdio.h>

#define LED1 1 << 0  // 0001
#define LED2 1 << 1  // 0010
#define LED3 1 << 2  // 0100
#define LED4 1 << 3  // 1000

void enableLED(unsigned int *GPIO_PORT, unsigned int LED) {
    *GPIO_PORT |= LED;
}

void disableLED(unsigned int *GPIO_PORT, unsigned int LED) {
    *GPIO_PORT &= ~LED;
}

int main() {
    unsigned int GPIO_PORT = 0;
    enableLED(&GPIO_PORT, LED1 | LED3);
    if (GPIO_PORT & LED1) printf("LED1 is on\n");
    if (GPIO_PORT & LED3) printf("LED3 is on\n");
    return 0;
}
```

## Example: Using Bit Fields for LED Control
Bit fields can be used to store LED states efficiently.
```c
#include <stdio.h>
#include <stdint.h>
#define ENABLE 1
#define DISABLE 0

typedef struct {
    uint8_t LED1 : 1;
    uint8_t LED2 : 1;
    uint8_t LED3 : 1;
    uint8_t LED4 : 1;
    uint8_t LED5 : 1;
    uint8_t LED6 : 1;
    uint8_t LED7 : 1;
    uint8_t LED8 : 1;
} LEDStatus;

void displayAllStatusLed(LEDStatus status) {
    uint8_t* statusPtr = (uint8_t*)&status;
    for (int j = 0; j < 8; j++) {
        printf("LED%d: %d\n", j+1, (*statusPtr >> j) & 1);
    }
}

int main() {
    LEDStatus ledStatus = { .LED7 = ENABLE, .LED5 = ENABLE };
    ledStatus.LED1 = ENABLE;
    ledStatus.LED3 = ENABLE;
    displayAllStatusLed(ledStatus);
    return 0;
}
```

## Example: Car Options Using Bitmask
This example manages car configurations using bitmask.
```c
#include <stdio.h>
#include <stdint.h>

#define COLOR_RED 0
#define COLOR_BLUE 1
#define COLOR_BLACK 2
#define COLOR_WHITE 3
#define POWER_100HP 0
#define POWER_150HP 1
#define POWER_200HP 2
#define ENGINE_1_5L 0
#define ENGINE_2_0L 1

#define SUNROOF_MASK 1 << 0
#define PREMIUM_AUDIO_MASK 1 << 1
#define SPORTS_PACKAGE_MASK 1 << 2

typedef struct {
    uint8_t additionalOptions : 3;
    uint8_t color : 2;
    uint8_t power : 2;
    uint8_t engine : 1;
} CarOptions;
```
