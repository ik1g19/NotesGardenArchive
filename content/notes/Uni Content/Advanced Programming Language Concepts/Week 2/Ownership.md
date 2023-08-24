---
title: Ownership
---
Only one variable “owns” data at any given moment in time
You can see, but you cannot change something that you don’t own

```RUST
fn main() {  
	let a = 27;  
	let mut b = a;  
	b = b - 7;  
	println!("a={}, b={}", a, b);  
}
```

**Output**:
`a=27, b=20`

# Clone

```RUST
fn main() {  
	let mut a = String::from("Hello");  
	let mut b = a.clone();  
	a.push('!');  
	b.push('?');  
	println!("a={}, b={}", a, b);  
}
```

**Output**:
`a=Hello!, b=Hello?`

# Borrow

```RUST
fn main() {  
	let a = String::from("Hello");  
	let b = &a;  
	let c = &b;  
	println!("a={}, b={}, c={}", a, b, c);  
}
```

**Output**:
`a=Hello, b=Hello, c=Hello`

## When being Borrowed from, You Retain the Rights to Change

```RUST
fn main() {  
	let mut a = String::from("Hello");  
	let b = &a;  
	println!("a={}, b={}", a, b);  
	a.push('!');  
	println!("a={}", a);  
}
```

**Output**:
`a=Hello b=Hello a=Hello!`

## Borrower does not have the Right to Change

```RUST
fn main() {  
	let a = String::from("Hello");  
	let b = &a;  
	println!("a={}, b={}", a, b);  
	b.push('!');  
}
```

Results in an **error**

# Mutable Borrow

```RUST
fn main() {  
	let a = String::from("Hello");  
	let b = &a;  
	println!("a={}, b={}", a, b);  
	b.push('!');  
}
```

**Output**:
`b=Hello! a=Hello!`

# Dereferencing Primitive Types

```RUST
fn square_by_ref(n: &mut i32){
    *n = *n * *n;
}
fn main(){
    let mut n: i32 = 12;
    square_by_ref(&mut n);
    println!("n={}",n);
}
```

**Output**:
`n=144`

