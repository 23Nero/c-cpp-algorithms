# Pointers in C

## What is a Pointer?
In the C programming language, a pointer is a variable that stores the memory address of another object (variable, array, or function). Using pointers allows us to manipulate memory efficiently and flexibly.

## Declaring a Pointer
```c
int *ptr_int;   // Pointer to an integer
char *ptr_char; // Pointer to a character
float *ptr_float; // Pointer to a float
```

## Getting the Address of a Variable
```c
int x = 10;
int *ptr_x = &x; // ptr_x holds the address of x
```

## Dereferencing a Pointer
```c
int y = *ptr_x; // y gets the value stored at ptr_x (value of x)
ptr_x = &x;
*ptr_x = *(0x01) = 10;
```

## Pointer Size
Pointer size depends on the system architecture and compiler. For example:
```c
#include <stdio.h>
int main()
{
    printf("Size of pointer: %d bytes\n", sizeof(int*));
    return 0;
}
```

## Swapping Values Using Pointers
```c
#include <stdio.h>
void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

int main()
{
    int a = 10, b = 20;
    swap(&a, &b);
    printf("Value of a: %d\n", a);
    printf("Value of b: %d\n", b);
    return 0;
}
```

## Void Pointer
A void pointer can point to any data type.
```c
#include <stdio.h>
int main()
{
    int value = 5;
    double test = 15.7;
    char letter = 'A';

    void *ptr = &value;
    printf("Value: %d\n", *(int*)(ptr));
    ptr = &test;
    printf("Value: %f\n", *(double*)(ptr));
    ptr = &letter;
    printf("Value: %c\n", *(char*)(ptr));
    return 0;
}
```

## Function Pointers
A function pointer stores the address of a function and allows calling functions dynamically.
```c
#include <stdio.h>
void greetEnglish() { printf("Hello!\n"); }
void greetFrench() { printf("Bonjour!\n"); }

int main()
{
    void (*ptrToGreet)();
    ptrToGreet = greetEnglish;
    ptrToGreet(); // Output: Hello!
    ptrToGreet = greetFrench;
    (*ptrToGreet)(); // Output: Bonjour!
    return 0;
}
```

## Pointer to Constant
A pointer that cannot modify the value it points to.
```c
int const *ptr_const;
const int *ptr_const;
```
Example:
```c
#include <stdio.h>
int main()
{
    int value = 5;
    int const *ptr_const = &value;
    printf("Value: %d\n", *ptr_const);
    return 0;
}
```

## Constant Pointer
A pointer that cannot point to another address after initialization.
```c
#include <stdio.h>
int main()
{
    int value = 5;
    int *const const_ptr = &value;
    printf("Value: %d\n", *const_ptr);
    *const_ptr = 7; // Allowed
    printf("Value: %d\n", *const_ptr);
    return 0;
}
```

## Pointer to Pointer
A pointer that stores the address of another pointer.
```c
#include <stdio.h>
int main()
{
    int value = 42;
    int *ptr1 = &value;
    int **ptr2 = &ptr1;
    printf("Address of value: %p\n", &value);
    printf("Value of ptr1: %p\n", ptr1);
    printf("Value of ptr2: %p\n", ptr2);
    printf("Dereference ptr2 first time: %p\n", *ptr2);
    printf("Dereference ptr2 second time: %d\n", **ptr2);
    return 0;
}
```

## NULL Pointer
A pointer that does not point to any memory address.
```c
#include <stdio.h>
int main()
{
    int *ptr = NULL;
    if (ptr == NULL)
    {
        printf("Pointer is NULL\n");
    }
    return 0;
}
```

## Summary
- Definition and syntax of pointers
- Pointer dereferencing
- Pointer size
- Different pointer types and their usage

## Bubble Sort Using Pointers
Bubble Sort algorithm sorts an array by repeatedly swapping adjacent elements if they are in the wrong order.
```c
#include <stdio.h>
void bubbleSort(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main()
{
    int arr[] = {5, 3, 8, 6, 2, -3};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    for (int i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

