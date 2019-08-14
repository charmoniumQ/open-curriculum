# How C/C++ programs work

## Memory

[Reading](https://www.geeksforgeeks.org/memory-layout-of-c-program/)

```C

#include <stdio.h>

int global = 34; // stored on data
int another_global = 0; // stored on uninitialized data

int main() {
    int i = 0; // stored on stack
    int* ptr = malloc(sizeof(int)); // address stored on stack
    *ptr = 123; // value '123' is stored in heap
    printf("%d", factorial(5));
    return 0;
}
```

1. Which segments do you always know the size of at compile-time? Why can't you figure out the size of the others?
2. Suppose you want to run two copies of a program with different inputs on the same processor. Which segments can be shared? Which ones have to be copied? Does the copy-(only)-on-write optimization apply?

## The stack

Function storage.

Goes arbitrarily 'deep' into functions that call functions that call functions...

"stack trace" = which functions got called (can tell by looking at stack)

1. If each function has a constant size at compile-time, why is the stack's size non-deterministic?

## Heap

Allocations not constant at runtime.

Doesn't have to be laid out this way;

malloc(n * sizeof(byte)); // give me n bytes. I don't care where

In C, always use a 'unit' (sizeof(SomeType))

In C++, always use new.

## Linking

[Reading](https://www.lurklurk.org/linkers/linkers.html)
