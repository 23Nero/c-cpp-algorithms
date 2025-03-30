# STDARG and ASSERT

## 1. The `stdarg.h` Library

The `stdarg.h` library provides methods for handling functions with a variable number of input parameters. Common examples include `printf` and `scanf`.

### Key Functions in `stdarg.h`
- **`va_list`**: A data type that represents a list of variable arguments.
- **`va_start(va_list, lastFixedArg)`**: Initializes the argument list. Must be called before accessing the arguments.
- **`va_arg(va_list, type)`**: Retrieves the next argument in the list.
- **`va_end(va_list)`**: Ends the usage of the argument list. Must be called before the function terminates.
- **`va_copy(va_list dest, va_list src)`**: Copies data between two `va_list` variables.

### Example 1: Displaying Variable Arguments
```c
#include <stdio.h>
#include <stdarg.h>

void display(int count, ...) {
    va_list args;
    va_start(args, count);

    for (int i = 0; i < count; i++) {
        printf("Value at %d: %d\n", i, va_arg(args, int));
    }
    va_end(args);
}

int main() {
    display(5, 5, 8, 15, 10, 13);
    return 0;
}
```

### Example 2: Summing Variable Arguments
```c
#include <stdio.h>
#include <stdarg.h>

int sum(int count, ...) {
    va_list args;
    va_start(args, count);
    int result = 0;

    for (int i = 0; i < count; i++) {
        result += va_arg(args, int);
    }
    va_end(args);
    return result;
}

int main() {
    printf("Sum: %d\n", sum(4, 1, 2, 3, 4));
    return 0;
}
```

### Example 3: Passing Struct Data
```c
#include <stdio.h>
#include <stdarg.h>

typedef struct {
    int x;
    double y;
} Data;

void display(int count, ...) {
    va_list args;
    va_start(args, count);

    for (int i = 0; i < count; i++) {
        Data tmp = va_arg(args, Data);
        printf("Data.x at %d is: %d\n", i, tmp.x);
        printf("Data.y at %d is: %f\n", i, tmp.y);
    }
    va_end(args);
}

int main() {
    display(3, (Data){2, 5.0}, (Data){10, 57.0}, (Data){29, 36.0});
    return 0;
}
```

### Example 4: Handling Different Sensor Types
```c
#include <stdio.h>
#include <stdarg.h>

typedef enum {
    TEMPERATURE_SENSOR,
    PRESSURE_SENSOR
} SensorType;

void processSensorData(SensorType type, ...) {
    va_list args;
    va_start(args, type);
    
    switch (type) {
        case TEMPERATURE_SENSOR: {
            int numArgs = va_arg(args, int);
            int sensorId = va_arg(args, int);
            float temperature = va_arg(args, double); // float is promoted to double
            printf("Temperature Sensor ID: %d, Reading: %.2f degrees\n", sensorId, temperature);
            if (numArgs > 2) {
                char* additionalInfo = va_arg(args, char*);
                printf("Additional Info: %s\n", additionalInfo);
            }
            break;
        }
        case PRESSURE_SENSOR: {
            int numArgs = va_arg(args, int);
            int sensorId = va_arg(args, int);
            int pressure = va_arg(args, int);
            printf("Pressure Sensor ID: %d, Reading: %d Pa\n", sensorId, pressure);
            if (numArgs > 2) {
                char* unit = va_arg(args, char*);
                printf("Unit: %s\n", unit);
            }
            break;
        }
    }
    va_end(args);
}
```

---
## 2. The `assert.h` Library

The `assert.h` library provides the `assert` macro, which checks conditions at runtime. If the condition evaluates to `false`, the program terminates and displays an error message. It is commonly used for debugging.

### Using `assert`
```c
#include <stdio.h>
#include <assert.h>

int main() {
    int x = 5;
    assert(x == 5);
    printf("X is: %d", x);
    return 0;
}
```

### Common Use Cases
1. **Detecting Out-of-Bounds Array Access**
2. **Preventing Division by Zero**
3. **Ensuring Type Safety in Functions**

### Example: Debugging with `assert`
```c
#include <assert.h>
#define LOG(condition, cmd) assert(condition && #cmd)
```

### Example: Ensuring Values are Within a Range
```c
#include <assert.h>
#define ASSERT_IN_RANGE(val, min, max) assert((val) >= (min) && (val) <= (max))

void setLevel(int level) {
    ASSERT_IN_RANGE(level, 1, 10);
    // Set the level
}
```

### Example: Checking Data Type Sizes
```c
#include <assert.h>
#include <stdint.h>
#define ASSERT_SIZE(type, size) assert(sizeof(type) == (size))

void checkTypeSizes() {
    ASSERT_SIZE(int, 4);
    // Check other data types
}
```

## Conclusion
- `stdarg.h` is essential for handling functions with variable argument lists.
- `assert.h` is useful for debugging and ensuring runtime constraints.
- These libraries help write more flexible and reliable C programs.

---
Let me know if you need further explanations or modifications!

