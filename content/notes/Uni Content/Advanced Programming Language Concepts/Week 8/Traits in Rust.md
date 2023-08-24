---
title: "Traits in Rust"
---

# What is a Trait

A trait is a way of grouping method/function signatures together and providing and to define their behaviours.

Isn't this just an interface?
- No, traits may contain implementations of the methods Isn't this just interfaces with default implementations?
- No, an object implementing a trait does not signify an "is a" relationship with the trait.

Isn't this just a mixin then?
- No, mixins can contain state - traits
- No, mixins use implicit resolution of the delegated calls

# Implicit Conflict Resolution in Mixins

Where an object is composed from several mixins, there may be name clashes between the mixed in behaviours.

In use of mixins there needs to be a way to resolve such a conflict.

A typical solution (C++, Python, JavaScript) is to use the order in which the mixins are applied:
- object class, then mixins in program order, then parent

In this example, `A::foo` would be called as foo is not defined in $\mathrm{C}$

In Java, this example (where the mixins are interfaces) this would be a compiler error.

In case of conflict, Rust requires that we explicitly call the appropriate trait method `A::foo` or `B::foo`

# Example Trait in Rust

To define a Trait in Rust we use the trait keyword and provide a struct like definition containing the declared methods/functions

These may optionally contain an implementation for each declared function

```Rust
pub trait Example {
	fn string(&self) -> String;
	
	fn default(&self) -> String {
		format!("the default")
	}
	
	fn partial(&self) -> String {
		format!("Here is extra string to {}", self.default())
	}
}
```

To include the behaviour of a trait in a struct-like type we use the impl-for keyword.

This requires us to name the trait that we are implementing and the struct to associate the implementation with

```Rust
pub struct Bar {
	pub bar_val : String
}

impl Example for Bar {
	fn default(&self) -> String {
		format!("the bar default, which is overridden")
	}

	fn string(&self) -> String {
		self.bar_val.to_string()
	}
}
```

```Rust
pub struct Foo {
	pub foo_val : String
}

impl Example for Foo {
	fn string(&self) -> String {
		self.foo_val.to_string()
	}
}
```

To use the trait behaviour you can simply call the functions as if they were a member of the struct they are associated with

```Rust
use traits_example::{Example,Foo,Bar};

fn main() {
	let foo = Foo {
		foo_val : String::from("Foo String")
	};
	let bar = Bar {
		bar_val : String::from("Bar String")
	};

	println!("Foo
		Call to string : {}
		Call to default : {}
		Call to partial : {}",
		foo.string(),
		foo.default(),
		foo.partial()
	);

	println!("Bar
		Call to string : {}
		Call to default : {}
		Call to partial : {}",
		bar.string(),
		bar.default(),
		bar.partial()
	);
}
```

# Trait Parameters

The "is a" relationship that comes with inheritance is useful for providing polymorphic methods.

How do we say that a methods should accept objects that have implementations of a particular Trait?

To do this we use the `&impI Trait` syntax

```Rust
fn must_have_example( ex : &impl Example ){ ... }
```

This is actually a short form of the more flexible Trait bounds syntax:

```Rust
fn must_have_example<T : Example> (ex : &T){ ... }
```

## Multiple Traits

What if we want to say that a parameter to a function should implement multiple traits

We use the `+` notation in the Trait bound

```Rust
fn must_have_example( ex : &impl (Example + OtherTrait) ){ ... }
```

This can get messy when there are many bounds e.g.

```Rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 { ... }
```

Rust provides a syntax sugar to help with this:

```Rust
fn some_function<T, U>(t: &T, u: &U) -> i32
where
	T: Display + Clone,
	U: Clone + Debug,
{ ... }
```

# Specifying a Return Type as a Trait

To specify that a function will return a type that implements a trait we can simply use the `impl` keyword again

```Rust
fn will_return_example() -> impl Example {
	Foo {
		foo_val : "I'm a foo"
	}
}
```

This above example is monomorphic, rust must statically determine which type is to be returned

```Rust
fn will_return_example() -> impl Example {
	if (...) then
		Foo {
		foo_val : "I'm a foo"
	}

	else
		Bar {
		bar : "I'm a bar"
	}
}
```

>[!Tip]
>This will fail to type check - remember that traits are not an "is a" relationship
>
>It is possible to make this example type check by declaring that the function returns something called a "trait object" and using dynamic dispatch on the delegates

# Conditional Implementations using Trait Bounds

Suppose we have a generic struct and a generic implementation of a function on that struct.

We might want to specify that the generic type parameter should satisfy a trait bound.

Now, the generic implementation is only conditionally defined for types that satisfy the bound.

Duplicate definitions are not allowed though

```Rust
struct Pair<T> {
	x: T,
	y: T,
}
impl<T> Pair<T> {
	fn new(x: T, y: T) -> Self {
		Self { x, y }
	}
}
```

```Rust
impl<T: Display + PartialOrd> Pair<T> {
	fn cmp_display(&self) {
		if self.x >= self.y {
			println!("The largest member is x = {}", self.x);
		} else {
			println!("The largest member is y = {}", self.y);
		}
	}
}
```

# Blanket Implementations

Suppose we want to implement a trait for any type that implements another trait

This is what we call a blanket implementation

These are used extensively across the standard library.

For example, the ToString trait is implemented this way by leveraging the implementations in the Display trait

```Rust
impl<T: Display> ToString for T {
	// --snip--
}
```

# Associated Types in Traits

An interesting feature that traits can support is the ability to declare a "placeholder" types in their definition.

The trait can be defined with respect to this placeholder type, the concrete instance of which is then provided by the implementation of the type.

The Iterator trait in Rust is defined using this feature

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230505201709.png|450]]

Why not just use generic parameters e.g.:

```Rust
pub trait Iterator<T> {
	fn next(&mut self) -> Option<T>;
}
```

Using a generic parameter would then allow me to implement this trait for a given struct several times, at potentially different types

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507183225.png|500]]

In order to select which Iterator implementation to use for String, I would then need to specify it explicitly as, say, `Iterator::<char>::next()`
Using an associated type only lets me implement it once, which obviates the need to specify the generic parameter whenever I use it

# Fully Qualified Syntax

In order to select the correct implementation for a call to a struct we will occasionally have to explicitly say which implementation to use.

e.g. if a struct implements a method/function and a method/function of the same signature is included from a trait then we need to identify which call we intend.

By default, the struct implementation will be used in preference to a trait implementation method/function.

In order to call the trait implementation method/function we need to specify this - however this is not always straightforward.

For associated functions (where there is no self parameter) the function name alone called directly in the trait is not sufficient to identify which implementation to use as it doesn't specify which struct type we are referring to.

In this case, we need both the struct name and the trait name.

There is a special syntax to allow us to do this <struct as trait>

The example overleaf shows the a method and a function call in this scenario

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230507183830.png]]

