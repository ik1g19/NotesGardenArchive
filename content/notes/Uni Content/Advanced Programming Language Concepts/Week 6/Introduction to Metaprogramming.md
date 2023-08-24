---
title: Introduction to Metaprogramming
---
# Limitations of Library Re-use

These re-use methods have limitations
- Encapsulation can prevent optimisation
- Can make (static) error checking difficult - error reporting may not suit the software domain
- Library Scaling can be a problem (the Python Standard Library contains over 200 modules!)

## Causes of Limitations

Poor abstractions - not domain specific to the problem
Components bound to core Functionality
- What about secondary concepts e.g. persistence, security, distribution?

Host language restrictions - Java libraries are called using Java syntax
- Sometimes domain specific notation is better e.g. query languages, regexes, mathematical operators

# Metaprogramming

**Idea** - Write programs to write routine code
- Model programs themselves as data objects and write programs to manipulate these data objects

This is already common practice
- Compilers, interpreters, pre-processors, lexer/parser generators, CASE tools, GUI builders 
- But is often invisible to the mainstream programmer

## Common Approaches to Metaprogramming

#### Direct  
- Use string manipulation to write code directly  
- Low overhead to use but difficult to program with and very fragile

```Bash
/bin/sh
# metaprogram
echo ' # ! / bin/sh' > program
for i in $ (seq 992)
do
	echo "echo $1" >> program
done
chmod +x program
```

#### Reflection
- e.g. Java API. Unwieldy to learn and use - representation far from the source code representation

```Java
Class obj = foo. getC1ass();
Method [] methods = obj.getDec1aredMethods();
for (Method m : methods) {
	System. out. print ("Method Name: " + m.getName() );
	int modifier = m.getModifiers();
	System.out.print ("Modifier :" + Modifier.toString(modifier) );
	System.out.print ("Return Types :" + m. getReturnType() );
	System.out.println("");
}
```

#### Metaclasses
- Every class has type of the metaclass type
- In e.g. Python metaclasses are modifiable! By overriding

```Python
class AttributeInitType(type):  
	def __call__(self, *args, **kwargs):  
		"""Create a new instance."""  
		
		# First, create the object in the normal default way.  
		obj = type.__call__(self, *args)  
		
		# Additionally, set attributes on the new object.  
		for name, value in kwargs.items():  
			setattr(obj, name, value)  
			
		# Return the new object.  
		return obj
```

```Python
class Car(object, metaclass=AttributeInitType):  
	@property  
	def description(self) -> str:  
		"""Return a description of this car."""  
		return " ".join(str(value) for value in self.__dict__.values())
```

```Python
new_car =  
Car(make='Toyota',  
	model='Prius',  
	year=2005,  
	color='Green',  
	engine='Hybrid'  
)
```

#### Macro-based
- Named fragments of code used within code

#### Template-based
- Generic code that can be instantiated to have different behaviour based on the instantiation

#### Quote-based
- Transformations to move smoothly between parsed and unparsed source code


