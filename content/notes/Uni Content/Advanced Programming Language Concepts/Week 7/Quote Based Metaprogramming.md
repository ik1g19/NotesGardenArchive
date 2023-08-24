---
title: "Quote Based Metaprogramming"
---

# Metaprogramming Requirements

In order to provide meta programming support in a language we need support to
- Represent programs as data objects
- Manipulate programs as data objects
The former is fundamental to this but the question of what is a good representation is wide open.
- Strings or pure text based representations
- Lexical or token based representations
- (Abstract) Syntax tree representations
- Something else? Data formats, XML, JSON ?

# Pros and Cons of Representations

Text Based:
+ Easy "low tech" solution, very flexible, easiest to write code in
- Not grammar aware so no safety of any kind

Token Based:
+ Better "mid tech" solution, flexible
- harder to work with for programmer - who knows the token names?
- Not grammar aware, no limited safety

AST Based:
+ Even better solution still - bound to work in AST data structure
+ Grammar aware, syntactic safety possible
- hard to program, uses e.g. reflection and AST node constructors

# Basic Idea of Quote Based Metaprogramming I

- Let the compiler work build the AST!
- To get the benefit of the ease of working with string representations (just write the source code) but the integrity of working with ASTs we need to use an approach to move between the two.
- If we can code program values as strings but manipulate them as ASTs this would achieve this. i.e. we need to parse the string values.
- Compilers already contain a parser for the language!
- If we can expose that parser and make calls to it then we can exploit it for metaprogramming.
- This is the first basic idea of quote based metaprogramming.
- We quote portions of source code within our code to instruct the compiler to treat this not as code but as data. i.e. build the AST from it

## Example of Quoting Code

The meta-language manipulates AST objects built from directly "quoting" source level artefacts

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504012331.png|400]]

# LISP Quote

An early example of seeing code as data appears in the LISP language (and Scheme and Racket)

This is achieved by the use of S-expressions in LISP

These are essentially symbolic lists that represent LISP expressions - i.e. simple forms of an AST

The quote operation in LISP convert an expression in to an Sexpression: we use a single apostrophe to quote an expression

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504012522.png|400]]

There is a variant of quoting that uses the backtick \`symbol instead

# Julia Quote

A modern version of Lisp quote has made its way in to the Julia language

We use `:(` expr `)` to build an AST of the expr within the parentheses.

e.g. the quote :(1 $\left.{ }^* \sin (\mathrm{pi} / 2)\right)$ converts to

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504012747.png|250]]

We can manipulate this tree directly in Julia:
e.g. $P=:(a=2 ; b=3 ;$ add $[a, b])$

# Basic Idea of Quote Based Metaprogramming II

- Quote is pretty boring
- It is just an embedded call to parse source expressions with the (meta)language.
- What if we could insert meta-level values into the ASTs that a quote generates though?
- This would be akin to a parametric AST.
- This is the second basic idea of quote based meta programming.
- Take a (meta level) value and splice it in to the AST.
- We call this operation unquote or splicing

# Example of Unqouting Code

The meta-language manipulates AST objects by inserting (the parsed) meta-level values in to the quoted tree

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504013028.png|400]]

# Interpolation

We are familiar from scripting languages with the idea of string interpolation.

e.g. message $=$ "Hello there, the value of $x$ is $\$ x$ "

The value of variable $x$ is treated as and inserted in to the string.

Unquote is a similar operation, it interpolates ASTs rather than strings.

In the Julia language, the $\$$ ( expr ) operation is the syntax used for unquote, reflecting this. e.g
- julia $>:(s=\$(\sin (1)+\cos (1)))$ yields $:(s=1.3817732906760363)$

In LISP the syntax for this is more complicated

# LISP Backtick and Comma

Recall that the quote operator in LISP makes a symbol list (S-expression) from its expression argument.


Any symbol used to denote interpolation or unquote would be treated as the literal symbol.

In LISP the symbol use is a comma.

We would like the quoted expression

```LISP
' (add 1 ,(add 2 3))
```

... to mean the symbols (add 15) where the interpolated expression has been evaluated


However, using quote, actually converts this to the literal symbols:

In order to achieve the intended expression ...

```LISP
(add 1 , ( add 2 3 ) )
```

LISP supports an alternative quote operator

The \` (or backtick) quasiquotation operator allows for, to be used as
12 interpolation.

We can also use ,@for interpolation of a list of values

# Node Types of Quoted Code

An interesting aspect of using quoted code in a metaprogram is to understand what type of value the quote will evaluate to.

Quotes produce nodes in an AST.

For LISP and Julia there is essentially only type of tree node

>[!Tip]
>Actually it is more complicated in Julia with types Symbol and QuoteNode also

This makes for a nice simple view of the type of a quote.

For other languages, ASTs can have multiple node types, e.g. MethodDecl, ClassDecl, Expression, Statement, Identifier ...
The quote operator must return a node type that matches a grammatical entry point!

In order to maintain syntactic integrity, the context in which a quote is used in the meta program must be such that the value it returns is of the correct type of node. e.g.

```
VarDec id = `[ int i = 0; ] ;
Expr e = `[ if (#id) then 1 else 0 ] ; ✘
ClassDec c = `[ class Foo { #id } ]    ✔
```

>[!Tip]
>In general, we can declare the type of a quote, or infer it, or treat them uniformly.

# Quote as Representation

We said that metaprogramming involves both representation of code as data and manipulation of that representation.

Quote and unquote are largely concerned with the representation aspect of this.

What about manipulation of ASTs?
e.g. Traversal, Patten Matching, Rewrites?

Support for this is less consistent across languages and can actually be the harder part of metaprogramming.

A typical approach is to combine the use of macros with quote / unquote.

This is largely the approach taken in Rust - but it is way more complicated!

# The Quote Crate in Rust

This crate provides a macro called `quote`!

It is different to quote as outlined above as the quote macro takes a syntax tree as an argument and converts it to a `proc_macro2::TokenStream` ( iterator over a Token Tree !).

This token stream can then be passed to procedural macros for manipulation

There is an annoying conversion (Into::into or From::.from) needed as procedural macros use type `proc_macro::TokenStream` (why?)

These will output the token stream after some modification.

We then need to re-parse the resulting token stream to get back to an AST

This means we need access to a parser - we'll come back to this

# Interpolation in Rust Quotes

Inside a call to the quote! macro we can use the syntax \#var to interpolate the meta level of var and splice it in to the Token Stream.

This is valid for any type that implements the ToTokens trait.

There are also a number of special interpolation operations for variables containing a Vec, slice, BTreeSet, or any Iterator

```Rust
#(#var)* — no separators
#(#var),* — the character before the asterisk is used as a separator
#( struct #var; )* — the repetition can contain other tokens
#( #k => println!("{}", #v), )* — even multiple interpolations
```

>[!Tip]
>Note that quoted code just returns Rust values and as such can be combined and used in interpolation

```Rust
let type_definition = quote! {...};
let methods = quote! {...};

let tokens = quote! {
	#type_definition
	#methods
};
```

# The Syn Crate in Rust

This crate provides a parsing library for Rust token trees.

It provides the Data Type of Abstract Syntax Trees

It provides a number of parsing functions (from Token Streams, from Files, from Strings)

Used in combination with the quote crate this allows us to move smoothly between parse trees and token trees.

Crate syn also provides a macro parse_quote! that quotes a piece of Rust code, infers the grammar entry point of the tokens produced and then parses them back to an AST.

Used with interpolation this is effectively quasiquotation in Rust

```Rust
use quote::quote;
use syn::{parse_quote, Stmt};

fn main() {
	let name = quote!(v);
	let ty = quote!(u8);
	
	let stmt: Stmt = parse_quote! {
		let #name: #ty = Default::default();
	};
	
	println!("{:#?}", stmt);
}
```