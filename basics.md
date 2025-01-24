# C Basics - Assuming C++ Knowledge

## Variables 

```c
type name = value;
// Example
int val = 0;
```

## Scope & Preprocessor Directives
```c

#include <stdio.h>

// Macros
#define MAX_PERSONS 1024
#define DEBUG

// Global Scope 
int global = 1;

int main() {
    // Local Scope

    int val = 0;
    printf("val is %d",val);
    {
        // Sub-scope
        int val = 1;
        printf("val is %d",val);
    }
    printf("val is %d",val);

    #ifdef DEBUG
    printf("We are in DEBUG mode");
    #endif
    return 0;
}
```

Other preprocessor directives like #undef, #ifndef, #elif, #else, #endif, #error, #pragma, #line and #warning will probably be introduced later.

## Arrays & Strings

String and arrays are the same as in C++. Always remember to terminate strings (character arrays) with the zero byte

```c
#include <stdio.h>

#define MAX_IDS 32
#define STRING

int main() {
    int ids[MAX_IDS]; // type name[SIZE] = {val1,val2,...valSIZE-1};

    for (int i = 0; i < MAX_IDS; i++) {
        ids[i] = i + 1;
    }

    // Strings must be terminated by 0
    char mystr[] = {'h', 'e', 'l', 'l', 'o', 0};

    #ifdef STRING
    printf("%s\n", mystr);
    #endif
    printf("0 - %d\n10 - %d\n", ids[0], ids[10]);
    return 0;
}
```

## Conditional Statements

Same as C++

## Loops

Same as C++ (if, while, do-while)

## Functions

Similar structure to C
```c
type function(type arg, ... type argn);
```

**Unlike C++, C does not support funciton overloading**

## Structures

```c
struct mystruct {
    int i;
    char c;
};

int main() {
    // We are able to create an array of structures
    struct mystruct data[10];
```

## Unions

```c
union myunion {
    int i; // 4 bytes
    char c; // 1 byte
}
``` 

Unions are similar to structures, but instead of storing all of the members declared, unions have size of the *largest* data type where memory is reused for each member.

## Struct modifications
```c
struct __attribute__((__packed__)) mystruct {
    int i;
    char c;
}
```

We expect this structure to require 5 bytes, however, this may not be the case on all systems. By adding the packed attribute, we can ensure the compiler doesn't add any additional padding memory.

## Pointers
Very similar to C++.
```c
int x = 3;
int *pX = &x; // & Address, *pointer/dereference operator
```

## Dynamic Memory Allocation

Core concept is we want to allocate memory at runtime instead of compile time. Todo this, we use the
```c
malloc();
```

function. Remember to use
```c
free();
```
on the created object and set the object to NULL.

## Static Memory Allocation

Static variables retain their value between function calls and are initialized only once when the program starts like global variables but unlike global variable have limited scope.

```c
static int test = 0;
```

## Double pointers

Double pointers hold the address to/of a pointer. The main usecase presented is when you need to perform allocation/resizing of dynamic memory in a function in which case you would want to pass in a double pointer to the memory.

```c
int resize(int **p);
```

## Testing for Memory Leaks

Memory leaks occur when we don't free memory that we allocate. To do this, we need to compile our code with debug symbols enabled. Example:
```console
gcc code.c -g
```
And to test the code
```console
valgrind --leak-check=full ./a.out
```

