---
title: Template Metaprogramming
---
# Parametric Declarations

Parametric declarations of classes, structures, functions etc could be loosely considered as another very simple common form of metaprogramming.
We see these in many languages
- Parametric polymorphism in functional languages such as ML and Haskell
- Java Generics
- C++ template polymorphism (e.g. in the Standard Template Library)

Although we aren't manipulating code directly when using these, there is often some notion of expansion or rewriting of code that happens to implement these

# C++ Templates

The C++ approach to parametric polymorphism

Class definitions may be written in templated form

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330163542.png|500]]

# C++ Function Templates

The same template modifier can be applied to individual function definitions

```C
template <class T>  
T min(const T& a, const T& b){  
	if (a < b) return a; else return b;  
}
```

>[!Tip]
>There is no separate type-checking upon template instantiation and expansion.  
>If the programmer uses the instance `min<someType>` where someType does not support an < operation this will fail. cf. Haskell type class Ord

# Template Instatiation

To instantiate a template at a particular concrete argument we use the notation `Foo<Arg>`

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330163753.png|500]]

A fully expanded template class is just a normal class
Template expansion is performed in an early stage of the compiler

## Code Bloat

Implementation of $\mathrm{C}++$ templates usually follows the instantiation model:
- for each template instance, a separate piece of code is generated
- there is no sharing between different template instances
- but caching of repeated instances with same arguments
- not directly required by semantics (but implicit)
Different to Java Generics
Speed/space trade-off: instantiation model usually faster but prone to code bloat:
- many instances leads to class definitions for each different combination of the arguments used

# Template Parameters

Templates can have three different kinds of parameters:
The first is **types** or **classes**:
- these are the most common kind
- they are usually denoted by class keyword
- some restrictions: no local classes, ...
The second kind is non-types (i.e., **values**)
- These are integral value types : int, bool, short, long etc
The third kind is **templates** themselves as parameters!
- This allows for higher-order template definitions

>[!Tip]
>There is also an alternative keyword `typename` that is sometimes used to denote type parameters

```C
template <template <class T> class TT>  
class A {  
	//...  
};
```

# Value Parameters

The use of value parameters is a very interesting feature in C++ templates and distinguishes it from e.g. Java Generics

```C
template <class T, int Max>  
class stack {  
	//...  
	public:  
	//...  
		bool is_full() { return size==Max}  
};
```

This allows for a generic stack implementation but also allows the type itself to depend on the integer value parameter
- This is dependent typing! In C++ !

# Template Specialisation

Each template may be defined using several **specialised** cases

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330164447.png|700]]

>[!Tip]
>Given a usage `t<A,B,C>`, the compiler expansions algorithm has to choose the maximally specialised pattern that matches `A,B,C`
>This must be unique or a compiler error occurs

# Observations on Template Specialisation

Specialisation is allowed for all template parameters including non-type parameters
This requires compile-time expression evaluation, which can be forced by using static const or enum
The selection of most specialised instances is a form of computation - it can encode conditionals!
Recursive expansion of templates is a form of computation - it can encode recursion.
Template expansion is a Turing-complete computational model!
It is executed "statically" by the compiler!
We could (but shouldn't) make a programming language out of this.
It is akin to "functional programming with bad syntax"

# Template Metaprogramming

We can use the template "meta programming" language to say, calculate expressions at compile time

```C
template <int N> struct Factorial {  
	enum { RET = N * Factorial<N - 1>::RET };  
};  
template <> struct Factorial<0> {  
	enum { RET = 1 };  
};  
void foo() {  
	int x = Factorial<3>::RET; // == 6  
	int y = Factorial<0>::RET; // == 1  
}
```

The use case for this is not entirely convincing and nowadays would be better done using a constexpr (C++11) or better a consteval (C++20)
The use of pattern matching and recursion is useful to see though.
Template metaprogramming becomes more powerful when used for manipulating code portions programmatically. e.g. loop unrolling

# Loop Unrolling with Template Metaprogramming

Suppose
```C
inline void addVec(int size, double* c, double* a, double* b) {  
	while (size--)  
		*c++ = *a++ + *b++;  
}
```

Typically we might know the size of vectors that we are manipulating at compile time. This is a "static" argument
If so then we should be able to avoid the while loop and create code that makes the appropriate fixed number of additions

```C
template <int n>  
inline void addVect(double* c, double* a, double* b) {  
	*c = *a + *b;  
	addVect<n-1>(c+1, a+1, b+1);  
}  
template<>  
inline void addVect<0>(double* c, double* a, double* b) { }
```

An expansion of the instantiation at some integer `N` would have `addVect<N>` unroll to create a series of assignments

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330165110.png|500]]

# Partial Evaluation using Template Metaprogramming

Notice the mix of both static and dynamic arguments to the example `addVec` function above.  
We can use this idea to good effect in a variety of scenarios

```C
int power(int n, int m){  
	if (n==0) return 1  
	else if (n==1) return m  
	else return power(n-1, m) * m ;  
};
```

Suppose the value n is known at compile-time  
- make it a template argument!

If the n argument is static but m not then we can partially evaluate the function using a template

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330165603.png|500]]

>[!Tip]
>The concept of **partial evaluation** or **staged computation** refers to symbolically executing code P for some given static inputs, leaving a residual computation P' that depends on dynamic inputs

>[!Tip]
>The concept of **staging** refers to identifying those parts of the code that are suitable for evaluating statically

