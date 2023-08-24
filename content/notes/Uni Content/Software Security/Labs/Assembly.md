---
title: Assembly
---
# x86_64 Register Architecture

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314192038.png)

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314192611.png)

## Example: 64-bit Addition

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314193007.png)

## Example: 32-bit Addition

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314193037.png)

## Example: 16-bit Addition

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314193125.png)

## Example: 8-bit Addition

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314193140.png)

## Byte Order

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314193624.png)

## Virtual Address Space

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314201423.png)

Addressing memory in absolute terms witha 64 bit address is not a good idea
It is forbidden on most architectures
All references to memory have to be relative from a register

```
-16(%rsp)  
8(%rbp)  
127(%rip)
```

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230314202807.png)

`disp(base,index,scale) à base + index*scale + disp`

**Example**
`-3(%rbp,%rdi,8)`
typically used to access `%rbp[%rdi]` where each array element is 8 bytes long and you you’re accessing at -3 bytes from it

# x86_64

## Addressing Modes

### Immediate
`mov $10, %eax`

### Register to Register
`mov %r8l, %al`

### Indirect
`mov 1234(%rcx, %rax, 8), %r8w`

Sometimes it is necessary to add a size postfix to instructions
`movb, movw, movl, movq (b = byte, w = word, l = long, q = quadword)`

### Rip-Relative
`movb 12(%rip), %al`

### Example
Sum numbers 1 to 10 in register `%eax`
```
    xor %eax, %eax                   # zero %eax – why not “mov $0, %eax” ?  
  mov $10, %ecx                      # set the loop index  
lab:                                 # define label  
	add %ecx, %eax                   # %eax += %ecx  
	loop lab                         # dec %ecx, jump to lab if not  
zero
```

## Instruction Set

### MOV
![|550](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315171206.png)

### MOV v LEA
![|550](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315171355.png)

### CMOV
CMOVcc instructions can replace two instructions in situations like  
`if ecx == 5 then eax = ebx`

Normally this would need to be implemented as:  
```
cmp $5, %ecx  
jnz continue  
mov %ebx, %eax  
continue:  
```

Instead:  
```
cmp $5, %ecx  
cmovz %ebx, %eax
```

### Tests and Jumps
![|550](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315171858.png)

### Arithmetic
![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315172405.png)

### Push and Pop
![|550](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315172558.png)

`push <src>` is like `dec %rsp; mov <src>,(%rsp)` 
`pop <dst>` is like `mov (%rsp),<dst>; inc %rsp`

## Program Structure

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315173141.png)

### Example: Sum an Array
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315181616.png)

### Example: Max of Three
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315181747.png)
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315182023.png)

## Calling Conventions

### Passing and Return Arguments
The first six integer arguments are passed in registers as follows:
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315182317.png)
![|300](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315182335.png)

The seventh and additional arguments are passed on the stack
Standard calling convention requires that when passing arguments (values or addresses) on the stack, the arguments should be pushed in **reverse** order
`someFunc (one, two, three, four, five, six, seven, eight, nine)` would imply a push order of: `nine`, `eight`, and then `seven`

For floating-point arguments, the floating-point registers $\mathbf{x m m 0}$ to $\mathbf{x m m} 7$ are used in that order for the first eight float arguments

### Calling 64-bit Code
After the parameters are pushed, the call instruction is made, so when the called function gets control, the return address is at `%(rsp)`, the first memory parameter is at `8(%rsp)`, etc

**The stack pointer `%RSP` must be aligned to a 16-byte boundary before making a call**
But the process of making a call pushes the return address (8 bytes) on the stack, so when a function gets control, `%rsp` is not aligned. You have to make that extra space yourself, by pushing something or subtracting 8 from `%rsp`

The only registers that the called function is required to preserve (the calle-save registers) are: `rbp`, `rbx`, `r12`, `r13`, `r14`, `r15`
All others are free to be changed by the called function

![|300](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315183728.png)

This is what the stack will look like on entry to a function with $9+$ arguments, assuming that the callee uses (and) therefore must save `%rbx`, `%r12`, `%r13`
Notice that it is good practice to save `%rbp` on the stack, and set it to point at the base of the stack for the current frame - which is where it takes its name from

#### Example: Hello World
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315183946.png)

#### Example: Hello World with OS System Calls Directly
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315184114.png)

### Summary of Stack Organization
![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315184214.png)
![|300](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315184233.png)

### Summary of Register Conventions
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315184352.png)

