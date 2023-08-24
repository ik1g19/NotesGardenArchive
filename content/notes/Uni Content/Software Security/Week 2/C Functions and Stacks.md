---
title: C Functions and Stacks
---
# Data types

## Integer Types

| datatype | size | range |
| :--- | :--- | :--- |
| char | 1 byte | -128 to 127 or 0 to 255 |
| unsigned char | 1 byte | 0 to 255 |
| signed char | 1 byte | -128 to 127 |
| int | 2 or 4 bytes | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
| unsigned int | 2 or 4 bytes | 0 to 65,535 or 0 to 4,294,967,295 |
| short | 2 bytes | -32,768 to 32,767 |
| unsigned short | 2 bytes | 0 to 65,535 |
| long | 4 bytes | -2,147,483,648 to 2,147,483,647 |
| unsigned long | 4 bytes | 0 to 4,294,967,295 |

## Floating Point Types

| datatype | size | range | precision |
| :--- | :--- | :--- | :--- |
| float | 4 byte | 1.2E-38 to 3.4E+38 | 6 decimal places |
| double | 8 byte | 2.3E-308 to 1.7E+308 | 15 decimal places |
| long double | 10 byte | 3.4E-4932 to 1.1E+4932 | 19 decimal places |

# Memory Layout

## Stack

The stack is the area where local variables are stored
When any function is called, a stack frame is created
When a function returns, the corresponding stack frame is destroyed

The stack frame contains data like the return address, arguments passed to the function and local variables
![|300](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221212722.png)

### Call by Value

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221213738.png)

Copies the actual value of the argument into the stack frame
Changes made to the parameters inside the function affect locations on the stack that are destroyed upon exiting the function

### Call by Reference
Copies the address of the argument into the stack frame
The address is used to access the actual argument
Therefore effects of the function persist after the stack frame is destroyed

## * and & Operators

\* indicates the variable type is a pointer
This is dereferencing

&  allows to get the address of the variable
This is referencing

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221214511.png)

## Pointers Arithmetic

The pointer can be incremented or decremented
If pointer `p` has type `T*`, the `ith` address after `p` can be calculated by using:

```C
(p + i) == (p) + [i * sizeof(T)]
```

## Null Pointers

NULL can be assigned to a pointer via:

```C
int *ptr = NULL;
```

To check for a null pointer you can use:

```C
if (ptr) /* succeeds if p is not null */
if (!ptr) /* succeeds if p i null*/
```