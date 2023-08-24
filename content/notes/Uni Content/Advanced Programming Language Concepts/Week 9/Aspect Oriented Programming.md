---
title: "Aspect Oriented Programming"
---

# Separation of Concerns

A **concern** is a specific requirement or consideration that must be addressed in order to satisfy the overall system goal

e.g. functionality, efficiency, reliability, persistence, security, usability

# Dominant Decomoposition

We use the term "cross-cutting" concern for concerns that are not located in a single unit of code.

Generally speaking we try to avoid cross-cutting concerns as they lead to high coupling and low cohesion

We can't always achieve this though as refactoring code to isolate one concern may cause another concern to become cross-cutting.

We saw this as a problem with inheritance also and the phenomenon is often referred to as "Dominant Decomposition"

The key issue is that cross-cutting concerns are really common - we tend to design around functionality so the following are often crosscutting:
- Error handling, memory management, caching, distribution, persistence, security, logging, network management etc.

The idea of Aspect Oriented Programming is a response to the dominant decomposition problem

# Fundamental Idea of Aspect-Oriented Programming

Isolate cross-cutting concerns in separate code units called **aspects**

Use code-generation techniques to rewrite the code base to distribute the aspects across the code base as required.

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507185739.png|450]]

# Macros vs Aspects

This looks a little bit like a load of macro definitions and macro expansion doesn't it?

Macros use explicit invocation - if you want to insert code defined in a macro in to your code base you need to call the macro by name.

Aspects use implicit invocation!

The code base is oblivious to the code contained in the aspects and can be compiled with or without weaving the aspect code in.

This allows for e.g. software product lines to include concerns on a per-product basis without disrupting the main code base.

This is a compelling idea but doesn't quite convey how the aspect weaver knows where to insert the aspect code.

There is a small domain specific language used to describe exactly this.

# JoinPoints

A **JoinPoint** is a point in the execution of a program at which a crosscutting concern might intervene.

It is a semantic concept - JoinPoints aren't just locations in the code-base but can correspond to these.
- **Static JoinPoints** refer to JoinPoints described by code patterns that do not depend on runtime information to identify when to intervene.
- **Dynamic JoinPoints** refer to JoinPoints that require runtime information to execute the intervening code

For example, for a concern where code intervenes after every execution of a given method then the 
JoinPoints for this can be determined statically by inserting code at the end of the given method definition.

For a concern where the intervening code is to be made after execution of a given method but it depends on the arguments to the method call then this cannot necessarily be determined statically and so is a dynamic JoinPoint

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507190124.png|500]]

## Dynamic JoinPoint Example in AspectJ

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507190237.png|500]]

# PointCuts

A **PointCut Descriptor** is a syntactic expression that describes a set of JointPoints

These are given in a domain specific language to describe JoinPoints.

For example, in AspectJ we have pointcut descriptors:
- call that describes the invocation point of a method
- execution that describes the actual execution of a method after dispatch
- get that describes the access of a field value
- set that describes the mutation of a field value

There are also pointcut kinds that describe the call of a constructor, the initialisation of an object, the pre-initialisation of an object! The handling of exceptions ...

## Example PointCut

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507190639.png|500]]

# Advice Code

Advice code (or just advice) is the name given to the code that is used when intervening at a JoinPoint

That is, the advice is the code that implements the cross-cutting concern that this aspect is being used to implement.

Advice is a syntactic construct - in AspectJ it is just Java code.

Given that a JoinPoint is a point in the execution of a program, there are different possibilities about how advice code is placed relative to the JoinPoint code.

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507190856.png|560]]

# Aspects

An aspect is the packaging together of PointCut descriptors and corresponding advice code to implementing a given cross-cutting concern.

That is, the advice is the code that implements the cross-cutting concern that this aspect is being used to implement.

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507191009.png|500]]