---
layout: post
title:      "Scoping and Hoisting"
date:       2020-10-14 22:18:31 +0000
permalink:  scoping_and_hoisting
---


# Scoping 
Scoping is the availabliy of  variables, functions, and objects in your code during runtime. To put it simply, scope determines where a variable (function/object)  can be accessed is determined by the location of it's declaration. 

In javascript there are two types of scopes: 

###  Global Scope 
*A variable is in Global scope if it's defined outside of a function *
```
//this is defaulted to global
var greeting = "Hello";
```

Varaibles with a global scope can be accessed and changed in any other scope.

```
van greeting = "Hello";
console.log(greeting); // logs 'Hello'

function sayGreeting() {
   console.log(greeting); // 'greeting' can be accessed here
}

sayGreeting(); // logs 'Hello'
```


## Local Scope 
*Variables declared within a function are in the local scope*
Local scope variables can only be accessed within their respective functions. Meaning that a variable can have the same name and be used in different functions. 

```
function hello() {
  var greeting = 'hello'
  console.log(greeting)
}

function goodbye() {
  var greeting = 'goodbye'
  console.log(greeting)
}

hello(); // logs 'hello'
goodbye(); // logs 'goodbye'

```

*The **var** statement declares a function-scoped or globally-scoped variable*

## Block statments
Block statements do not create a new scope and variables defined inside will remain in that scope. 

```
if (true) {
    var greeting = 'Hello'; // name is still in the global scope
}

console.log(greeting); // logs 'Hello'

```

With ECMAScript 6 the keywords** let** and **const** can be used to replace **var**.  Unlike var, let and const you can delcare a variable in local scope inside block statements. 

```
if (true) {
    // this 'if' conditional block doesn't create a scope

    var hello = 'Hello';   // hello is in the global scope because of the 'var' keyword
   
    let goodbye = 'Goodby';   // goodybye is in the local scope because of the 'let' keyword
  
    const howdy = 'Howdy';    // howdy is in the local scope because of the 'const' keyword
}

console.log(hello); // logs 'Hello'
console.log(goodbye); // Uncaught ReferenceError: goodbye is not defined
console.log(howdy); // Uncaught ReferenceError: howdy is not defined
```

## Execution context
*Execution context (EC) is defined as the environment in which the JavaScript code is executed. Environment, meaning the value of ` this`, variables, objects, and functions that the code has access to at a particular time.*

Each execution context creates a Variable Object which consists of three things,
1. Local Variable Object
2. Scope Chain
3. `this` (refered to as context and in the global scope is always the Window object)

## Lexical Scope 
Lexical Scope allows nested functions to have access to vaiables and other resources of their parent scope. 

```
function second () {
  function first () {
    console.log('Inside first()');
 
    console.log('myVar is currently equal to:', myVar);
  }
 
  const myVar = 'Bar';
 
  first();
}

second();
// LOG: Inside first()
// LOG: myVar is currently equal to: Bar
// => undefined
```

## Closures 
*Closures contain their own scope chain, the scope chain of their parents and the global scope.*
Closures can access varaiables and arguments in its outer function. 

```
function greeting() {
    hello = 'Hello';
    return function () {
        console.log(hello);
    }
}

greeting(); // nothing happens, no errors

// the returned function from greeting() gets saved in callGreeting
callGreeting = greeting();

 // calling callGreeting calls the returned function from the greeting()
callGreeting(); // logs 'Hello'
```

# Hoisting 
Hoisting is when you execute a piece of code and the Javascript engine cretes the global execution context which has two phases:

### Creation Phase 
In this first phase a function is called by not executed. The following occurs:
* Creation of the Variable (Activation) Object 
   *    *contains all of the variables, functions and other declarations    *
* Creation of the Scope Chain
     *  created after the variable object and contains the variable object*
* Setting the value of `this`

### Execution Phase 
In this second phase other values are assigned and code is executed. 


## Variable hoisting
Variable hoisting is when variable declarations are moved to the top of the script. 

```
console.log(counter); // undefined
var counter = 1;
```

The above code looks like this during execution phase 
```
var counter;

console.log(counter); // undefined
counter = 1;
```
if using let you get:
```
console.log(counter);
let counter = 1;

"ReferenceError: Cannot access 'counter' before initialization
```
It's best practice to define all variables at the top of your code to prevent this issue: 
```
let counter = 1;
console.log(counter); // logs 1
```

## Function Hoisting 
Like varaibles, functions also get hoisted; moving the function declarations to the top of the script.

```
let x = 20,
    y = 10;

let result = add(x,y);
console.log(result); // logs 30

function add(a, b){
return a + b;
}
```
In the above code we called add() before defining it. The code below is the same as the previous example. 

```
function add(a, b){
    return a + b;
}

let x = 20,
    y = 10;

let result = add(x,y);
console.log(result); // logs 30

```
The creation phase places add() in the memory and executes it when called. 

