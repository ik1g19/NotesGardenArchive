#### Explain the Difference between .NET and C#

.NET is the framework - a collection of libraries

C# is the programming language

#### Differences between .NET framework and .NET core

.NET core has better performance than framework

.NET 5.0 is a unified .NET development environment

#### What is Intermediate Code and the JIT

Partially compiled code

The JIT (Just in Time) compiler compiles the intermediate code to machine code for execution

#### What is the benefit of compiling to Intermediate Code

The runtime environment and development environment can be very different

JIT can optimize code for the runtime environment

#### What is CLR

Common Language Runtime

The first job of the CLR is to convert intermediate code to machine code

The second most important job is cleaning any unused memory using the Garbage Collector

#### What is Managed and Unmanaged Code

Code that runs under the umbrella of the CLR environment is managed code

Other code (their own compilers and runtimes) is unmanaged code

#### Explain the Importance of the Garbage Collector

The Garbage Collector runs constantly and consumes any **unused**, **managed** resources

#### Can the Garbage Collector claim Unmanaged Resources

No, the Garbage Collector only has access to managed resources

#### What is the Importance of CTS

Common Type System

The compiler compiles code into a Common Type System, it ensures that data types defined in two different languages get compiled into a common data type

#### Explain the Importance of CLS

Common Language Specification

A set of guidelines, when a .NET language adheres to the CLS it can be consumed by any language following .NET specifications

#### Explain the Difference between the Stack and the Heap

The stack is used to store primitive (and short lived) data types

The heap is used to hold data types with longer life spans, such as objects
- The pointer will be allocated to the stack, but the object itself will be allocated to the heap

#### What are Value Types and Reference Types

Value types contain the actual data e.g. where both the label and the data are kept on the stack

Whereas reference types only contain pointers, and the pointers point to the actual data e.g. on the heap

#### What is Boxing and Unboxing

Boxing s where your data moves from a value type to a reference type

```C#
int i = 10;
object y = i;
```

Unboxing is when you move a reference type to a value type

```C#
int z = (int)y;
```

#### What are the Consequences of Boxing and Unboxing

Moving data back and forth from stack to heap and so forth has an impact on performance

#### Explain Casting, Implicit Casting and Explicit Casting

Casting means you a trying to move one data type to another data type

If casting is done automatically, then it means it is implicit casting
- This happens when you are moving from a lower data type to a higher data type

```C#
int i = 10;
double d = i;
```

You need to do explicit casting when you are converting from a higher data type to a lower data type

```C#
double d = 100.23;
int y = (int)d1;
```

The consequences of explicit casting can be data loss, as you are converting to a less complex data type

#### What is the Difference between an Array and an ArrayList

Array
- Fixed size
- Strongly typed
	- Only use the same data types
- Better performance
	- Because it is strongly typed

ArrayList
- Variable size
- Not strongly typed
	- Add different data types
- Slower performance
	- Boxing and Unboxing

#### What are Generic Collections

Strongly typed and flexible collection

```C#
List<int> geneint = new List<int>();
```

#### How are Threads different from TPL

TPL - Task Parallel Library

![[Pasted image 20230920213432.png]]

TPL is used for parallel processing

Threads have an affinity for a single core and so will run on the same core

#### What is the Purpose of `Out`

`Out` is used to return multiple variables from a function

```C#
add(10, 10, out one, out two);

static void add(int num1, int num2, out int one, out int two)
{
	one = num1 + num2;
	two = num1 - num2;
}
```

#### What is a Delegate

A delegate is effectively a pointer to a function

Delegates are callbacks which help to communicate between asynchronous and parallel execution

![[Pasted image 20230920214710.png]]

#### What are some Example Usages of Delegates

Delegates can be used to send data between processes

If you have two tasks, and you need one task to receive data from another whilst continuing its normal operation - then you can subscribe a method from one task to the delegate so that the other task can pass data to it

#### What are Multicast Delegates

Where you can attach multiple functions to a delegate

#### What is an Event and How are Events different from Delegates

Events use delegates internally

Events are an encapsulation of delegates that make them safe

Events make a publisher and subscriber model

#### Events vs Delegates

Delegates are for callbacks, but are not encapsulated

Events are for a publisher subscriber model, they encapsulate delegates