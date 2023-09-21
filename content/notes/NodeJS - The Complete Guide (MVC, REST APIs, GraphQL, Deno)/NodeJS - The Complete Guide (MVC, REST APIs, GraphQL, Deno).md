NodeJS is a JavaScript runtime
- Built on top of JavaScript
- Allows you to run JavaScript code on the server, or anywhere else

JS allows you to change the webpage once it has been loaded

NodeJS uses V8
- The name of the JavaScript engine, built by Google
- Compiles JavaScript code to machine code
- Written in C++

NodeJS adds features to V8

![](notes/NodeJS%20-%20The%20Complete%20Guide%20(MVC,%20REST%20APIs,%20GraphQL,%20Deno)/Images/Pasted%20image%2020230920131200.png)

# JavaScript

## Let vs Var

1. **Scope**:
    
    - **`var`**: Declares a variable with function scope or globally (if it's declared outside of a function). This means if a variable is declared using `var` inside a function, it can't be accessed outside of that function. However, if it's declared inside a block (e.g., inside an `if` statement or a `for` loop), it can still be accessed outside of that block within the same function.
    - **`let`**: Declares a variable with block scope. This means the variable can't be accessed outside the block in which it is contained. This makes `let` more predictable in structures like loops and conditionals.
2. **Hoisting**:
    
    - **`var`**: Variables declared with `var` are hoisted to the top of their scope. This means the variable declaration is moved to the top, but the initialization remains where you wrote it. If you try to access the variable before it's initialized, you'll get `undefined`.
    - **`let`**: Variables declared with `let` are also hoisted, but you can't access them before the declaration in the code. Trying to do so will result in a `ReferenceError`.
3. **Re-declaration in the same scope**:
    
    - **`var`**: Allows re-declaring the same variable multiple times in the same scope without an error.
    - **`let`**: Does not allow re-declaring the same variable in the same scope. Doing so will result in a syntax error.
4. **Global Object Property**:
    
    - **`var`**: When you declare a global variable using `var` (i.e., outside of any function), it's added as a property of the global object (like `window` in browsers).
    - **`let`**: When you declare a global variable using `let`, it is not added as a property of the global object.
5. **Temporal Dead Zone (TDZ)**:
    
    - **`var`**: Doesn't have a TDZ. You can access a `var` variable before its declaration, but it will be `undefined`.
    - **`let`**: Has a TDZ. If you try to access a `let` variable before its declaration, you'll get a `ReferenceError`, even though it's technically hoisted.

Given these differences, `let` is generally recommended over `var` in modern JavaScript development because of its more predictable behaviour, especially with block-level scoping

## Arrow Functions

```JavaScript
const summarizeUser = (userName, userAge, userHasHobby) => {
  return (
    'Name is ' +
    userName +
    ', age is ' +
    userAge +
    ' and the user has hobbies: ' +
    userHasHobby
  );
};
```

When the body is a single return statement:

```JavaScript
const add =(a,b) => a + b;
```

When there is only one argument:

```JavaScript
const addOne = a => a + 1
```

When there are no arguments:

```JavaScript
const addRandom = () => 1 + 2;
```

## Objects

```JavaScript
const person = {
  name: 'Max',
  age: 29,
  greet() {
    console.log('Hi, I am ' + this.name);
  }
};

person.greet();

```

Arrow notation would not work for greet

## Arrays and Array Methods

```JavaScript
const hobbies = ['Sports', 'Cooking'];

console.log(hobbies.map(hobby => 'Hobby: ' + hobby));
```

Array methods will return a new array

So calling `hobbies` again will return the original array

You can push to an array that is const because the reference type has not changed

## Spread and Rest Operators

### Spread

```JavaScript
const copiedArray = [...hobbies]
```

Extracts the contents of the array and adds them to the surrounding structure, which in this case is another array

So in this scenario a copy of the array will be made

```JavaScript
const copiedPerson = {...person}
```

### Rest

Used to merge multiple arguments into an array

```JavaScript
const toArray = (...args) => {
	return args;
}
```

## Destructuring

Used to pull out elements from a structure by name or position

```JavaScript
const person = {
  name: 'Max',
  age: 29,
  greet() {
    console.log('Hi, I am ' + this.name);
  }
};

const printName = ({ name }) => {
  console.log(name);
};

printName(person);

const { name, age } = person;
console.log(name, age);
```

## Asynchronous Code

A callback function is a function that should be executed later

JavaScript recognises asynchronous code and will callback to it later

```JavaScript
setTimeout(() => {
	console.log('Timer is done!');
}, 1);

console.log('Hello');
```

`Hello` will be printed first since JS automatically recognises the asynchronous code

Creating a promise takes two arguments, `resolve` is when it is completed successfully and `reject` is when it fails - like it is throwing an error

`then` can be called on a function that returns a promise, its code will be executed once the promise is resolved

You can nest callbacks by continuing to return promises and calling `then` on each

```JavaScript
const fetchData = () => {
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Done!');
    }, 1500);
  });
  return promise;
};

setTimeout(() => {
  console.log('Timer is done!');
  fetchData()
    .then(text => {
      console.log(text);
      return fetchData();
    })
    .then(text2 => {
      console.log(text2);
    });
}, 2000);

console.log('Hello!');
```

## Template Literals

Dynamically add data into strings by using backticks \`

```JavaScript
const name = "Max";
const age = 29;
console.log(`My name is ${name} and I am ${age} years old.`);
```

# NodeJS

## Creating a Server

Create a server with `createServer`

```Node
const http = require('http');

const server = http.createServer((req, res) => {
	console.log(req);
});

server.listen(3000)
```

`createServer` accepts a function with two parameters, request and response
- This is the request and how the server should respond

Then calling `listen` will start the event loop on the specified port

## Understanding Requests

Headers in a http request contain metadata about the request

```Node
req.url
```

## Sending Responses

```Node
const server = http.createServer((req,res) => {
	console.log(req.url, req.method, req.headers);

	res.setHeader('Content-Type', 'text/html');
	res.write('<html>');
	res.write('<head><title>My First Page</title></head>');
	res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
	res.write('</html>');
	res.end();
});

server.listen(3000);
```

## Routing Requests

```Node
const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;
  if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title><head>');
    res.write('<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>');
    res.write('</html>');
    return res.end();
  }
  if (url === '/message' && method === 'POST') {
    fs.writeFileSync('message.txt', 'DUMMY');
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
});

server.listen(3000);
```

`302` is a redirect status code

## Parsing Request Bodies

![](notes/NodeJS%20-%20The%20Complete%20Guide%20(MVC,%20REST%20APIs,%20GraphQL,%20Deno)/Images/Pasted%20image%2020230920144619.png)

`on()` allows us to listen for certain events

```Node
...
if (url === '/message' && method === 'POST') {
    const body = [];
    req.on('data', (chunk) => {
      console.log(chunk);
      body.push(chunk);
    });
    req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFileSync('message.txt', message);
    });
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
...
```

The request body is read in chunks

On finishing reading the last chunk `end` is executed

The parsed body is then concatenated together

## Understanding Event Driven Code Execution

Sometimes functions passed as parameters will be executed asynchronously (later)

## Single Thread, Event Loop and Blocking Code

![](notes/NodeJS%20-%20The%20Complete%20Guide%20(MVC,%20REST%20APIs,%20GraphQL,%20Deno)/Images/Pasted%20image%2020230920150931.png)

![](notes/NodeJS%20-%20The%20Complete%20Guide%20(MVC,%20REST%20APIs,%20GraphQL,%20Deno)/Images/Pasted%20image%2020230920151347.png)

`refs` increments by 1 for every new callback that is registered, and reduces it by 1 for every event listener it doesn't need anymore

## Using Node Modules

`app.js`

```Node
const http = require('http');

const routes = require('./routes');

console.log(routes.someText);

const server = http.createServer(routes.handler);

server.listen(3000);
```

`routes.js`

```Node
const fs = require('fs');

const requestHandler = (req, res) => {
  const url = req.url;
  const method = req.method;
  if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title></head>');
    res.write(
      '<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>'
    );
    res.write('</html>');
    return res.end();
  }
  
  if (url === '/message' && method === 'POST') {
    const body = [];
    req.on('data', chunk => {
      console.log(chunk);
      body.push(chunk);
    });
    return req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFile('message.txt', message, err => {
        res.statusCode = 302;
        res.setHeader('Location', '/');
        return res.end();
      });
    });
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
};

// module.exports = requestHandler;

// module.exports = {
//     handler: requestHandler,
//     someText: 'Some hard coded text'
// };

// module.exports.handler = requestHandler;
// module.exports.someText = 'Some text';

exports.handler = requestHandler;
exports.someText = 'Some hard coded text';
```

## Summary

![](notes/NodeJS%20-%20The%20Complete%20Guide%20(MVC,%20REST%20APIs,%20GraphQL,%20Deno)/Images/Pasted%20image%2020230920152401.png)