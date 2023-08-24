---
title: Simple Macros
---
# Text-based Macros

The earliest form of macros appeared in macro assembly languages where a name could be given to a common pattern of assembler instructions

This idea made its way in to the C programming language - enhanced with parameters  
- The task of textually replacing (expanding) macros became the responsibility of the C pre-processor - often separated from the main compiler code
- C style macros subsequently made their way in to C++

## Object-like Macros

The easiest form of macro definition in C is the object-like macro  
- Typically used to name constants

- Use \#define to create a macro name and simply use the macro name in the main code
- Macro usages are expanded by the pre-processor to be textual replaced with their definition
- Multiline macro definitions use \\ as a line separator
- Macro definitions are scanned sequentially within the code and only defined in program order
- The \#undef directive removes a macro definition at that program point
- Macro usages are repeatedly expanded until no further usages are found

```C
#define BUFFER_SIZE 1024  
//...  
foo = (char *) malloc (BUFFER_SIZE);  
//...
```

```C
#define BUFSIZE 1024  
#define TABLESIZE BUFSIZE  
#undef BUFSIZE  
#define BUFSIZE 512  
#define DECSIZE int tSize \  
			= TABLESIZE;
```

>[!Tip]
>Expands to `"int tSize = 512;"`

## Function-like Macros

Macros make take parameters:  
- Use parentheses in the definition after the macro name to indicate these
- Use valid C identifiers, comma separated, optional whitespace

- Macro argument usages are supplied using comma separated lists of code fragments
- Arguments may contain macro usages - these are (repeatedly) expanded before expanding the macro being called
- Whitespace is normalised to single spaces where needed
- You can omit arguments in calls - this supplies empty arguments

```C
#define MIN(X,Y) (X<Y)?X:Y  
//...  
x = MIN(3,5) → x = (3<5)?3:5  
MIN((z+1),20) → ((z+1)<20)?(z+1):20  
//...
```

```C
#define FOO(X,Y) X + Y + "Y"  
FOO(3, ) //→ 3 + + "Y"  
FOO(3,5) //→ 3 + 5 + "Y"  
FOO() //→ error
```

## Lexical Expansion

C style macros use lexical expansion
High-Level overview:
- Macros definitions are stored in Tokenised form - not raw strings
- pre-processor scans the program text
- on \#define, macro definition is extracted and stored
- if a name is macro-defined, it is expanded
	- macro parameters replaced by expanded arguments
	- result is re-expanded to expand lower macro layers
- if a name is not macro-defined, it is copied to output
- Recursive calls to a macro are not re-expanded

## Macros vs Functions

- Although parameterised macros look a little like (inlined) functions, they are crucially different
- Macro definitions and arguments are code fragments - no need for completed expressions as with functions
- Macro arguments can contain other macro usages (cf. first-order functions only in $\mathrm{C} / \mathrm{C}++$ ), types and lexical entities e.g. variable names
- Unlike function bodies, macro definitions can be used to declare new functions, variables, classes etc.

```C
#define SWAP(T,x,y) T t=x;x=y;y=t;  
#define INITIALIZE = 0;  
SWAP(int, low, high)  
low INITIALIZE
```

>[!Tip]
>Expands to : 
>`int t = low ; low = high; high = t`
>`low = 0;`

## Stringizing

Sometimes you don't want to treat the macro argument as a token sequence (to be later parsed) but actually as the string literal that was used to represent the argument
C Style macros allow for this - it is called "stringizing"
Simply use \# before the macro argument usage to stringize an argument

```C
#define WARN_IF(EXP) \  
do { if (EXP) \  
	fprintf (stderr, "Warning: " #EXP "\n"); } \  
while (0)  
WARN_IF (x == 0);
```

>[!Tip]
>Expands to :  
>`do { if (x == 0) fprint (stderr,"Warning: " "x==0" "\n"); while (0);`

## Token Pasting

C Style macros also allow you to modify the lexically matched strings used for identifiers in types, function names, variables etc  
Use the directive ## between two tokens to effectively paste them, or concatenate the tokens together to form a single token

```C
#define COMMAND(NAME) { #NAME, NAME ## _command }  
struct command commands[] =  
{  
	COMMAND (quit),  
	COMMAND (help),  
};
```

```C
struct command  
{  
	char *name;  
	void (*function) (void);  
};
```

>[!Tip]
>Expands to :  
>```C
>struct command commands[] =  
>{  
>	{"quit",quit_command },  
>	{"help",help_command }  
>};

## Variadic Macros

C style macros support variadic arguments  
Use ... as the argument name and `__VA_ARGS__` inside the macro  
body to use the argument

```C
#define eprintf(...) fprintf (stderr, __VA_ARGS__)  
eprintf ("%s:%d: ", input_file, lineno)
```

>[!Tip]
>Expands to :  
>`fprintf (stderr, "%s:$d: ", input_file, lineno)`

#### Example - 3D Arrays as Macros for 1D Arrays
```C
#include<stdio.h>  
#define MAKE_2DARRAY(T,N,M,a) \  

T a[N*M];\  
int a##COLS = M;  

#define SET_2D(a,i,j,v) a[i*a##COLS+j]=v  
#define GET_2D(a,i,j) a[i*a##COLS+j]
```

```C
int main(){  
	MAKE_3DARRAY(int,3,5,3,a)  
	SET_3D(a,2,3,1,455);  
	int v = GET_3D(a,2,3,1);  
	printf("COLS is %d\n" , aCOLS);  
	printf("VALUE is %d\n" , v);  
}
```

```C
#define MAKE_3DARRAY(T,N,M,K,a) \  
MAKE_2DARRAY(T,N,M*K,a)\  
a##COLS = M;\  
int a##DEP = K; 

#define SET_3D(a,i,j,k,v) SET_2D(a, i*a##DEP, j*a##DEP+k, v)  
#define GET_3D(a,i,j,k) GET_2D(a,i*a##DEP,j*a##DEP+k)
```

