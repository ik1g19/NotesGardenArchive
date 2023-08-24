---
title: Arbitrary Code Execution and Mitigation
---
# How to Execute an Arbitrary Payload

1. We put the payload somewhere in the buffer
2. We put in the return address as the address of the buffer before the payload
3. We fill the buffer before the payload with `0x90` (`NOP` instruction)
	1. When the return register redirects to the buffer it will go ahead to find the payload to execute

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317192827.png)

# Creating the Payload

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317193343.png)

## Registers before Syscall

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317193834.png)

## Assemble the Payload

Payload must be assembled into machine code first to be executed

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317193921.png)

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317194122.png)

## How many NOP Operations to Create

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317194028.png)

## Creating the Exploit

Create a script that produces the command line input we need for the exploit
- A sequence of `NOP` (436 `0x90`)
- The payload
- Followed by the return address (So far unknown, left as `0x41` Char 'A')

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317195047.png)

It is necessary to avoid zeros in the payload, replace with `1-1` operations

# Executing the Exploit

Make the exploit script executable, (outside gdb launch):
```
chmod +x exploit
```

Execute the exploit inside gdb:
```
run $(./exploit)
```

`RBP` and `RIP` registers should be filled with `0x41`

# Locate the Memory Address of where to go

Examine the stack

```
mem read %rsp %rbp
```

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317200208.png)

When choosing a return address, pick an address with a `0x90`
Modify the exploit to print that as the last 8 bytes

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317200500.png)

# Launching the Exploit

Launch the exploit again and it should open a shell

# Using scanf vs strcpy

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317201044.png)

The overflow occurs here when more than 8 chars are passed from the keyboard when we call `scanf`
The input will overflow the buffer and overwrite `val`

Launching the overflow inside gdb
```
gdb ./vuln
run <<(repeat 8 printf 'A'; printf "\xef\xbe\xad\xde")
```

Here we use `run <<(...)` as we want to simulate the input like it is typed with the keyboard 

# Heap Based Buffer Overflow

Not as easy as overwriting a return address in the stack
By overflowing a buffer on the Heap we can overwrite a function pointer to point to another portion of the memory

In order to execute `winner()`, we overflow the buffer of 64 bytes so that the pointer `fp` points to `winner()` instead of `loser()`

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230317203106.png)

# Mitigation to Buffer Overflow

**Build and Compilation**
- compile using features or extensions that automatically provide a protection that mitigates or eliminates buffer overflows
- Examples: Microsoft Visual Studio /GS flag, Fedora/Red Hat FORTIFY_SOURCE GCC flag, StackGuard, and ProPolice
- **Limitations**:
	- these mechanisms can only detect certain types of overflows
	- an attack could still cause a denial of service, since the typical response is to exit the application
**OS Protection**: e.g. ASLR (address space layout randomisation), non-executable stack **Implementation**
- Implement and perform bounds checking on input
- Do not use dangerous functions (`gets`, `scanf`, `strcpy`)
- Use safer, equivalent functions which check for boundary errors
- Check the functions you are using (e.g. `man`)