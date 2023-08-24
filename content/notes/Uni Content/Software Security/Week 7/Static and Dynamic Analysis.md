---
title: "Static and Dynamic Analysis"
---

# Code Review

Manual debugging is not an easy process

When trying to write secure software, we use **atuomated code review**
- Static Analysis - Without running the program
- Dynamic Analysis - While the program is running

# Static Analysis

Enables us to verify software, find defects and problems and learnt about it without executing the software

## What can you find

- Flow issues
	- Infinite loops, unreachable code
- Security issues
	- Buffer overflows, input validation errors
- Memory issues
	- Unitialised data, null dereferences
- Input issues
	- SQL injection, Cross-site scripting
- Resources leaks
- Thread issues
- Exceptions
- Checking against pre-defined rules

## What can't you find

Unfortunately, non-trivial properties of programs are undecidable - A decision problem that admits no algorithmic solution is said to be undecidable.

We can never determine all possible program behaviours

## Types of Static Analysis Tools

- Source code analyzers
	$\circ$ Examine the source code and search for vulnerabilities using pattern matching against common types of vulnerabilities
- Bytecode code analyzers
	- Same as source code analyzers but analysis is performed on bytecode
- Binary code analyzers
	- Same as source code analyzers but analysis is performed on binary code

## Looking at it in Different Ways

- What strings does it contain?
- What functions does it call?
- How is the program set out?
- What libraries does it use?
- How was it compiled?

## How do Static Analysis Tools work

![[notes/Uni Content/Software Security/Images/Pasted image 20230507193034.png|500]]

## Intermediate Representations

- Abstract Syntax Trees (AST)
	- Encode how statements and expressions are nested to produce a programs
- Control Flow Graphs (CFG)
	- Describe the order in which code statements are executed and
	- Conditions to be met for a particular path of execution to be taken

Analyzers operate on these representations

### Abstract Syntax Tree (AST)

Tree representation of the abstract syntax of a program source code

The syntax is "abstract" in not representing every detail appearing in the real syntax
- Do not contain parentheses, brackets, comments,...

Leaves represent operands e.g variables or constants

Inner nodes denote operators e.g addition, assignments

![[notes/Uni Content/Software Security/Images/Pasted image 20230507193517.png|600]]

### Control Flow Graph (CFG)

A directed graph where
- Each node represents a statement
- Edges represent control flow

Statements may be
- Assignments $\mathrm{x}:=\mathrm{y}$
- Branches if $\mathrm{x}>0$ then
- Etc..

![[notes/Uni Content/Software Security/Images/Pasted image 20230507193639.png|600]]

## Analysis Techniques

- Lexical Analysis
	- Makes use of AST
- Data flow Analysis
	- Makes use of CFG
- Control Flow Analysis
	- Makes use of CFG

### Lexical Analysis

Scan the code and search for matches of functions that are know to be vulnerable

They skip comments and strings

Pro:
- Fast and cheap
- Good way to detect common unsafe and deprecate functions

Cons
- Not aware of the context

#### Example

![[notes/Uni Content/Software Security/Images/Pasted image 20230507194013.png|600]]

### Data Flow - Taint Propagation

Many tools perform "taint propagation"
- Input from untrusted users ("sources") considered "tainted"
- Warn/forbid sending tainted data to certain methods \& constructs ("sinks")
- Some operations (e.g., checking) may "untaint" data

Static analysis:
- Follow data flow from sources through program
- Determine if tainted data can get to vulnerable "sink"

#### Example

![[notes/Uni Content/Software Security/Images/Pasted image 20230507194256.png|500]]

### Control Flow

![[notes/Uni Content/Software Security/Images/Pasted image 20230507194422.png|600]]

### Tools

#### Open Source Tools

| Tool | Languages | Vulnerabilities |
| :--- | :--- | :--- |
| FlawFinder | C/C++ | Buffer overflows, format, string vulnerabilities, race, conditions etc |
| RATS | C/C++, Perl, PHP, Python, | Buffer overflows, format, string vulnerabilities, race, conditions etc |
| Clang Static Analysis | C, C++, Objective-C | Memory Leaks, Null, pointer dereferences |
| FindBugs | Java, Groovy, Scala | Null pointer, dereferences, synchronization errors |

#### Commerical Tools

| Tool | Languages | Vulnerabilities |
| :--- | :--- | :--- |
| Fortify |  Java, C, C++, C\#,XML, , SQL, JSP |  Buffer overflows, XSS, , SQL injection, Log forging, , Memory Leaks |
| Coverity | C, C++, C#, Java |  Buffer overflows, XSS, SQL injection, Log forging, , Memory Leaks |
| CodeSecure |  ASP.NET, VB.NET, C\#, Java/J2EE, JSP, EJB, PHP, Classic ASP and VBScript  | Web Application, Vulnerabilities and Malwares  |

#### Limitations

False positives: the tool reports bugs that program does not contain - Need to be manually reviewed

False negatives: the program contains vulnerabilities that the tool does not report
- They lead to a false sense of security

A tool is sound if it produces zero false negatives

It is unsound when it reduces the false positives at the cost of sometimes letting a false negative slip by

Static Analysis tools are a starting point for code review. Not a complete solution

Static Analysis tools do not understand what your application is supposed to do
- Out of the box rules are for general classes of security defects
- Applications can still have issues with authorization and other trust issues
- Only cover $50 \%$ of security defects (Dr Gary McGraw)

False positives can be time consuming to address

#### Key Characteristics

- Support multiple tiers
	- Many software projects are written in more than one language or programming platform
- Be extensible
	- New rules can be added
- Useful for security analysts and developers
- Support existing development process

# Dynamic Analysis

Dynamic analysis is all about what we can learn from the program while it is running

We can do this by examining the program state throughout execution

Approach for verifying software (including finding defects) by executing software on specific inputs \& checking results
- Functional testing, web application scanners, fuzz testing, etc.

Detection of vulnerabilities is integrated into the actual program's execution

## What can you find

- Runtime error detection
- Subtle defects and vulnerabilities
- Memory issues
- Memory leaks
- Input/output validation issues - Find the results of non-expected inputs
- Pointer arithmetic errors
- Response time issues
- Functional issues
- Performance

## What can't you find

- Anything off the runtime path
	- Input dependent

## Common Dynamic Analysis

- Coverage
- Performance
- Memory Usage
- Security properties
- Concurrency errors
- Violation of rules
- Invariant detection

Run the program, collect the information, analyse it

## Code Instrumentation

A technique that inserts extra code into a program to observe its runtime behavior

The extra code is called instrumentation code
- It inserts calls to analysis code when an instruction is executed
- Analysis code collects data about the execution of an instruction or about its behavior

The code can be inserted in the source code or in the binary code

## Instrumentation Approaches

Source instrumentation
- Instrument source programs

Binary instrumentation
- Instrument executables directly

Advantages for binary instrumentation
- Language independent
- No need to recompile the code
- All code is naturally covered

```C
#include <stdio.h>
int addnum(int a, int b)
{
	int sum;
	sum = a+b;
	return sum;
}

int main()
{
	int total;
	int x,y;
	x = 4;
	y = 7;
	total = addnum(x,y);
	printf("total %d\n”, total);
}
```


```C
include <stdio.h>
int addnum(int a, int b)
{
	int sum;
	#ifdef INSTDEBUG
		printf("Debug: Entering addnum %s %d\n”,__FILE__, __LINE__);
		printf("Debug: a = %d\n”, a);
		printf("Debug: b = %d\n”, b);
	#endif
	sum = a+b;
	#ifdef INSTDEBUG
		printf("Debug: sum = %d\n”, sum);
		printf("Debug: Leaving addnum %s %d\n”,__FILE__, __LINE__);
	#endif
	return sum;
}
```

## Compile Time Instrumentation Tools

**gprof**
- provides program profiling

**gcov**
- provides coverage analysis

**dmalloc**
- provides drop in replacement for the system's `malloc`, `realloc`, `calloc`, `free` and other memory management routines to enable runtime tracking of memory-leaks, out-of-bounds writes, and other capabilities

## Valgrind

It is a tool suite that provides a number of debugging and profiling tools

The most popular of these tools is called Memcheck
- detects many memory-related errors that are common in C and C++ programs and that can lead to crashes and unpredictable behaviour

## Pin

Pin is a dynamic binary instrumentation framework developed by Intel Corp

It lets you build program analysis tools called Pintools for Windows and Linux platforms

Pintools are written in C / C++

You can use these Pintools to monitor and record the behavior of a program while it's running

They have 3 main components
- Instrumentation
	- Enable the insertion of analysis routines
- Analysis
	- Performing the analysis itself
- Callback routines
	- Called when specific conditions are met

## Advantages of Dynamic Analysis

- No false positives or negatives on a given run
	- An error detection occurs right at the moment of its occurrence
- Do not need source code
	- You can also test proprietary code
- Clear which path was taken
- Can be used on live code
	- Particularly useful for security

## Disadvantages of Dynamic Analysis

- Detect vulnerabilities only on execution path defined by the concrete input data
- Significant computational resources are required to perform the analysis
- One execution path can be checked at each particular moment
- It is more difficult to track back a vulnerability to its exact location in the code

# Static Analysis vs Dynamic Analysis

```start-multi-column  
ID: ExampleRegion1  
number of columns: 2
border: off
shadow: off
```

**Static analysis**
- Analyze code without executing it.
- Systematically follow an abstraction.
- Find bugs/enforce specifications/prove correctness.
- Often correctness/security related.

--- end-column ---

**Dynamic analysis**
- Analyze specific executions.
- Instrument program, or use a special interpreter.
- Abstract parts of the trace.
- Find bugs/enforce stronger specifications/debugging/profiling.
- Often memory/performance/concurrency /security related.

=== end-multi-column