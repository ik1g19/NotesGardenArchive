---
title: Gradual Typing
---
# Typing

**Static Typing** - Correctness of typing is checked at compile time
**Dynamic Typing** - Correctness of typing is checked at runtime
**Gradual Typing** - Combines both Static and Dynamic typing

# Typescript

TypeScript is JavaScript with gradual typing

# Generic Functions

```Typescript
function identity<X>(arg: X): X {
  return arg;
}
```

# Generic Types

```Typescript
type A<T> = (x: T) => T;
const  f: A<number> = function (y: number){
  return y + 7;
}
const  g: A<string> = function (y: string){
  return y + '!';
}
console.log(f(5));
console.log(g("Hello World"));
```

**Output**:
`[LOG]: 12 [LOG]: "Hello World!" `

# Union Type

```Typescript
type A = boolean | number; 

function f(x: number): A{
    return 55;
}
function g(x: boolean): A{
    return !x;
}

console.log(f(5));
console.log(g(true));
```

**Output**:
`[LOG]: 55 [LOG]: false `