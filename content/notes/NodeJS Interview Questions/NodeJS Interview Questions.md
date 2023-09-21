#### Why might you need a C Compiler for some NodeJS Modules

NodeJS is primarily JavaScript, but some modules might have parts written in C or C++ for performance or to interface with system-level APIs

These are called **native modules**

When installing these modules with npm, they might need to be compiled for your specific system

`node-gyp` is a cross-platform command line tool for compiling native addon modules for NodeJS
- It requires a C/C++ toolchain to work

#### How can I verify a library is safe to use that I am using with Node

npm provides some security insights

- `npm audit` - Running `npm audit` in the project directory reviews the projects dependencies and reports known vulnerabilities
- **External Reviews & Security Advisories**: Sites like Snyk or NodeSource's Certified Modules can provide more insights into a package's safety

#### What is the NodeJS event loop and how does it work

When NodeJS performs an IO operation, instead of waiting for the operation to complete, it continues executing subsequent code

Once the Io operation is finished, the callback associated with it is added to the Event Queue

The Event Loop constantly check the Call Stack, if the Call Stack is empty it dequeues the callback from the Event Queue and pushes it to the Call Stack to be executed

#### What are Streams in NodeJS and why are they useful

Streams are objects that allow reading data from a source or writing data to a destination continuously

They are useful for handling large amounts of data because you don't need to load the entire data into memory before processing it

The four types of streams in NodeJS:
- Readable
- Writeable
- Duplex - both readable and writeable
- Transform - A type of duplex stream where the output is computed based on the input

#### Explain the differences between `async/await` and promises in handling asynchronous operations

Both `async/await` and promises are constructs in JavaScript to handle asynchronous operations

- Promises - Represent a value that might be available now, or in the future, or never
	- Promises have three states: pending, fulfilled and rejected
	- We used `.then()` to handle resolved values and `.catch()` to handle errors
- `async/await` - Syntactic sugar on top of Promises, that makes asynchronous code look and behave more like synchronous code
	- An `async` function always returns a promise, and using `await` inside it makes the function wait until the promise resolves or rejects

#### What is the difference between `exports` and `module.exports`

Every file is treated as a module, and the variables or functions defined the file are private to that module unless explicitly exported

Both `exports` and `module.exports` are objects provided by Node to expose functionalities from one module to another

- `exports` is a reference to `module.exports` - it is a shorthand to add properties to `module.exports`, however if you assign a new value to `exports`, it will no longer be a reference to `module.exports`
- `module.exports` is the real object that will be exported when another module imports the current module

