# Concepts

- [NodeJS](content/concepts/NodeJS.md)
- [JavaScript](JavaScript.md)

---

NodeJS is a JavaScript runtime
- Built on top of JavaScript
- Allows you to run JavaScript code on the server, or anywhere else

JS allows you to change the webpage once it has been loaded

NodeJS uses V8
- The name of the JavaScript engine, built by Google
- Compiles JavaScript code to machine code
- Written in C++

NodeJS adds features to V8

![](Pasted%20image%2020230920131200.png)

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

![](Pasted%20image%2020230920144619.png)

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

![](Pasted%20image%2020230920150931.png)

![](Pasted%20image%2020230920151347.png)

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

![](Pasted%20image%2020230920152401.png)

# Improved Development Workflow and Debugging

## Understanding NPM Scripts

You can create a `package.json` using `npm` so that you can run your program with just `npm start` 
## Installing 3rd Party Packages

Packages are installed from the npm repository with npm

We can indicate a dependency is a development dependency by appending `--save-dev` to the end

The `package-lock.json` contains the version information about the exact versions of the dependencies installed, in case the project is shared with others who also need to download the dependencies

## Using Nodemon for Autorestarts

Nodemon is a utility package that will watch our files for changes and restart our process if we make changes

## Global and Local npm Packages

The benefit of local dependencies is that you can share projects without the `node_modules` folder and you can run `npm install` in a project to re-create that node_modules folder

You could install a package globally with the `-g` flag

# Express.js

Simplifies server logic

Alternatives to Express:
- Adonis.js
- Koa
- Salis.js

import with `const express = require('express');`

Create the app with `express()`

The created app can be used as a request handler

```node
const app = express();
const server = http.createServer(app);
```

## Middleware

The function passed to `app.use((req, res, next) => {})` will be used to handle every request

`next` is a function that will be executed to allow the request to travel on to the next middleware

```node
app.use((req, res, next) => {
	console.log('In the middleware');
	next();
});

app.use((req, rest, next) => {
	console.log('Another middleware');
});
```

If `next` was not called then only the first middleware would be executed upon a request

`send()` is used to send responses (by default `text/html`)

```node
app.use((req, res, next) => {
	console.log('In the middleware');
	next();
});

app.use((req, rest, next) => {
	console.log('Another middleware');
	res.send('<h1>Test Header</h1>');
});
```

Instead of using:

```node
const server = http.createServer(app);
server.listen(3000);
```

We can use:

```node
app.listen(3000);
```

## Handling Different Routes

`app.use('/', (req, res, next) => {});` means that every routing starting with a `/` will be handled
- Not to be confused with exactly being the route `/`

So to handle a route whilst also handling the root path, you need to route the root path last

```node
app.use('/add-product', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>The "Add Product" Page</h1>');
});

app.use('/', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>Hello from Express!</h1>');
});
```

To have code that will execute every time:

```node
app.use('/', (req, res, next) => {
    console.log('This always runs!');
    next();
});

app.use('/add-product', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>The "Add Product" Page</h1>');
});

app.use('/', (req, res, next) => {
  console.log('In another middleware!');
  res.send('<h1>Hello from Express!</h1>');
});
```

## Parsing Incoming Requests

Package needed in order to parse requests:

```
npm install --save body-parser
```

And import with:

```node
const bodyParser = require('body-parser');
```

To then parse the request you pass it to the app handler:

```node
app.use(bodyParser.urlencoded({extended: false}));

app.use('/add-product', (req, res, next) => {
  res.send('<form action="/product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>');
});

app.post('/product', (req, res, next) => {
    console.log(req.body);
    res.redirect('/');
});

app.use('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});
```

`app.use` would be used for every request, regardless of if it was GET or POST

So to filter requests we use `app.get` or `app.post`

## Using Express Router

Typically we want to split our routing code over multiple files

Routing related code typically goes under the `routes` folder

Add `admin.js` and `shop.js`
- These will control routing for normal and admin users

Create an express router with `const router = express.Router()`

Use this to handle the admin requests in `admin.js`:

```node
app.use('/add-product', (req, res, next) => {
  res.send('<form action="/product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>');
});

app.post('/product', (req, res, next) => {
    console.log(req.body);
    res.redirect('/');
});

app.use('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});
```

And in `shop.js`:

```node
const express = require('express');

const router = express.Router();

router.get('/', (req, res, next) => {
  res.send('<h1>Hello from Express!</h1>');
});

module.exports = router;
```

We can then `require` the exported modules from the main app and `use` the routing:

```node
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

const adminRoutes = require('./routes/admin');
const shopRoutes = require('./routes/shop');

app.use(bodyParser.urlencoded({extended: false}));

app.use(adminRoutes);
app.use(shopRoutes);

app.listen(3000);
```

## Adding a 404 Page

We want to add a 'catch all' middleware at the bottom

```node
...
app.use(adminRoutes);
app.use(shopRoutes);

app.use((req, rest, next) => {
	res.status(404).send('<h1>Page not found</h1>');
})

app.listen(3000);
```

## Filtering Paths

You can filter by paths at the `use` level

```node
app.use('/admin', adminRoutes);
app.use(shopRoutes);
```

This means that any paths after this will be /admin/path

```node
router.get('/add-product', (req, res, next) => {
  res.send(
    '<form action="/admin/add-product" method="POST"><input type="text" name="title"><button type="submit">Add Product</button></form>'
  );
});

router.post('/add-product', (req, res, next) => {
  console.log(req.body);
  res.redirect('/');
});
```

It is not necessary to repeat /admin once it has been filtered

So the examples above are actually for /admin/add-product

## Creating and Serving HTML Pages

Create a folder called `views` to contain HTML files you want to serve

Example:

`add-product.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
</head>

<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Shop</a></li>
                <li><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <form action="/add-product" method="POST">
            <input type="text" name="title">
            <button type="submit">Add Product</button>
        </form>
    </main>
</body>

</html>
```

`shop.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
</head>

<body>
    <header>
        <nav>
            <ul>
                <li><a href="/">Shop</a></li>
                <li><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
    </main>
</body>

</html>
```

We can now serve these HTML pages using `sendFile`

By default `/` references the root directory on the operating system, so `path` is used to reference the current working directory

`admin.js`

```node
const path = require('path');

const express = require('express');

const router = express.Router();

// /admin/add-product => GET
router.get('/add-product', (req, res, next) => {
  res.sendFile(path.join(__dirname, '../', 'views', 'add-product.html'));
});

// /admin/add-product => POST
router.post('/add-product', (req, res, next) => {
  console.log(req.body);
  res.redirect('/');
});

module.exports = router;
```

`shop.js`

```node
const path = require('path');

const express = require('express');

const router = express.Router();

router.get('/', (req, res, next) => {
  res.sendFile(path.join(__dirname, '../', 'views', 'shop.html'));
});

module.exports = router;
```

## Serving File Statically

Create a folder `public` to hold all the files accessible to the client

This folder will hold css content for pages

Serving files **statically** - Serving files not through the router, but directly from the file system

Use:

```node
app.use(express.static(path.join(__dirname, 'public')));
```

To grant 'read access' (serve statically) the public folder

When referencing the stylesheet, you do not need to include /public as node will already be working within this folder as the folder `public` is being served

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Add Product</title>
    <link rel="stylesheet" href="/css/main.css">
</head>

<body>
    <header class="main-header">
        <nav class="main-header__nav">
            <ul class="main-header__item-list">
                <li class="main-header__item"><a class="active" href="/">Shop</a></li>
                <li class="main-header__item"><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>My Products</h1>
        <p>List of all the products...</p>
    </main>
</body>

</html>
```

## Summary

![](Pasted%20image%2020230925215649.png)

# Dynamic Content and Template

## Templating Engines

![](Pasted%20image%2020230925220915.png)

### Available Engines

![](Screenshot%20from%202023-09-25%2022-11-27.png)

## Installing and Implementing Pug

`npm install --save ejs pug express-handlebars`

`app.set` allows us to set a global configuration value

```node
app.set('view engine', 'pug');
```

The default locations for views is `/views/`

We can specify a custom location with:

```node
app.set('views', 'views');
```

Create `shop.pug` under `views/` - this will hold the template that pug will convert to HTML

`shop.pug`

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title My Shop
        link(rel="stylesheet", href="/css/main.css")
        link(rel="stylesheet", href="/css/product.css")
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a.active(href="/") Shop
                    li.main-header__item
                        a(href="/admin/add-product") Add Product
```

Since this is now using a templating engine, we don't use `sendFile`

We now use `render` (in `shop.js`):

```node
router.get('/', (req, res, next) => {
  res.render('shop');
});
```

## Outputting Dynamic Content

We can share variables between requests by exporting them (`admin.js`):

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');

const router = express.Router();

const products = [];

// /admin/add-product => GET
router.get('/add-product', (req, res, next) => {
  res.sendFile(path.join(rootDir, 'views', 'add-product.html'));
});

// /admin/add-product => POST
router.post('/add-product', (req, res, next) => {
  products.push({ title: req.body.title });
  res.redirect('/');
});

exports.routes = router;
exports.products = products;
```

And then requiring them (`shop.js`):

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');
const adminData = require('./admin');

const router = express.Router();

router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {prods: products, docTitle: 'Shop'});
});

module.exports = router;
```

We can pass dynamic content to the `render` function as a js object with key-value pairs

In this case we are passing a list of products, which hold a value `title`

We can then handle this content in `shop.pug`:

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title #{docTitle}
        link(rel="stylesheet", href="/css/main.css")
        link(rel="stylesheet", href="/css/product.css")
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a.active(href="/") Shop
                    li.main-header__item
                        a(href="/admin/add-product") Add Product

        main
            if prods.length > 0
                .grid
                    each product in prods
                        article.card.product-item
                            header.card__header
                                h1.product__title #{product.title}
                            div.card__image
                                img(src="link_to_image", alt="A Book")
                            div.card__content
                                h2.product__price $19.99
                                p.product__description A very interesting book about so many even more interesting things!
                            .card__actions
                                button.btn Add to Cart
            else
                h1 No Products
```

We reference a variable in pug using `#{}` e.g. `#{docTitle}`

We then iterate through objects in pug with `each`

The `if` statement is used to catch the case where no objects have been added

## Using Pug Layouts

Create a `layouts` subfolder under `views`

This will contain the main layout of every page

`main-layout.pug`

```
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title #{pageTitle}
        link(rel="stylesheet", href="/css/main.css")
        block styles
    body   
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a(href="/", class=(path === '/' ? 'active' : '')) Shop
                    li.main-header__item
                        a(href="/admin/add-product", class=(path === '/admin/add-product' ? 'active' : '')) Add Product
        block content
```

`block` tags represent spaces where other pug files can extend the template and insert their own custom content

Inline ifs are used to add the `active` class if the path of the page matches parameter `path` that is passed to the render function e.g. in `shop.js`

```node
router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {prods: products, pageTitle: 'Shop', path: '/'});
});
```

`add-product.pug`

```
extends layouts/main-layout.pug

block styles
    link(rel="stylesheet", href="/css/forms.css")
    link(rel="stylesheet", href="/css/product.css")

block content
    main
        form.product-form(action="/admin/add-product", method="POST")
            .form-control
                label(for="title") Title
                input(type="text", name="title")#title
            button.btn(type="submit") Add Product
```

`extends` is used to extend the pug template

Content is inserted into `block`s with the `block` tags

`404.pug`

```
extends layouts/main-layout.pug

block content
    h1 Page Not Found!
```

## Working with Handlebars

Uses normal HTML mixed with some templating logic

Importing:

```node
const expressHbs = require('express-handlebars');
```

Using:

```node
app.engine('hbs', expressHbs());
app.set('view engine', 'hbs');
```

Create a file with the extension of what you used in the above code, in this case `404.hbs`

Dynamic content is then passed through render as a key-value js object in the same way

Handlebar content is normal HTML code but dynamic content is represented with `{{}}`

```html
<title>{{ pageTitle }}</title>
```

Handlebars only supports True/False logic in its templating, so any calculations must be performed in js code and then passed to handlebar templating as a boolean

```node
res.render('shop', {prods: products, pageTitle: 'Shop', path: '/', hasProducts: products.length > 0})
```

```html
{{#if hasProducts}}
...
{{else}}
...
{{/if}}
```

You can iterate in handlebars with `each`

```html
{{#each prods}}
<h1 class="product_title">{{ this.title }}</h1>
{{/each}}
```

## Using Handlebar Layouts

`main-layout.hbs`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>{{ pageTitle }}</title>
    <link rel="stylesheet" href="/css/main.css">
    {{#if formsCSS}}
        <link rel="stylesheet" href="/css/forms.css">
    {{/if}}
    {{#if productCSS}}
        <link rel="stylesheet" href="/css/product.css">
    {{/if}}
</head>

<body>
    <header class="main-header">
        <nav class="main-header__nav">
            <ul class="main-header__item-list">
                <li class="main-header__item"><a class="{{#if activeShop }}active{{/if}}" href="/">Shop</a></li>
                <li class="main-header__item"><a class="{{#if activeAddProduct }}active{{/if}}" href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>
    {{{ body }}}
</body>

</html>
```

The only way to extend a layout is by inserting content into `{{{ body }}}`

So `if` statements have to be used to dynamically insert styles

e.g. `shop.js`:

```node
const path = require('path');

const express = require('express');

const rootDir = require('../util/path');
const adminData = require('./admin');

const router = express.Router();

router.get('/', (req, res, next) => {
  const products = adminData.products;
  res.render('shop', {
    prods: products,
    pageTitle: 'Shop',
    path: '/',
    hasProducts: products.length > 0,
    activeShop: true,
    productCSS: true
  });
});

module.exports = router;
```

Using handlebars in `app.js`:

```node
const path = require('path');

const express = require('express');
const bodyParser = require('body-parser');
const expressHbs = require('express-handlebars');

const app = express();

app.engine(
  'hbs',
  expressHbs({
    layoutsDir: 'views/layouts/',
    defaultLayout: 'main-layout',
    extname: 'hbs'
  })
);
app.set('view engine', 'hbs');
app.set('views', 'views');

const adminData = require('./routes/admin');
const shopRoutes = require('./routes/shop');

app.use(bodyParser.urlencoded({ extended: false }));
app.use(express.static(path.join(__dirname, 'public')));

app.use('/admin', adminData.routes);
app.use(shopRoutes);

app.use((req, res, next) => {
  res.status(404).render('404', { pageTitle: 'Page Not Found' });
});

app.listen(3000);
```

