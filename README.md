# JavaScript: The Weird Parts

Below is a list of notes made for the course JavaScript: The Weird Parts.

## Table of Contents
- [JavaScript: The Weird Parts](#javascript-the-weird-parts)
  * [01. Execution Contexts and Lexical Environments](#01-execution-contexts-and-lexical-environments)
    + [Syntax Parser](#syntax-parser)
    + [Lexical Environment](#lexical-environment)
    + [Execution Context](#execution-context)
    + [Name/Value Pair](#namevalue-pair)
    + [Object](#object)
    + [Hoisting](#hoisting)
    + [Phases of execution context inside JavaScript](#phases-of-execution-context-inside-javascript)
    + [JavaScript is single threaded, synchronous execution](#javascript-is-single-threaded-synchronous-execution)
    + [Invocation](#invocation)
    + [Execution Stack](#execution-stack)
    + [Variable environment](#variable-environment)
    + [Scope Chain](#scope-chain)
    + [Event Queue](#event-queue)
  * [02. Types and Operators](#02-types-and-operators)
    + [Dynamic Typing](#dynamic-typing)
    + [Primitive Type](#primitive-type)
    + [Operator](#operator)
    + [Operator Precedence](#operator-precedence)
    + [Associativity](#associativity)
    + [Coercion](#coercion)
    + [Short Circuiting](#short-circuiting)
    + [Frameworks](#frameworks)
  * [03. Objects and Functions](#03-objects-and-functions)
    + [Namespace](#namespace)
    + [First Class Functions](#first-class-functions)
    + [Expression vs Statement](#expression-vs-statement)
    + [Pass-by-value and pass-by-reference](#pass-by-value-and-pass-by-reference)
    + [Objects, Functions, and 'this'](#objects-functions-and-this)
    + ['arguments' and REST](#arguments-and-rest)
    + [Immediately Invoked Function Expressions (IIFE)s](#immediately-invoked-function-expressions-iifes)
    + [Closures](#closures)
    + [Function Factories](#function-factories)
    + [Callback Functions and Closures](#callback-functions-and-closures)
    + [Call, Apply, and Bind](#call-apply-and-bind)
    + [Functional Programming](#functional-programming)
  * [04. Object-Oriented JavaScript and Prototypal Inheritance](#04-object-oriented-javascript-and-prototypal-inheritance)
    + [Prototypal Inheritance](#prototypal-inheritance)
    + [Reflection and Extend](#reflection-and-extend)
  * [05. Building Objects](#05-building-objects)
    + [Function Constructors, 'new', and The History of JavaScript](#function-constructors-new-and-the-history-of-javascript)
    + [Function Constructors and '.prototypes'](#function-constructors-and-prototypes)
    + ['new' and Functions](#new-and-functions)
    + [Built-in Function Constructors](#built-in-function-constructors)
    + [Arrays and for ... in](#arrays-and-for--in)
    + [Object.create and Pure Prototypal Inheritance](#objectcreate-and-pure-prototypal-inheritance)
    + [ES6 and Classes](#es6-and-classes)

## 01. Execution Contexts and Lexical Environments
### Syntax Parser
- A program that reads your code and determines what it does, and if the
grammar is valid.

### Lexical Environment
- Where something sits physically in the code you write, the positioning, where
is it contained

### Execution Context
- A wrapper to help manage the code that is currently running
- The environment of the code being executed
- Basically the scope of the code
- An example:

```JavaScript
// global context

function a() {
  // a() itself is a execution context, and the global context is also an
  // execution context
  var myVar = 5;
}
```

### Name/Value Pair
- A name which maps to a unique value, can be defined more than once, but can
have only one value in any given context

### Object
- A collection of Name/Value pairs, a function also counts as a value
- If the value is a primitive, it's called a property.
- If the value is a function, it's called a method.

### Hoisting
- Setup memory space for variables and functions
- Memory space is allocated for functions and variables, but variables are not
yet defined. All values in JS are set initially to undefined.
- Avoid using hoisting. Always declared methods and variables before using them.

### Phases of execution context inside JavaScript
1. Creation of variables and functions in memory
2. Execution phase

### JavaScript is single threaded, synchronous execution
- Means that it can only execute one instruction at a time in the order that it
appears.
- Asynchronous events are actually handled synchronously.

### Invocation
- Running a function, invoking a function

### Execution Stack
- When the script is run, the global execution context is created, and is
executed.
- However, if there is another function invocation, it will stop at that line
of code, and create and execute the execution context.

### Variable environment
- Where the variables live, and how they relate to each other in memory

### Scope Chain
- A scope is Where a variable is available in your code, and if it's truly the
same copy, or a new one.
- Basically what scope contains what scope/variables
- If the variable is not found inside the execution context, it will search for
the variable inside the outer lexical environment. If it is not found inside
the inside the outer lexical environment, then it will go up the scope chain
until it finds the variable, or when it reached the global execution context.
- Note that just because your execution context is on top of another in the
scope chain, it does not mean that it the one on the bottom is necessarily its
parent.
- An example:

```JavaScript
// global context

function a() {
  /*
  Function b is sitting lexically inside function a, so when it's referring to
  myVar, if it is not found inside function b, it will go to the parent
  execution context, which is positioned inside the scope chain.
  */
  function b() {
    console.log(myVar);
  }

  b();
}

var myVar = 1;
a();
```

### Event Queue
- Beside the scope chain list, there is also another list, called the event
queue.
- The event queue is populated with events, or populated events that we want to
be notified of.
- We can listen for events, and let a function handle that specific event.
- The event queue is only periodically looked at when the execution stack is
empty.
- If an event is in the event queue, JS checks if there is a specific function
to handle that specific event.
- If there is function to handle an event, the function is added to the
execution stack.

## 02. Types and Operators
### Dynamic Typing
- The type of variable does not need to be defined, it is automatically
determined in runtime.
- The variables can hold different types of values, and the data stored can
even be changed after the variable is declared.

### Primitive Type
- A type of data that represents a single value.
- There are not objects as they do not contain Name-Value pairs.
- List of primitive data types:
  1. Undefined
    - ***undefined*** represents a lack of existence, you should not assign a
    variable to this.
  2. Null
    - ***null*** also represents a lack of existence, but you can set a
    variable to this.
  3. Boolean
    - ***boolean*** is either *true* or *false*
  4. Number
    - A ***number*** is a floating point number. There is only one type of
    floating type number inside JavaScript.
  5. String
     - A ***String*** is a sequence of characters, and single quotes and
     double quotes can both be used to contain strings.
    6. Symbol
      - A ***symbol*** is used in ES6

### Operator
- Is a special function that is syntactically different.
- JavaScript operators are infix notations.
- Operators are actually just functions.

### Operator Precedence
- Decides which operator function gets called first.

### Associativity
- Decides what order operator functions get called, be it left-to-right , or
right-to-left.
- [Mozilla Developer Network on Associativity](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Associativity)

### Coercion
- **Coercion** is converting a value from one data type to another.
- Also known as type casting.

### Short Circuiting
- Because logical expressions are evaluated from left to right, they are tested
for possible '**short-circuit**' evaluation using the following rules:
  - ***false*** && (anything) is short-circuit evaluated to ***false***
  - ***true*** || (anything) is short-circuit evaluated to ***true***
  - If the statement is evaluated to ***true***, the last operand will be
  executed.
- An example:

```JavaScript
3 === 3 && 'cow' && console.log('chicken');

// Chicken will be logged to the console because if the condition is true,
// the last operand will be executed.
```
- This is particularly useful when used in functions, because it allows for
default parameters.

```JavaScript
function greet(name) {
  name && console.log('Hi, ' + name + '!');
}

greet('Sam');
```
- However, you should take note that if you pass in a **falsey** value, such as
***undefined***, ***null***, or ***0***, the conditional statement will still
evaluate to false, even if you have passed something in.

```JavaScript
function plusOne(num) {
  num = num || 1;
  return num + 1;
}

// This statement will return 2, if you pass in a falsey value such as 0
plusOne(0);
```

### Frameworks
- When you include several JavaScript files inside a HTML file, the browser
does not actually create new execution contexts. Instead, the JavaScript files
must be executed in order.

## 03. Objects and Functions
### Namespace
- Is a container for variables and functions
- Uses an object in JavaScript

```JavaScript

var english = {};
var spanish = {};

english.greet = 'Hello!';
spanish.greet = 'Hola!';

```

### First Class Functions
- You can do everything to them that you can do with other types.
- E.g.
  - Being assigned to a variable
  - Passed around as an argument
  - Being created on the fly
- In JavaScript, a function is actually a special type of object, hence, we can
attach additional functions, variables, and even objects to it.
- Functions also have some hidden special properties:
  - ***name***: The name is optional, the function can be anonymous.
  - ***code***: The code inside the function is actually stored inside a code
  variable, this code variable is actually invocable.
- A function is actually just an object, whose code just happens to be one of
the properties attached to the object.

### Expression vs Statement
- An ***expression*** Is a unit of code that results in a value
- A ***statement*** a unit of code that does not result in a value
- E.g.

```JavaScript
// The function greet here is just a statement, because it does not return a
// value when evaluated.
function greet() {
  console.log('hi');
}

// This is an anonymous function, it is just a function without a name
// In this case, the function here is an expression, because it returns a
// value when evaluated, which is the function object
var anonymousGreet  = function() {
  console.log('hello');
}
```

### Pass-by-value and pass-by-reference
- Primitive data types are pass-by-value, whereas objects are pass-by-reference

### Objects, Functions, and 'this'
- When a function is invoked, a new execution context is invoked. When the
**code** 'property' is invoked, a new execution context is created, and put on
the execution stack. That determines how the code is executed.
- An execution context has:
  1. Variable Environment
  2. Outer Environment
  3. '***this***'
- The '***this***' keyword can point to different objects, and that depends on
where the function is and where it's called.
- When you're simply invoking a function, the ***this*** keyword inside will
always point to the global object, the **Window** object.
- If you're invoking a method inside a object, the ***this*** keyword will
point to the object itself.
- However, the '***this***' keyword when used inside a function inside a method
inside an object, will point back to the global object.

```JavaScript
// To be updated
var c = {
  name: 'The c object',
  log: function() {
    this.name = 'Updated c object';
    console.log(this);

    var setname = function(newname) {
      this.name = newname;
    }
    setname('Updated again! The c object');
  }
}
c.log();

```

### 'arguments' and REST
- **Arguments** are the parameters that you pass to a function
- When an execution context is created, JavaScript creates the variable
environment, outer environment, this, and ***arguments***.
- The ***arguments*** variable is actually an array, and it contains all the
arguments that you have passed to the function.
- The rest operator takes the arguments that aren't defined specifically, and
get wrapped into an array.

### Immediately Invoked Function Expressions (IIFE)s
- IIFEs are function expressions that are immediately invoked once they are
declared.
- An example:

```JavaScript
// function statement
function greet(name) {
  console.log('Hello ' + name);
}
greet('John');

// using a function expression
var greetFunc = function(name) {
  console.log('Hello ' + name);
}
greetFunc('John');

// using an IIFE
var greeting = function(name) {
  return 'Hello ' + name;
}('Adam');
console.log(greeting);

/*
Using an anonymous IIFE, by using the parentheses
This is because JavaScript treats everything inside parentheses as
expressions. This way you're telling JS that you're not creating a new
statement, but creating a new expression instead.
*/

(function(name) {
  console.log('Hello ' + name);
}('Adam'));
```
- By wrapping code in an IIFE, we can ensure that our code does not pollute
the global namespace. (Like in any other normal function)

### Closures
- A ***closure*** is the combination of a function and the lexical environment
within which that function was declared.
- It refers to a function having access to variables that it would normally
would have access to, even though the execution context containing those
variables is now gone.
- In short, ***closures*** make sure that the scope of a method will always be
intact, regardless of when or where you invoke a function. They make sure a
function runs the way it's supposed to.
- E.g.

```JavaScript
function greet(whattosay) {
  return function(name) {
    console.log(whattosay + '' + name);
  }
}

var sayHi = greet('Hi');

/*
The sayHi method still has access to the whattosay variable, even though
the execution context of greet no longer exists. This is automatically
done by JavaScript.

*/
sayHi('Tony');
```

```JavaScript
function buildFunctions() {
  var arr = [];

  for(var i = 0; i < 3; i++) {
    arr.push(function() {
      console.log(i);
    });
  }
  return arr;
}

var fs = buildFunctions();

/*
All three methods above will log out the number 3.
Because JavaScript actually prints out the current value of i,
not the value of i at the point of time the function was pushed into the
console. This is because the console logging is done after the method
assignments, not during the creation of the functions.
*/

fs[0]();
fs[1]();
fs[2]();
```
- If you want to change the number that is logged, you could do this:

```JavaScript
function buildFunctions2() {
  var arr = [];

  for(var i = 0; i < 3; i++) {
    let j = i;
    arr.push(function() {
      console.log(j);
    });
  }
  return arr;
}

/*
This works because a new variable is actually created every time the loop runs,
hence, the variable j will be pointing to different memory locations even if
they have the same variable name.
*/

// OR YOU COULD DO THIS (If you don't have ES5 support)

function buildFunctions2() {
  var arr = [];

  for(var i = 0; i < 3; i++) {
    arr.push(
      (function(j) {
        return function() {
          console.log(j);
        }
      }(i))
    )
  }
  return arr;
}

/*
The code above simply pushes a function that returns another function. Each
of the functions has its very own execution context, and they contain different
values of j. Hence, the console is able to log different values of j.
*/

var fs2 = buildFunctions2();

fs2[0]();
fs2[1]();
fs2[2]();
```

### Function Factories
- A function factory is simply a function that generates another function, but
the function generated may vary.
- Function factories take advantage of closures, which is the ability to make
sure that the scope of a function will always be intact.

```JavaScript
function makeGreeting(language) {
  return function(firstname, lastname) {
    if (language === 'en') {
      console.log('Hello '+ firstname + ' ' + lastname);
    }

    if (language === 'es') {
      console.log('Hola '+ firstname + ' ' + lastname);
    }
  };
}

var greetEnglish = makeGreeting('en');
var greetSpanish = makeGreeting('es');

greetEnglish('John', 'Doe');
greetSpanish('John', 'Doa');
```

### Callback Functions and Closures
- A callback function, is a function that you pass to another function, to be
run when the other function is finished.
- An example:

```JavaScript
function sayHiLater() {
  var greeting = 'Hi';

  setTimeout(function() {
    console.log(greeting);
  }, 3000);
}

sayHiLater();
```
- But this does not work:

```JavaScript
function sayHiLater(callback) {
  var greeting = 'Hi';

  setTimeout(callback, 3000);
}

sayHiLater(function() {
  console.log(greeting);
});
```
- This is because the function is actually declared outside the function, and
since it's parent execution context is not **sayHiLater**, it cannot access
the variable greeting.

### Call, Apply, and Bind
- The Function is just another special kind of object, it has the following
attributes:
  1. Name
  2. Code (Invocable)
  3. ***call()***
  4. ***apply()***
  5. ***bind()***
- Bind is used when you want to change the reference of this for a function
- It creates a copy of your function, and whatever object you pass to the bind
method, becomes the object that the '***this***' keyword points to.
- The ***call*** function also lets you decide what the **this** variable will
be. The first argument for ***call*** should be what the **this** variable
should refer to. The rest of the arguments passed to it are the arguments
that you will normally pass to a function.
- The difference between the ***bind*** and the ***call*** method is that the
***call*** method actually executes the method.
- The ***call*** method and the ***apply*** method perform the same actions,
but the ***call*** method accepts the arguments directly in the parentheses,
whereas the ***apply*** method accepts the arguments in an array format.
- A use for **apply** and **call** would be function borrowing.
- Function borrowing is used to reduce redundant code, by using functions from
an object on another object.
- Example of use of **bind**, **call**, and **apply**:

```JavaScript
var person = {
  firstName: 'John',
  lastName: 'Doe',
  getFullName: function() {
    var fullName = this.firstName + ' ' + this.lastName;
    return fullName;
  }
}

var logName = function(lang1, lang2) {
  console.log('Logged: '+ this.getFullName());
  console.log('Arguments: ' + lang1 + ' ' + lang2);
  console.log('-----------');
};

var logPersonName = logName.bind(person);

logPersonName('en', 'cn');

logName.call(person, 'en', 'es');

logName.apply(person, ['en', 'my']);

// You can also create a function on the fly and invoking it using apply and call

(function(lang1, lang2) {
  console.log('Logged: '+ this.getFullName());
  console.log('Arguments: ' + lang1 + ' ' + lang2);
  console.log('-----------');
}).call(person, 'en', 'ru');

// function borrowing
var person2 = {
  firstName: 'Jane',
  lastName: 'Doe'
};

person.getFullName.call(person2, 'en', 'ru');

```
- Function currying is the act of creating a copy of a function but with some
preset parameters. This is done by passing additional arguments to the bind
method.

```JavaScript
// function currying
function multiply(a, b) {
  return a*b;
}

var multiplyByTwo = multiply.bind(this, 2);

// is actually equals to
function multiply(b) {
  var a = 2;
  return a*b;
}

```

```JavaScript
function multiply(a, b, c) {
  return a * b * c;
}

function curriedMultiply(a) {
    return function (b) {
      return function (c) {
        return a * b * c;
      }
    }
}

console.log(multiply(5, 10, 3));
console.log(curriedMultiply(5)(10)(3));
```

### Functional Programming
- Functional programming is a programming style where you think and code in
terms of functions
- Functional programming languages are languages that have first-class functions
- Here are the examples of the use of first-class functions:

```JavaScript
function mapForEach(arr, fn) {

  var newArr = [];
  for (var i=0; i < arr.length; i++) {
    newArr.push(
      fn(arr[i])  
    );
  }
  return newArr;
}

var arr1 = [1,2,3];
console.log(arr1);

var arr2 = mapForEach(arr1, function(item) {
  return item * 2;
});
console.log(arr2);

var arr3 = mapForEach(arr1, function(item) {
  return item > 2;
});
console.log(arr3);

var checkPastLimit = function(limiter, item) {
  return item > limiter;
}

// When additional arguments to the bind method,
// a new copy of the method gets created with preset parameters.
var arr4 = mapForEach(arr1, bindy(checkPastLimit, 1));
console.log(arr4);

var checkPastLimitSimplified = function(limiter) {
  return function(limiter, item) {
    return item > limiter;
  }.bind(this, limiter);
};

var arr5 = mapForEach(arr1, checkPastLimitSimplified(2));
console.log(arr5);

```
- Instead of just separating your code into functions, first class functions
allow you to pass functions to your functions, and also return functions
from your functions.
- In functional programming, your functions should not mutate data, but instead
output data from input data.

## 04. Object-Oriented JavaScript and Prototypal Inheritance
### Prototypal Inheritance
- ***Inheritance*** is when one object gets access to the properties and
methods of another object.
- In prototypal inheritance, each object has its **\__proto__** property,
which contains a **reference** to another object, which is its prototype.
- The prototype of an object can also have a reference to its very own
prototype.
- When you're looking for a property on an object, if it doesn't find the
property on the object you're specifying, JavaScript will go down the
prototypal chain until it finds the property specified.
- All objects in JavaScript have their own prototypes, except for the base
*Object*.
- An example would be that each function has the methods **bind**, **call**,
and **apply**
on its on prototype chain.
- A code example:

```JavaScript
var getCookies = function() {
  console.log('I has the cookies');
}

// Instead of calling getCookies.__proto__.bind(this);
// We can do this:

getCookies.bind(this);

```
### Reflection and Extend
- ***Reflection*** means that an **object** can look at itself, and it can list
and change its properties and methods.

```JavaScript
var person = {
  firstname: 'Default',
  lastname: 'Default',
  getFullName: function() {
    return this.firstname + ' ' + this.lastname;
  }
};

var john = {
  firstname: 'John',
  lastname: 'Doe'
};

for (var prop in john) {
  // To check if the property is actually directly on the object
  if (john.hasOwnProperty(prop))
    console.log(prop + ': ' + john[prop]);
}

var jim = {
  getFirstName: function() {
    return firstname;
  }
};

// Using Lodash / Underscore JS
_.extend(john, jim);
```

## 05. Building Objects
### Function Constructors, 'new', and The History of JavaScript
- A ***function constructor*** is actually just a normal function, that is used
to construct objects.
- When you create a new object using a function constructor, the following
happens:
  1. The '**new**' keyword creates a new empty object.
  2. It then binds the '**this**' keyword to that of the new empty object.
  3. It binds the ***\__proto__*** property of the new object to the prototype
  property of the function constructor.
  4. It then executes the code inside the function constructor, which sets
  the properties of the object.
  5. As long as the function constructor doesn't explicitly return a value,
  JavaScript will automatically return the object that was created.

### Function Constructors and '.prototypes'
- When the function constructor is used, the prototype is already automatically
set for the object.
- Other than name and code, all functions in JavaScript have a property called
***prototype***. Unless the function is used as a function constructor,
***prototype*** will never be used. (It is only used by the **new** operator).
- The ***prototype*** property on the function is not the prototype of the
function (The prototypes of the function are actually accessed using the
**\__proto__** keyword).
- Instead, ***prototype*** is actually the prototype of any objects created
using the function constructor.

```JavaScript
function Person(firstname, lastname) {
  console.log(this);
  this.firstname = firstname;
  this.lastname = lastname;
  console.log('This function is invoked.');
}

Person.prototype.getFullName = function() {
  return this.firstname + ' ' + this.lastname;
};

// The 'new' keyword is actually an operator, which is used to actually
// create a new object, and perform the binding of 'this'
var john = new Person('John', 'Doe');
console.log(john);

var jane = new Person('Jane', 'Doe');  
```
- When you create an object using the **new** keyword, a new empty object is
created, it binds the '***this***' keyword to the new object, and it sets the
***\__proto__*** of the empty object to the ***prototype*** property of the
function constructor that is called.
- The ***prototype*** property of function constructors is where the
***\__proto__*** property of all objects created using the function
constructors point to.
- This means that you can add additional functionality to the objects later on,
all at once since you're adding functionality to the prototype of the objects.
- Properties are often setup inside the function constructors, because
properties largely vary from object to object.
- However, since objects created from the same class have mostly the same
functionality, we could put functions on the prototype of the function
constructor, and objects can refer to the function on its prototype.

### 'new' and Functions
- Function constructors are actually just regular functions.
- That means that if you forgot to use the ***new*** keyword when creating a
new object, the function is still syntactically correct, and JavaScript won't
catch the error.
- When you try to create a new object without using the ***new*** keyword, the
function constructor will return ***undefined***. Hence, an error will be
thrown when you try to access the uncreated object.
- As a rule of thumb, any function that is intended to be used as a function
constructor, should start with a capital letter.

### Built-in Function Constructors
- An example built-in function constructors are:

```JavaScript
var a = new Number('3');

var b = new String('John');

'John'.length;
// is equal to
var c = new String('John');
c.length;
```
- We could also add new functions to existing objects in JavaScript:

```JavaScript
String.prototype.isLengthGreaterThan = function(limit) {
  // If this is called inside a string object, it would be pointing at your
  // String object. JavaScript takes care of this by going down the prototype
  // chain.
  return this.lengthh > limit;
};

console.log('John'.isLengthGreaterThan(2));

Number.prototype.isPositive = function() {
  return this > 0;
}
```
- Built-in functions constructors especially for primitive data types are
dangerous.
- When using built-in function constructors for creating primitives, actual
primitives are not created. Hence, when strict comparison happens a primitive
and a primitive created using a built-in function constructor, the two values
will not be the same.
- Moment.js is useful for manipulating dates in JavaScript

### Arrays and for ... in
- An array in JavaScript is actually an object.
- Whenever you're adding additional functionality to a built-in functionality
constructor, when you use for ... in, the additional functionality
gets triggered even if it was not explicitly called.
- This is because the for ... in gets every property in the object, regardless
if it is directly on the object itself, or on the prototype of the object.

```JavaScript
Array.prototype.myCustomFeature = 'cool';

var arr = ['John', 'Jane', 'Jim'];

// avoid this
for (var prop in arr) {
  console.log(prop + ': ' + arr[prop]);
}

//use this instead
for (var i=0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

### Object.create and Pure Prototypal Inheritance
- Object.create is a newer way to create objects, using pure prototypal
inheritance concepts.
- With Object.create, you create a new empty object, and the object that you
have passed in becomes your prototype.
- If you do not use '***this***' to refer to properties inside the object,
JavaScript will not be able to locate the property that you want, since the
creation of the object does not actually create a new execution context.
- With this pattern, you simply override whatever you need to by simply adding
the properties or methods to your created object.
- A ***polyfill*** is code that adds a feature which the engine *may* lack.

```JavaScript
// polyfill
if(!Object.create) {
  Object.create = function (o) {
    if (arguments.length > 1) {
      throw new Error('Object.create implementation'
      + ' only accepts the first parameter.');
    }
    function F() {};
      F.prototype = o;
      return new F();
  };
}

var person = {
  firstname: 'Default',
  lastname: 'Default',
  greet: function() {
    return 'Hi ' + this.firstname;
  }
};

// Object.create is just used to create others of person
var john = Object.create(person);
john.firstname = 'John';
john.lastname = 'Doe';
console.log(john);
```

### ES6 and Classes
- Classes in JavaScript are actually objects. When you create a new object from
a class in JavaScript, you're actually creating an object from an object.
- The ***extends*** keyword in JavaScript is actually just used to set the
prototype of an object to another object.
- ***Syntactic Sugar*** is just a different way to type something that doesn't
change how it works under the hood.
