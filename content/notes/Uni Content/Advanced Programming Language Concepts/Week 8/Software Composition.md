---
title: "Software Composition"
---

# Problems with Inheritance

- Tight Coupling - child classes are dependent on the implementation of the parent class!
- Fragile Base - changes to the base (parent) class can cause problems in descendant classes. Perhaps even in third party code.
- Inflexible Hierarchy - with single ancestor hierarchies, over time and evolution, all class taxonomies are eventually wrong for new use-cases.
- Duplication by Necessity - because of inflexibility, new use cases often lead to duplication of code in similar classes. This can cause divergence (forks) and make it difficult to understand which class new classes should inherit from.
- Gorilla / Banana - "...the problem with object-oriented languages is they've got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle." Joe Armstrong, Coders at Work

# Composition over Inheritance

Different composite structures create different semantic relationships between objects - tight coupling is generally considered a bad thing.

The composition over inheritance principle says that polymorphism should be achieved by using interfaces to represent behaviours. Concrete classes are added to the business domain by implementing the identified interface without necessarily becoming a subclass or inheriting behaviour

## Example

```C++
class Object
{
	public:
		virtual void update() {/* no-op */}
		virtual void draw() {/* no-op */*}
		virtual void collide(Object objects[]) {/* no-op */}
};

class Visible : public Object
{
	Model* model;
	public:
		virtual void draw() override {/* code */}
};

class Solid : public Object
{
	public:
		virtual void collide(Object objects[]) override {/* code */}
};

class Movable : public Object
{
	public:
		virtual void update() override {/* code */}
};
```

(The Diamond Problem) For example, hard to implement:
- Player - Solid , Movable,Visible
- Cloud - Movable, Visible , not Solid
- Building - Solid, Visible , not Movable
- Trap - Solid , not Visible, not Movable

Using composition instead of inheritance:

```C++
class VisibilityDelegate
{
	public:
		virtual void draw() = 0;
};

class NotVisible : public VisibilityDelegate
{
	public:
		virtual void draw() override {/* no-op */}
};

class Visible : public VisibilityDelegate
{
	public:
		virtual void draw() override {/* code */}
};

class UpdateDelegate
{
	public:
		virtual void update() = 0;
};

class NotMovable : public UpdateDelegate
{
	public:
		virtual void update() override {/* no-op */}
};

class Movable : public UpdateDelegate
{
	public:
		virtual void update() override {/* code */}
};

class CollisionDelegate
{
	public:
		virtual void collide(Object objects[]) = 0;
};

class NotSolid : public CollisionDelegate
{
	public:
		virtual void collide(Object objects[]) override {/* no-op */}
};

class Solid : public CollisionDelegate
{
	public:
		virtual void collide(Object objects[]) override {/* code */}
};

class Object
{
	VisibilityDelegate* _v;
	UpdateDelegate* _u;
	CollisionDelegate* _c;

	public:
	Object(VisibilityDelegate* v,
		   UpdateDelegate* u,
		   CollisionDelegate* c)
	: _v(v)
	, _u(u)
	, _c(c)
	{}

	void update() {
		_u->update();
	}
	
	void draw() {
		_v->draw();
	}

	void collide(Object objects[]) {
		_c->collide(objects);
	}
};
```

Example usage:

```C++
class Player : public Object
{
	public:
		Player()
			: Object(new Visible(), new Movable(), new Solid())
		{}

	// ...
};

class Smoke : public Object
{
	public:
		Smoke()
			: Object(new Visible(), new Movable(), new NotSolid())
		{}

	// ...
};
```

# Giving up Inheritance

Of course, there are drawbacks to using this approach.

Inheritance is good for avoiding having to implement all of the methods in the derived classes.
- cf. the no-op implementations in the example above.

This drawback is easily avoided using language support though
- C\# and Java - both since v8, can supply default implementations in interfaces.
- Go uses type embeddings to mimic inheritance
- Dart uses mixins (see below)
- Julia uses macros to generate forwarding methods
- Scala uses "export" clauses to generate aliases for methods
- Rust uses traits (more to come)

# Patterns

The Gang of Four Design Patterns book contains lots of patterns that deal with object composition from a structural point of view.
Let's have a look at two of these.
A Decorator is itself a Component and also contains a reference to a Component.

Concrete Components can be "decorated" by wrapping Components
Calls of base methods are delegated to the wrapped Component.

The decorator adds extra functionality as needed

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504164512.png|300]]

# Static Decorators in C++

C++ templates allow for a static approach to decorators by inheriting from the template parameter!

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504171619.png|500]]

# The Composite Pattern

The Composite pattern takes a similar approach to composition in the Decorator pattern in that a Composite is a Component but also contains references to an aggregation of Components

![[notes/Uni Content/Advanced Programming Language Concepts/Images/Pasted image 20230504171811.png|300]]

The idea is to recursive build a tree hierarchy in which individual components or collections of these components can be treated uniformly.

Composite components delegate to each of their referenced components - down the tree.

Decorators seem to be an example of this with singleton aggregations.

But differently, decorators encourage delegation

# Delegation, Aggregation and Concatenation

The three main approaches to software composition are in fact delegation, aggregation and concatenation.

We have seen examples of delegation and aggregation in the two patterns above.

There has been less focus on Concatenation historically as the main $\mathrm{OO}$ languages don't support it.

JavaScript however makes extensive use of dynamic types for objects and object concatenation either through the spread operator ...

```JavaScript
let person = {
	firstName: 'John',
	lastName: 'Doe',
};

let address = {
	email: 'jd@gmail.com',
	location: 'UK'
};

let employee = {
	...person,
	...job
};

let friend =
	Object.assign(person, job);
```

or Object.assign()

# Mixins

- Mixins are a form of object composition that avoids the "is a" relationship that comes with inheritance.
- Component features are mixed together to form a composite object.
- Terminology comes from ice-cream shop idea of vanilla as base flavour with several toppings that can be mixed in.
- Mixins are included rather than inherited to avoid the diamond problem - exactly how is language dependent.
- A bit like interfaces with implementations of their declared methods but this view suffers from dependency inversion
- Really useful for re-using components without forcing a hierarchical relation between them.
- First appeared in Flavors (early 80s) and Common Lisp
- Support now in many mainstream languages via explicit mixin support, default interfaces, delegates and traits

Example of Mixin code by using object concatenation in JavaScript:

```JavaScript
const chocolate={ hasChocolate: () => true };

const caramel ={ hasCaramel: () => true };

const pecans={ hasPecans: () => true };

const vanilla = {};

const iceCream=Object.assign(vanilla,chocolate, caramel,pecans);

console.log(`
	hasChocolate: ${ iceCream.hasChocolate() }
	hasCaramel: ${ iceCream.hasCaramel() }
	hasPecans: ${ iceCream.hasPecans() }
`);
```

A major criticism of mixins is that they don't scale well - conflicts, and lack of transparency regarding where functionality is coming from

# Functional Mixins

In the example above, we created mixin objects by creating the mixin objects and using dynamic extension

An alternative style is to provide functions that accept the object to be mixed into and the function extends the behaviour

```JavaScript
const addName = o => {
	let name = "";

	return Object.assign({},o,{
		getName(){
			return name;
		},
		setName(newName){
			name = newName;
			return this;
		}
	});
};
```

```JavaScript
const addHello = str => o => {

	return Object.assign({},o,{
		sayHello(name){
			return "Hello, my $str is $name";
		}
	});
};
```

```JavaScript
const helloSailor = addHello("NickName")(addName({}))
let name = helloSailor.setName("Sailor").getName();
let output = helloSailor.sayHello(name);
```

This leverages standard function composition to compose objects as mixins

