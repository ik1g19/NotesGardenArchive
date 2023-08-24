---
title: C Heaps and Memory Errors
---
# Heap

The heap is a region of memory that is not managed automatically
Memory on the heap has to be allocated and released by the programmer
Memory in the heap is allocated through `malloc()` and released through `free()`

## malloc()

```C
void *malloc(size_t size);
```

Allocates a memory area of size `size` and returns a pointer to that area
Returns `NULL` in case of error while allocating memory

#### Example
```C
int* x = malloc(sizeof(int));  
int* array = malloc(N * sizeof(int)); // int array[N]
```

## free()

```C
void *free(void *ptr);
```

Release the memory area pointed to by `ptr`

#### Example
```C
int* x = malloc(sizeof(int));  
/*  ... body ...  */
free(x)
```

## Stack vs. Heap

```C
int foo() {  
int x;  
int* y = malloc(sizeof(int));  
/*...*/
}
```

`x` and `y` are allocated on the stack, but `y` contains memory that is allocated on the heap

## Advantages of the Heap

Variables in the heap can be accessed globally until explicitly freed  
Those in the stack can only be accessed locally and die when they go out of scope  
Heap variables have no limit on memory size
Stack size is dependent on the OS
Heap variables can be resized
In the stack the dimension is fixed at compile time

# Memory Errors

```C
#include  <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <string.h>

int main(int argc, char* argv\[\]) {
	if (argc != 2)
		printf("Syntax: %s <string>\n", argv[0]);
		exit(EXIT_FAILURE);
	}

	char *p;
	sprintf(p, "Input: %s", 
	printf("%s\n", p);
	return 0;
}
```

## Segmentation Fault

Notified by the OS when a program has attempted to access a restricted area of memory

In the previous code, memory wasn't allocated to store the string so the pointer `p`p is `NULL`
`malloc()` should be used to allocate memory in the heap to store the string

```C
char *p = malloc(strlen(argv[1]) + 1);
```

To allocate the memory for a string you need to allocate a byte more for a string terminator

## Memory Leak

Occurs when memory that is no longer needed is not released

Can lead to running out of memory causing the OS to thrash
**Thrashing** - Constant state of paging (rapidly exchaning data in memory for data on disk), causing the performance of the computer to fall

Fix the code by releasing the allocated memory
```C
free(p);
```

# Compiler Optimisation

Some compilers optimise code and automatically allocate the memory for obvious usage

## GCC Optimisation

Different levels of optimisation through the flag `-0`
`-01` or `-02` are most common, `-02` is most aggressive

# Stack Overflow

Occurs if the call stack pointer exceeds the stack bound
Each stack frame has a limited amount of address space  
- Often determined at the start of the program

