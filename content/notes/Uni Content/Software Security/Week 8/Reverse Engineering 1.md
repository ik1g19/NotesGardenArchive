---
title: "Reverse Engineering 1"
---

# What is Reverse Engineering

- Taking an existing program for which source-code or proper documentation is not available
- Attempting to recover details regarding its' design and implementation

# Different Reprenstations

Zero level - Machine code (ones and zeros)

Low level - Assembly instructions

Intermediate level - Programming languages C++

High level - Programming languages Python

# Low-Level Software

Development tools isolate software developers from processor architectures and assembly languages

Low-level software (system software) is the layer that isolates software developers and application programs from physical hardware
- C program invoking `printf()` library call, which calls `write()` system call

Solid understanding of low-level software and programming is required to a reverser
- High-level details are almost always eliminated

# Machine Code

Machine code (often called binary code, or object code) is sequences of bits that contain a list of instructions for the CPU to perform

CPUs can only run machine code

The instructions depends on the architecture of CPUs
- How a CPU consumes the data

# Assembly Language

Assembly language is simply a textual representation of bits in machine code
- We name elements in these code sequences in order to make them human-readable
- Instead of cryptic hexadecimal numbers, we can look at textual instruction names such as MOV (Move), XCHG (Exchange), and so on
	- we call these as "mnemonics"
- Each assembly language command is represented by a number, called the operation code, or opcode

Every computer architecture has its own assembly language that is usually quite different from all the rest
- Therefore, assembly language is a class of languages, not one language

Machine code and assembly language are two different representations of the same thing

# Object Code

Object code is essentially a sequence of opcodes and other numbers used in connection with the opcodes to perform operations

CPUs constantly read object code from memory, decode it, and act based on the instructions embedded in it

An assembler translates the textual assembly language code into binary code
- A disassembler does the exact opposite

# Compilers

A compiler takes a source file and generates a corresponding machine code file
- The source file would contain instructions that describe the program in a high-level language such as C++ and Java

This machine code file can either be
- A standard platform-specific object code that is decoded directly by the CPU
- Or it can be encoded in a special platform-independent format called bytecode

Compilers of traditional (non-bytecode-based) programming language such as C and C++ directly generate machine-readable object code from the textual source code

# Java Virtual Machines (JVMs)

Compilers for high-level languages, such as Java, generate a bytecode instead of an object code

Bytecodes are similar to object codes
- Except that they are usually decoded by a program, instead of a CPU

A compiler generates the bytecode and a program, called a virtual machine, decodes the bytecode and performs the operations described in it

The virtual machine can be ported to different platforms, which enables running the same binary program on any CPU as long as it has a compatible virtual machine
- Platform independence

# Operating Systems

An operating system is a program that manages a computer, including hardware devices and software applications

An operating system takes care of many different tasks and can be seen as a kind of coordinator between the different elements in a computer

An operating system serves as a gatekeeper that controls the link between applications and the outside world
- Many reversing techniques revolve around the operating system
- Any reverser must have a good understanding of what they do and how they work

# Overall Picture

![[notes/Uni Content/Software Security/Images/Pasted image 20230508192408.png|600]]

# System Monitoring Tools

System-level reversing requires a variety of tools that sniff, monitor, explore, and expose the program being reversed

Because almost all communications between a program and the outside world go through the operating system, the operating system can usually be leveraged to extract such information

System-monitoring tools can monitor networking activity, file accesses, registry access and so on
- There are also tools that expose a program's use of operating system objects such as mutexes, events, and so forth

# Disassemblers

Disassemblers are programs that take a program's executable binary as input and generate textual files that contain the assembly language code for the entire program or parts of it

This is a relatively simple process considering that assembly language code is simply the textual mapping of the object code

Disassembly is a processor-specific process, but some disassemblers support multiple CPU architectures

# Debuggers

A debugger is a program that allows software developers to observe their program while it is running

The two most basic features in a debugger are the ability to set breakpoints and the ability to trace through code

Breakpoints allow users to select a certain function or code line anywhere in the program and instruct the debugger to pause program execution once that line is reached
- When the program reaches the breakpoint, the debugger stops (breaks) and displays the current state of the program
- At that point, it is possible to either release the debugger and the program will continue running or to start tracing through the program

Debuggers allow users to trace through a program while it is running - This is also known as single-stepping

Tracing means the program executes one line of code and then freezes, allowing the user to observe or even alter the program's state o The user can then execute the next line and repeat the process

This allows developers to view the exact flow of a program at a pace more appropriate for human comprehension

Because developers have access to the source code of their program, debuggers present the program in source-code form, and allow developers to set breakpoints and trace through source lines, even though the debugger is actually working with the machine code underneath

Reversers use debuggers in disassembly mode
- In disassembly mode, a debugger uses a built-in disassembler to disassemble object code on the fly
- Reversers can step through the disassembled code and essentially watch the CPU as it's running the program on instruction at a time
- Reversers can install breakpoints in locations of interest in the disassembled code and then examine the state of the program

# OllyDbg

1. Disassembled code as it is executed
2. Registers along with their value in real time (when a value is changed, it appears in red)
	- You can modify the value of these registers
3. Current state of the stack in memory
4. Dump of live memory for the debugged process

![[notes/Uni Content/Software Security/Images/Pasted image 20230508193039.png|600]]

# Decompilers

Decompilers are the next step up from disassemblers
- Takes an executable binary file and attempts to produce readable high-level language code from it

The idea is to try and reverse the compilation process, to obtain the original source code or something similar to it

On the vast majority of platforms, actual recovery of the original source code isn't really possible
- Significant elements are just omitted during the compilation process (for optimisation) and are impossible to recover

