# Garbage Collector for C

## Overview
This project provides a simple garbage collector for C programs. Instead of manually tracking and freeing allocated memory, this garbage collector manages all memory allocations automatically. It provides a wrapper function `ft_malloc()` that behaves like `malloc()`, and a function `free_garbage()` that frees all allocated memory at the end of the program.

## Usage

### 1. Include the Header File
```c
#include "ft_malloc.h"
```

### 2. Replace `malloc()` with `ft_malloc()`
Instead of using `malloc()`, use `ft_malloc()` to allocate memory:
```c
int *ptr = (int *)ft_malloc(sizeof(int) * 10);
```
This function works just like `malloc()`, but the allocated memory is automatically managed by the garbage collector.

### 3. Free All Allocated Memory
At the end of your program, call `free_garbage()` to free all allocated memory:
```c
free_garbage();
```
This function will release all memory allocated by `ft_malloc()`.

## Example
```c
#include "ft_malloc.h"
#include <stdio.h>

int main() {
    int *arr = (int *)ft_malloc(sizeof(int) * 5);
    if (!arr) {
        perror("ft_malloc failed");
        return 1;
    }
    
    for (int i = 0; i < 5; i++)
        arr[i] = i * 10;
    
    for (int i = 0; i < 5; i++)
        printf("%d ", arr[i]);
    
    printf("\n");
    free_garbage(); // Free all allocated memory
    return 0;
}
```

## Benefits
- **No manual `free()` calls required** – prevents memory leaks.
- **Easy integration** – just replace `malloc()` with `ft_malloc()`.
- **Efficient memory management** – all memory is freed in one function call at the end of execution.

## Notes
- `ft_malloc.h` must be included in every source file that uses `ft_malloc()`.
- `free_garbage()` should be called only once at the end of the program to avoid undefined behavior.
- This garbage collector does not track individual deallocations; it only frees all allocated memory at once.
