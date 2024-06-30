---
theme: moon
enableMenu: false
controls: false
mouseWheel: true
previewLinks: true
---

<style>
    .slide h1, .slide h2, .slide h3, .slide h4, .slide h5, .slide h6 {
        text-transform: none;
    }

    .col {
        display: grid;
        grid-auto-flow: column;
    }

    .left {
        text-align: left;
    }

    .cite {
        display: inline-block;
        width: fit-content;
        font-size: 0.6em;
        border-top: 1px solid #ccc;
        line-height: 1.5;
        margin-top: 3em;
    }
    .cite:before {
        content: "📖 ";
    }
</style>

## JavaScript Quick Start
### for Python Developers

---

### JavaScript Versions

- JavaScript is officially called ECMAScript
  - ECMA is the organization that maintains the js standard

---

- The standard has gone through [six major versions](https://www.w3schools.com/js/js_versions.asp)

- Most versions were backwards compatible
  - except for ES5 (2009), which introduced a backwards incompatible [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)
  - and then ES6 (2015) introduced a lot of cool new syntax and ushered in a new era we call "modern JavaScript"

---

- Every year since 2015 we get an updated version of the standard with new features
  - but usually there is a lag in browser support

---

### Objects

- js is object-oriented, but not in the classical sense
- objects are not necessarily instances of classes

[https://javascript.info/object]() <!-- .element: class="cite" -->

---

#### objects are collections of key-value pairs

```js
// `person` is an object with three properties
person = {
  name: 'Jim',
  age: 18,
  hobbies: ['sports', 'coding']
};

// accessing object properties
person.name; //=> 'Jim'

// objects are open for modification
person.name = 'Dimitris'; // Update a property
person.gender = 'male'; // Add a new property
```

---

where in python we would use a dictionary \
in js we use an object

---

but of course objects can have methods too

```js
person = {
  name: 'Jim',
  age: 18,
  hobbies: ['sports', 'coding'],
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};
```

---

### Variable declarations

```js
x = 5; // global variable -- avoid
var y = 10; // old-style local variable -- not recommended
let y = 10; // local variable
const z = 15; // local variable protected from reassignment
```

---

##### const

const offers protection against reassignment, but it does not make the variable immutable.

```js
const person = { name: 'Jim' };
person.name = 'Dimitris'; // allowed
person = { name: 'Dimitris' }; // not allowed

const arr = [1, 2, 3];
arr.push(4); // allowed
arr = [1, 2, 3, 4]; // not allowed
```

---

- Declare all variables with `const` or `let`
- Always prefer `const` for variables that are not going to be reassigned


[https://javascript.info/variables]() <!-- .element: class="cite" -->


---

### Function declarations

<article class="col">

<section>

##### Javascript

```js
// named function
function add(a, b) {
  return a + b;
}
```

```js
// arrow function
const add = (a, b) => a + b;

```

```js
// anonymous function
const add = function(a, b) {
  return a + b;
};
```

</section>

<section>

##### Python

```python
# named function
def add(a, b):
    return a + b

```

```python
# lambda
add = lambda a, b: a + b

```

```python

# no python equivalent


```

</section>

</article>

---

https://javascript.info/function-expressions <!-- .element: class="cite" -->

https://javascript.info/arrow-functions-basics <!-- .element: class="cite" -->

---

### Destructuring

<article class="col">

<section>

##### Javascript

```js
// array destructuring
const arr = ['John', 'Doe'];
const [firstname, lastname] = arr;

console.log(firstname); //=> 'John'
console.log(lastname); //=> 'Doe'
```

```js
// object destructuring
const person = {
    name: 'John',
    age: 30
};
const { name, age } = person;

console.log(name); //=> 'John'
console.log(age); //=> 30
```

</section>

<section>

##### Python

```python
# list unpacking
arr = ['John', 'Doe']
firstname, lastname = arr

print(firstname) #=> 'John'
print(lastname) #=> 'Doe'
```

```python





# no equivalent feature



```
</section>

</article>

---

[https://javascript.info/destructuring-assignment]() <!-- .element: class="cite" -->

---

#### spread operator (`...`)

Same as python's asterisk operator (`*`)


<article class="col">

<section>

##### Javascript

```js
// array destructuring
const arr = [1,2,3,4,5];
const [one, two, ...rest] = arr;

console.log(one); //=> 1
console.log(two); //=> 2
console.log(rest); //=> [3,4,5]
```

```js
// array concatenation
const middle = [2,3,4];
const arr = [1, ...middle, 5];

console.log(arr); //=> [1,2,3,4,5]
```

</section>

<section>

##### Python

```python
# list unpacking
arr = [1,2,3,4,5]
one, two, *rest = arr

print(one) #=> 1
print(two) #=> 2
print(rest) #=> [3,4,5]
```

```python
# list packing
middle = [2,3,4]
arr = [1, *middle, 5]

print(arr) #=> [1,2,3,4,5]
```

</section>

</article>

---

```js
// object destructuring
const person = {
    name: 'John',
    age: 30,
    nationality: 'US',
    married: true
};
const { name, nationality, ...demographics } = person;

console.log(name); //=> 'John'
console.log(nationality); //=> 'US'
console.log(demographics); //=> { age: 30, married: true }
```

---

```js
// object merging
const name = "John";
const nationality = "US";
const demographics = {
    age: 30,
    married: true
};
const person = { name, ...demographics, nationality };

console.log(person); //=>
// {
//    name: 'John',
//    age: 30,
//    married: true,
//    nationality: 'US'
// }
```

---

### Promises

(I promise you, this is not as complicated as it seems)

---

In most javascript code, you will see the keywords `async` and `await` used together.

What is the deal with that?

---

- Javascript was designed to make HTML pages interactive
    - user actions (e.g. clicking, scrolling etc) trigger events
    - events are handled by javascript functions called event handlers

[https://javascript.info/events]() <!-- .element: class="cite" -->

---

Imagine a webpage where clicking a button triggers an event handler that fetches data from the server. This could take a few seconds. <!-- .element: class="left" -->

Imagine if during those seconds the browser was unresponsive (e.g. you couldn't scroll, and you couldn't click on other buttons). That would be terrible. <!-- .element: class="left" -->

To avoid this, javascript was designed to be asynchronous by default. <!-- .element: class="left" -->

---

In most programming languages, to make an operation asynchronous, you run the operation in a separate thread. <!-- .element: class="left" -->

But launching multiple threads simultaneously can be expensive in terms of memory and CPU usage. <!-- .element: class="left" -->

Imagine a webpage with 100 interactive elements, each with its own event handler. If each event handler was running in a separate thread, the browser would quickly run out of resources. <!-- .element: class="left" -->

---

So javascript came up with an interesting solution:
- All potentially time-consuming operations would be asynchronous
- But they would all run in a single thread
- When an asynchronous operation was triggered, it would be added to a queue
- The interpreter would run in a continuous loop, processing the queue one operation at a time, until the queue was empty

This is called the event loop.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop <!-- .element: class="cite" -->

---

Why is this important to you, the programmer?  <!-- .element: class="left" -->

See, when you call an asynchronous function, the function doesn't return the result, like in most languages.  <!-- .element: class="left" -->

Instead, it simply enqueues the operation in the event loop and immediately returns special object called a Promise.  <!-- .element: class="left" -->

A Promise object is like a placeholder for the result, which will be available in the future.  <!-- .element: class="left" -->

---

So what do you do with a promise?  <!-- .element: class="left" -->

Usually, you await it. "Awaiting" means that you ask the interpreter to  <!-- .element: class="left" -->
- put your code to sleep until the result is available
- then resume your code, having replaced the promise with its result

---

Here is an example: fetching data from a server


```js
const employeesUrl =
  "https://dummy.restapiexample.com/api/v1/employees";
const response = await fetch(employeesUrl);
const { data } = await response.json();
console.log(data.length)
```

---

All functions that need to use `await` \
must be declared as `async`

```js
async function employeeCount() {
    const employeesUrl =
      "https://dummy.restapiexample.com/api/v1/employees";
    const response = await fetch(employeesUrl);
    const { data } = await response.json();
    return data.length;
}
```

---

All functions declared as `async` \
implicitly and automatically return a promise.

So they must be called with `await`.

```js
console.log(await employeeCount())
```

---

[https://javascript.info/async-await]() <!-- .element: class="cite" -->

---

### Modules

- Once upon a time, javascript did not provide a way to split code into multiple files, because this was not needed in the browser

- ES6 introduced the `import` and `export` keywords

---

```js
// mymodule.js
export function add(a, b) {
    return a + b;
}
```

```js
// main.js
import { add } from './mymodule.js';
console.log(add(3, 4)); //=> 7
```

[https://javascript.info/import-export]() <!-- .element: class="cite" -->
