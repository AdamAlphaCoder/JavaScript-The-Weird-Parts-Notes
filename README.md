# JavaScript: The Weird Parts

Below is a list of notes made for the course JavaScript: The Weird Parts.

## Table of Contents
- [JavaScript: The Weird Parts](#javascript--the-weird-parts)
  * [01. Execution Contexts and Lexical Environments](#01-execution-contexts-and-lexical-environments)
    + [Syntax Parser](#syntax-parser)
    + [Lexical Environment](#lexical-environment)
    + [Execution Context](#execution-context)
    + [Name/Value Pair](#name-value-pair)
    + [Object](#object)
    + [Hoisting](#hoisting)
    + [Phases of execution context inside JavaScript](#phases-of-execution-context-inside-javascript)
    + [JavaScript is single threaded, synchronous execution](#javascript-is-single-threaded--synchronous-execution)
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
    + [Objects, Functions, and 'this'](#objects--functions--and--this-)
    + ['arguments' and REST](#-arguments--and-rest)
    + [Immediately Invoked Function Expressions (IIFE)s](#immediately-invoked-function-expressions--iife-s)
    + [Closures](#closures)
    + [Function Factories](#function-factories)
    + [Callback Functions and Closures](#callback-functions-and-closures)
    + [Call, Apply, and Bind](#call--apply--and-bind)

## 01. Execution Contexts and Lexical Environments
### Syntax Parser
- A program that reads your code and determines what it does, and if the grammar is valid.

### Lexical Environment
- Where something sits physically in the code you write, the positioning, where is it contained

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
- A name which maps to a unique value, can be defined more than once, but can have only one value in any given context

### Object
- A collection of Name/Value pairs, a function also counts as a value
- If the value is a primitive, it's called a property.
- If the value is a function, it's called a method.

### Hoisting
- Setup memory space for variables and functions
- Memory space is allocated for functions and variables, but variables are not yet defined. All values in JS are set initially to undefined.
- Avoid using hoisting. Always declared methods and variables before using them.

### Phases of execution context inside JavaScript
1. Creation of variables and functions in memory
2. Execution phase

### JavaScript is single threaded, synchronous execution
- Means that it can only execute one instruction at a time in the order that it appears.
- Asynchronous events are actually handled synchronously.

### Invocation
- Running a function, invoking a function

### Execution Stack
- When the script is run, the global execution context is created, and is executed.
- However, if there is another function invocation, it will stop at that line of code, and create and execute the execution context.

### Variable environment
- Where the variables live, and how they relate to each other in memory

### Scope Chain
- A scope is Where a variable is available in your code, and if it's truly the
same copy, or a new one.
- Basically what scope contains what scope/variables
- If the variable is not found inside the execution context, it will search for the variable inside the outer lexical environment. If it is not found inside the inside the outer lexical environment, then it will go up the scope chain until it finds the variable, or when it reached the global execution context.
- Note that just because your execution context is on top of another in the scope chain, it does not mean that it the one on the bottom is necessarily its parent.
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
- A function is actually just an object, whose code just happens to be one of the
properties attached to the object.

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
