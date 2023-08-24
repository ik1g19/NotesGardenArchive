---
title: Hygienic Macros
---
# Problems with C Style Macros

Most of the problems stem from the way that a macro usage hides the code it maps to at the call site
The problems also stem from the fact that these are lexical macros that allow names to be mapped to arbitrary token streams
What might look like reasonable code may not even be grammatically correct, never mind behaviourally correct

## Misnesting

One can build macros where the macro call is expanded partially from the macro call and partially from its arguments
- This is generally considered bad but could be used as a form of macro "callback" feature

```C
#define twice(x) (2*(x))  
#define call_with_1(x) x(1)  
call_with_1 (twice)
```

>[!Tip]
>Expands to `twice(1)`
>Expands to `(2*(1))`

Because macro definitions do not have to have balanced parentheses, scope can begin within the body of a macro and end outside of the macro call

```C
#define strange(file) fprintf (file, "%s %d",  
strange(stderr) p, 35)
```

>[!Tip]
>Expands to `fprintf (file, "%s %d, p, 35)`

## Operator Precedence Changes

Suppose we define a function-like macro that converts degrees to radians

```C
#define PI 3.142  
#define DEGTORAD(X) X*PI / 180
```

`rad = DEGTORAD(angleA - angleB)` exapnds to `rad = angleA - angleB *3.142 / 180`
But * binds more tightly than - so although the macro usage looks okay, the operators in the arguments to the macro call can interact with the macro body to give unintended results

### Double Bagged Macros

To avoid these two kinds of operator precedence problems with macros we should always put parentheses both around macro argument usages **and** around the entire macro body

Now `DEGTORAD(angleA - angleB)` expands to `( (angleA - angleB) *3.142 / 180 )`

## Swallowed Semicolons

Suppose we define a function-like macro that assigns pairs of values
```C
#define ASSIGNPAIR(X,Y,V,W) X = (V) ; Y = (W)
```

Suppose we use this macro in a conditional statement
```C
if (x < y) ASSIGNPAIR(a,b,x,y); else ASSIGNPAIR(a,b,y,x);
```

This expands to `if (x < y) a = (x) ; b = (y) else a = (y) ; b = (x);`
The semicolon terminates the if statement

To avoid this we need to protect statement bodies by using a new block scope
```C
#define ASSIGNPAIR(X,Y,V,W) do { X = (V) ; Y = (W) } while (0)
```

## Duplicated Side-Effects

```C
#define MIN(X,Y) (((X)<(Y))?(X):(Y))
```

Suppose
```C
MIN(++x,y)
```

This expands to
```C
(((++x)<(y))?(++x):(y))
```

Although the macro call only contains one use of `++x` the expansion has two

To avoid this we need to define temporary variables
```C
#define MIN(X,Y) ( { typeOf(X) _X = X ; \
					 typeOf(Y) _Y = Y ; \
					 (((_X)<(_Y))?(_X):(_Y))
```

## Variable Capture

Suppose
```C
#define SWAP(T,X,Y) do {T tmp = X ; X = Y ; Y = tmp; } while (0)

int tmp = 0; int foo = 1 ; SWAP(int,tmp,foo) ;
```

This expands to
```C
int tmp = 0; int foo=1; do {int tmp = tmp ; tmp = foo; foo = tmp; } while (0);
```
`tmp` is used while undefined
The name `tmp` is passed as an argument is captured by the macro local name

Can decrease likelihood of this by obfuscating any macro local variables
```C
#define SWAP(T,X,Y) do {T __tmpSWAP__ = X ; X = Y ; Y = __tmpSWAP__; } while (0)
```

# Macro Hygiene

We say that a macro system is hygienic if its expansions cannot cause collisions with the arguments or calling context.
There are three kinds of macro hygiene:
- **Syntactic Hygiene** guarantees structural integrity of the expanded code - can be implemented by substituting syntax trees of macro bodies are in to syntax trees of the calling context.
- **Variable Hygiene** guarantees referential integrity of the expanded code - no capture of identifiers. Can be implemented by controlled renaming of variables.
- **Type Hygiene** guarantees type integrity, i.e. the type of expanded macro calls is consistent with the type expected in the calling context. This is difficult to implement and not commonly seen.

# Syntactic Hygiene

Macro expansion inserts trees
![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330162939.png|500]]

Macro processor needs to be language-aware:
- must parse macro bodies
- must check syntactic categories
- requires tighter integration with compiler, less general

# Variable Hygiene

To guarantee variable hygiene the macro expansion algorithm should distinguish the calling context from the macro body context
By systematically renaming variables by tagging them with contextual information then even when variables are passed in to a capturing body they will be distinct

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230330163107.png|600]]

The two tmp variable names would be named differently as they come from different contexts

# Languages with Hygienic Macros

The LISP programming language was an early adopter of hygienic macros (syntactic and variable)
This system was further refined and implemented in the Scheme language.
The macro system there is based around describing syntactic patterns to match along with syntactic trees to rewrite them with.
This idea inspired the (mostly) hygienic macro system in Rust - to be discussed in the next session.
Other languages with hygienic macros include;
- Dylan, Elixir, Nim, Haxe, Julia, Raku (Perl 6)

