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
