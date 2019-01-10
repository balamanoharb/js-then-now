Table of Contents
<!-- MarkdownTOC depth=0 autolink="true" bracket="round" -->

- [Introduction](#introduction)
- [New String Methods](#new-string-methods)
- [scoping var, let, const](#scoping-var-let-const)
	- [var](#var)
		- [declaration hoisting](#declaration-hoisting)
		- [var in loops](#var-in-loops)
		- [global scope](#global-scope)
	- [let](#let)
	- [const](#const)
	- [Temporal Deadzone](#temporal-deadzone)
	- [What to use ?](#what-to-use-)
- [Template Strings](#template-strings)
	- [Tag Functions](#tag-functions)
		- [various uses](#various-uses)
- [Arrow Funcitons](#arrow-funcitons)
	- [Different Formats](#different-formats)
		- [Named arrow functions](#named-arrow-functions)
		- [without any parameters/single parameter](#without-any-parameterssingle-parameter)
		- [with parameters](#with-parameters)
		- [non concise body](#non-concise-body)
		- [returning objects in concise format](#returning-objects-in-concise-format)
	- [arrow functions vs old functions](#arrow-functions-vs-old-functions)
		- [naming](#naming)
		- [the 'this' keyword](#the-this-keyword)
	- [Arrow function - Cautions](#arrow-function---cautions)
- [Default Arguments](#default-arguments)
	- [Lazy Expressions](#lazy-expressions)
	- [Useful cases](#useful-cases)
	- [Using already defined parameters in the list](#using-already-defined-parameters-in-the-list)
	- [A bad code example](#a-bad-code-example)
- [Destructuring](#destructuring)
	- [Destructuring Objects](#destructuring-objects)
		- [Destructuring nested objects](#destructuring-nested-objects)
		- [Merging Objects](#merging-objects)
	- [Destructuring Array](#destructuring-array)
		- [Usage](#usage)
			- [destructuring with default values](#destructuring-with-default-values)
			- [type error with destructuring](#type-error-with-destructuring)
			- [With rest operator](#with-rest-operator)
			- [swapping](#swapping)
			- [Array manipulation \( Dumping variables\)](#array-manipulation--dumping-variables)
			- [Destructing nested array](#destructing-nested-array)
			- [multiple destructuring](#multiple-destructuring)
		- [what not to do](#what-not-to-do)
	- [Destructuring & Function parameters](#destructuring--function-parameters)
- [Iterables and Looping](#iterables-and-looping)
	- [for loop](#for-loop)
	- [forEach](#foreach)
	- [for..in](#forin)
	- [for..of](#forof)
		- [for..of usage](#forof-usage)
		- [what is not iterable](#what-is-not-iterable)
		- [Make Objects iterable](#make-objects-iterable)
- [New  Methods](#new--methods)
	- [Array.from](#arrayfrom)
	- [Array.of](#arrayof)
	- [Array.find](#arrayfind)
	- [Array.findIndex](#arrayfindindex)
	- [Array.some](#arraysome)
	- [Array.every](#arrayevery)
- [...spread and ...rest operator](#spread-and-rest-operator)
	- [spread operator usage](#spread-operator-usage)
	- [...rest usage \(gather\)](#rest-usage-gather)
- [Object literal syntax upgrades](#object-literal-syntax-upgrades)
	- [concise property Names](#concise-property-names)
	- [concise methods](#concise-methods)
	- [computed property names](#computed-property-names)
	- [computed method names](#computed-method-names)
	- [Computed Generator function name](#computed-generator-function-name)
- [Promises](#promises)
	- [creating promise](#creating-promise)
		- [using promises](#using-promises)
		- [Handling multiple promises](#handling-multiple-promises)
- [Symbol - The seventh new data type](#symbol---the-seventh-new-data-type)
- [Code Quality](#code-quality)
	- [how to use in sublime](#how-to-use-in-sublime)
	- [forcing eslint before commit](#forcing-eslint-before-commit)
- [javascript modules](#javascript-modules)
	- [configuring webpack](#configuring-webpack)
	- [Creating Modules](#creating-modules)
	- [systemjs](#systemjs)
	- [babel](#babel)
		- [plugins](#plugins)
	- [Polyfill](#polyfill)
- [Prototypal Inheritance Briefing](#prototypal-inheritance-briefing)
- [Classes](#classes)
	- [static methods](#static-methods)
	- [getters and setters](#getters-and-setters)
	- [using super\(\)](#using-super)
	- [Extending native class](#extending-native-class)
- [Generator functions](#generator-functions)
	- [Use cases for generator functions](#use-cases-for-generator-functions)
	- [for..of with generators](#forof-with-generators)
	- [custom iterators for objects](#custom-iterators-for-objects)
- [Proxies!](#proxies)
	- [Usage](#usage-1)
- [Sets](#sets)
	- [set - methods](#set---methods)
	- [Weak Sets](#weak-sets)
- [Map](#map)
	- [Usage](#usage-2)
	- [WeakMap](#weakmap)
- [Promise - aysnc and wait](#promise---aysnc-and-wait)
	- [Calling multiple promises](#calling-multiple-promises)
	- [Changing with Async Await](#changing-with-async-await)
	- [Awaiting multiple promises](#awaiting-multiple-promises)
	- [Promisifying functions](#promisifying-functions)
- [Class Properties](#class-properties)
- [Padding Strings](#padding-strings)
- [Exponential Operator](#exponential-operator)
- [Trailing/Dangling comma](#trailingdangling-comma)
- [Object.entries\(\) and Object.values\(\)](#objectentries-and-objectvalues)

<!-- /MarkdownTOC -->

# Introduction

- es6 features overview

# New String Methods

- .startsWith('look')
- .endsWith('lookup')
- .includes('lookup string')
- .repeat('number_of_times')
- can be used for padding

# scoping var, let, const

## var

- var is function scoped 

### declaration hoisting

```
function foo(x,y) {
	if( x > y) {
		var tmp = x;
		x = y;
		y = tmp;
	}
}
```

- Functionally the variable 'tmp' is hoisted and scoped to foo
- But synctactically, what the code means is I want the 'tmp' variable to be available only to the if block.

### var in loops

```
for ( var i = 0; i < 10; i++){
	//..
	// functionally means that i should be scoped only to this for block
	// but functionally it's totally different.
	(function(i){
		// binding something or using at a later point in time where i is used
	})(i)
}
```

### global scope

- var can be declared multiple times without errors
- so accidentally the window scoped global variables can be replaced.
- scope gets leaked

```
var RegExp = 'yolo'
```

## let

- block scoped
- cannot be declared multiple times
- replaces iffe's in most places
- makes looping easier
- using let in global scope doesn't replace the values on window object.

## const

- cannot be re-assigned 
- does not mean it's a constant (i.e) values are still mutable
- value can be updated
- usually used for primitive constants
- to really make it a const, use Object.freeze()
- using const may cause confusion.

## Temporal Deadzone 

- let and const variables cannot be accessed before they are defined

## What to use ?

- there is no standard way. Just developer opinions
- There is a recommendation to use const by default and let for things that will change
- There is also recommendation to use var for function scope, let for block scope and const for literal constants


# Template Strings

- this is called as string interpolation in other languages

```
var name = 'Bala';
var orderNumber = "123";
var total = 319.7;

// multi line string
var msg = "Hello, " + name + ", your \
order (#" + orderNumber + ") was $" + 
total + ".";
```

- since single quote and double quote are already use for strings, the new way to interpolate strings is to use backtick.

```
var name = 'Bala';
var orderNumber = "123";
var total = 319.7;


var msg = `Hello ${name}, your
order (#${orderNumber}) was $${total}.`;

//output will actually span multiple lines just as given here
```

- It automatically preserves new lines.
- If that needs to be escaped then use \ like in normal method
- Any legal javascript expression can be put in to those brackets


## Tag Functions

- a tag function accepts the interpolation string as an input
- the strings are split based on the ${someVariable} presence
- Tag function's api
```
function msgFormatter(strings, value1, value2, value3, etc){
	return processedString;
}
```

```
// this function returns the same string
// but lot of formatting can be done with this
function msgFormatter(strings,...values){
	var str = "";
	for (let i = 0; i < strings.length; i++){
		if( i > 0) str += values[i - 1];
		str += strings[i];
	}
	return str;
}
var name = 'Bala';
var orderNumber = "123";
var total = 319.7;


var msg = msgFormatter`Hello ${name}, your
order (#${orderNumber}) was $${total}.`;
```

### various uses

- pre formatting values
- highlight values
- sanitize the values

# Arrow Funcitons

```
(parameter1, parameter2, etc...) => return_value_expression
```

- The above syntax creates an anonymous function and returns the value.
- this is the concise one liner function.
+ Regular functions can be either function declarations or function expressions, however arrow functions are always expressions. In fact, their full name is "arrow function expressions", so they can only be used where an expression is valid. This includes being:
1. stored in a variable,
2. passed as an argument to a function,
3. and stored in an object's property.

## Different Formats


### Named arrow functions

- arrow functions are anonymous by default

```
var funcName = (param1, param2, ...) => return_value_expression
```

- This syntax makes the js interpreter to automatically inference and set the function name of the returned arrow function to functionName.

### without any parameters/single parameter

- () -- will be just a placeholder, infact any valid name can be used there without any brackets

```
foo = () => 3
console.log(foo())

// similary
foo = x => x
console.log(foo(100))

//even this is valid
foo = _ => 5
console.log(foo())
```

### with parameters

- if there are morethan one parameter then () is required

```
foo = (x,y) => 6
console.log(foo())
```

### non concise body

- the concise body accepts any expression as a valid return statement.
- for any non concise body, the return statement should be explicit
- and it should be contained in curly braces

```
foo = x => { 
  try{ 
    return 3;
  } 
  catch(e) {
    console.log(e);
  } 
}
```

### returning objects in concise format

- to return objects in concise format, it should be enclosed in ()
- this is because when arrow function encounters {} it will be treated as non concise body format.

```
// in this it doesn't return an object instead it returns undefined
foo = x => { y: 5}
console.log(foo())

foo = x => ({ y: 3})
console.log(foo())
```

## arrow functions vs old functions

> there's a gotcha with the this keyword in arrow functions

>arrow functions are only expressions. There's no such thing as an arrow function declaration.

### naming

- arrow functions are syntactically anonymous, they are named only through name inferencing, that is through guessing the context.
- this might become a problem for identifying errors
- old function can be named when defining them

```
// Promises
p.then( function(v) {return v.id} )
// looks elegant doesn't it?
p.then( v => v.id)
// the problem with this?
// say v is null, v.id will throw exception but in stack trace it'll be anonymous function
// which is hard to debug
// so name it,then it will come with function name in stack trace
// p.then( function extractId(v) {return v.id} )
// advantage :: here the name will be self expressive and easy to debug
```

### the 'this' keyword

> Regular function 'this' behaves based on how the function is called

> On arrow functions 'this' behaves based on where the function is called

- arrow functions do not have their own 'this' keyword.
- so if 'this' keyword is used inside an arrow function, it will simply follow the scope chain to look for this.

- we can consider this as arrow functions inherit the 'this' keyword from it's parent. It's kind of using a normal variable in the scope chain.

- With regular functions, the value of this is set based on how the function is called. With arrow functions, the value of this is based on the function's surrounding context. In other words, the value of this inside an arrow function is the same as the value of this outside the function.

- functions inside object

```
var myObj = {
  id: 'adf-3ir9-alkdjfk',
  func: function foo() {
    setTimeo	ut(function(){
      console.log('---time out--')
      console.log(this)
      console.log(this.id)
    },100)
  }
}
```

- here this will be referring to the global window object instead of myObj

```
// people usually pass this as self
var myObj = {
  id: 'adf-3ir9-alkdjfk',
  func: function foo() {
    var self = this;
    setTimeout(function(){
      console.log('---time out--')
      console.log(self)
      console.log(self.id)
    },100)
  }
}
```

- self is just an un creative way of naming
- it should be context instead since that's what it's really referring to

```
var myObj = {
  id: 'adf-3ir9-alkdjfk',
  func: function foo() {
    var context = this;
    setTimeout(function(){
      console.log('---time out--')
      console.log(context)
    },100)
  }
}
```

- what should be really done is bind this to the function

```
var myObj = {
  id: 'adf-3ir9-alkdjfk',
  func: function foo() {
    setTimeout(function(){
      console.log('---time out--')
      console.log(this)
    }.bind(this),100)
  }
}
myObj.func()
```

- using arrow functions, we automatically gets the lexical context this

```
var myObj = {
  id: 'adf-3ir9-alkdjfk',
  func: function foo() {
    setTimeout(() => {
      console.log('---time out--')
      console.log(this.id)
    },100)
  }
}
myObj.func()
```

## 'this' keyword inside normal functions 

### A new object

If the function is called with new:

```
const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);
```

In the code above, the value of this inside the Sundae constructor function is a new object because it was called with new.

### A specified Object

If the function is invoked with call/apply:

```javascript
const result = obj1.printName.call(obj2);
```

In the code above, the value of this inside printName() will refer to obj2 since the first parameter of call() is to explicitly set what this refers to.

### A context object

If the function is a method of an object:

```javascript
data.teleport();
```

In the code above, the value of this inside teleport() will refer to data.

### The global object or undefined

If the function is called with no context:

```
teleport();
```

In the code above, the value of this inside teleport() is either the global object or, if in strict mode, it's undefined.


## Arrow function - Cautions

- because arrow functions doesn't have the 'this' variable call(), apply() and bind() can't be used, so all functions cannot be replaced with => function
- as direct functions inside object - since 'this' will be referring to the global context and not the object itself.
- adding a prototype method and using 'this'
- doesn't have access to arguments

# Default Arguments

- we used to set default values for function arguments like this

```
function foo(x){
	x = x || 42;
	return x;
}

foo() // will return 42
foo(0) // will also return 42 instead of expected 0
```

- this is because || operator will do truthy falsy value test. In this case because of corecion, x will be false
- it should be written as

```
function foo(x) {
	x = x !== undefined ? x : 42;
	return x;
}

foo(0) // will return 0
foo(null) // will return null
```

- null will be a valid value since we are specifically checking for 'undefined'
- the above code can be written with es6 syntax for setting default value as

```
function foo(x = 42) {
	return x;
}

foo() // will return 42
foo(undefined) // will return 42
foo(null) // will return null
```

- the parameter list is block scoped to the function so it's using 'let'

## Lazy Expressions

- How many times will bar be called in the following segment

```
function bar() {
	console.log("!");
}

function foo(x = bar() ){

}
```

- Zero times actually. It's not called until it's necessary for computation

```
foo(10) // bar is not called yet
foo()   // bar is called and computed
foo()   // bar is called and computed again
```

- How many ever times it's needed those many times it'll be called.

## Useful cases

- unique computations

```
function uniqueIdGenerator() {
	//...
}

function foo(x = uniqeIdGenerator() ){

}
```

- check for required parameter

```
function require() {
	throw "Parameter required!!!"
}

function foo(id = required()){

}
```

## Using already defined parameters in the list

- parameter definition goes from left to right
- so it's possible to use a parameter/argument already defined when going left to right

```
function foo( x = 2, y = x){
	console.log(x,y)
}

foo() // will return 2 2
```

## A bad code example

- since using an already defined parameter is possible what happens when it's combined with inline function

```
function foo( x=2, y = function() { return x}){
	console.log(y());
}

foo() // prints 2
```

- but what would happen here

```
var x = 1
function foo( x=2, y = function() { return x}){
	var x = 5;
	console.log(y());
}

foo() // still prints 2
```

- we are supposed to get 5
- x = 2 actually creates a function scoped variable
- so 'var x = 5' doesn't actually create a new function scoped variable instead it'll be considered like an assignment 'x = 5'.
- so when the anonymous function y was declared, it takes the current value of x which is 2.

# Destructuring

## Destructuring Objects

```
var { 
	objectKey1: "variable name where the objectKey's value should be stored" 
} = someObject
```


- allow us to extract property values from objects
- this can be nested
- defaults can be set

- we used to do it like this

```
function getDetails() {
	return {
		name: 'bala',
		age: 28,
		role: 'software engineer'
	}
}

var personName, personAge, personRole;

var personData = getDetails();

personName = personData.name;
personAge = personData.age;
personRole = personData.role;
```

- The above can be done as

```
var {
		name: personName,
		age: personAge,
		role: personRole
} = getDetails()
```

- when object destructuring is used without 'var' declaration, it needs to be wrapped in paranthesis as it will be considered as assigning something to object literal syntax and not qualify as a valid expression.
- It follows the object literal syntax where the left part denotes the keyName and the right part denotes the KeyValue. Similarly while destructuring, the keyName is specified on the left side and the variable where the value of the specified keyName should be stored to.
- If the keyname and the varaible name we want to store the value are the same, we can do it even more simpler like this.

```
var { name, age, role} = getDetails()
```

- This will extract the value of key 'name' from the object returned by getDetails and store it in a variable with the same name
- It's same as this

```
var name, age, role;
(
	{
		name: name,
		age: age,
		role: role
	} = getDetails()
)
```

### A thing to note when destructurin

```
const circle = {
  radius: 10,
  color: 'orange',
  getArea: function() {
    return Math.PI * this.radius * this.radius;
  },
  getCircumference: function() {
    return 2 * Math.PI * this.radius;
  }
};

let {radius, getArea, getCircumference} = circle;
```
- Here calling getArea() will return NaN since this reference actually lost.

### Destructuring nested objects

```
function getDetails() {
	return {
		name: 'bala',
		age: 28,
		role: 'software engineer',
		address: {
			line1: 'Private Corporation Ltd',
			line2: 'Indra Nagar',
			city: 'Bangalore'
		}
	};
}

var {
	name, 
	age, 
	role: personRole = 'IT Professional',
	role: roleCopy,
	address: {
		line1: address1,
		line2: address2,
		city
	} = {} ,
	randomKey: randomVal = 100
} = getDetails() || {};
```

- the abscence of a property behaves as 'undefined'
- if a nested expected object is not defined in the object it'll throw the same type error, so it should be default.
- this is how it'll search
	- look for the key
	- check for default value
	- then do destructuring of pattern

### Merging Objects


```
var defaults = {
	method: "POST",
	callback: function() {},
	headers: {
		"content-type": "text/plain"
	}
};

var config = {
	url: "http://some url",
	callback: foo,
	headers: {
		"x-requested-width": "foo"
	}
}
```

Merging two hashes can be done like this through destrucutring

```
let {
	method = defaults.method,
	url,
	callback = defaults.callback,
	headers: {
		"content-type": contentType = defaults.headers["content-type"],
		"x-requested-with": xRequestedWith
	}
} = config;

config = {
	method,
	url,
	callback,
	headers: {
		"content-type": contentType,
		"x-requested-with": xRequestedWith
	}
}
```


## Destructuring Array

```
function foo() {
	return [1,2,3];
}

var tmp = foo();
var a = tmp[0];
var b = tmp[1];
var c = tmp[2];
```

- this can be done as
```
function foo(){
	return [1, 2, 3];
}

var [a, b, c] = foo();
// to make it readable
var [
	a,
	b,
	c, // trailing comma is allowed
] = foo();
// easier to make out the diff as well
```

- that is not an array.
- it simply means the assignment is expecting a value on the right hand side with the pattern defined on the left hand side
- when the variable defined in the expected pattern is not exact as the value, it's simply ignored when it's more than what was expected or assigned as undefined when the value contains less stuff than expected

```
var a,b,c;

[
	a,
	b,
	c,
] = [1,2,3,4]
// extra value 4 is ignored

[
	a,
	b,
	c,
] = [1]
// values not found are assigned as undefined

```
- anything that is a valid assignment target can be put in that pattern

```
var x= [ 'name', 'dob', 'detail1', 'detail2'];
var person = {};
[
	person.name,
	person.dob,
	person.detail1,
	person.detail2
] = x;
```
### Usage

- very helpful when working with api responses

#### destructuring with default values

```
function foo()
	return [1];
}

var tmp = foo();
var a = tmp[0];
var b = tmp[1] !== undefined ? tmp[1] : 42;
var c = tmp[2]
```

- can be simplified with destructuring as

```
function foo() {
	return [1];
}

var [
	a,
	b = 42,
	c,
] = foo();
```

#### type error with destructuring

```
function foo() {
	return null;
}

var [
	a,
	b,
	c
] = foo() || [];
```

#### With rest operator

```
function getPersonDetails() {
	return ['bala', 'software engineer', pramata', '4th floor', salarpuria citadel', 'bangalore' ];
}

var person = {};
[
	person.name,
	person.role,
	person.org,
	...person.address
] = getPersonDetails();
```

#### swapping

```
var x = 10, y  20;

[x,y] = [y,x];
```

#### Array manipulation ( Dumping variables)

```
var a = [1,2,3];
var x,y;
[
	x, 
	y,
	...a
] = [ 0, ...a, 4];
```

- ignore first 2 elements

```
[ , , ..a] = a
```

#### Destructing nested array

```
function foo() {
	return [ 1, 2, 3, [4, 5, 6]];
}

var a, b, c, vals, d, e;

[
	a,
	b,
	c,
	...vals
] = foo();
// here vals = [[4, 5, 6]]
	
[
	a,
	b,
	c,
	[
		d,
		e
	]
] = foo();
```

- implicitly uses array indexes for matching with the pattern

#### multiple destructuring

- since destructuring is just pattern matching on assignments

```
[a, b] = [,,...args]
```

### what not to do 

- Destructuring is not an array, it's just pattern matching on assignments.

```
var x = [ a, b] = [ 1, 2, [3, 4, 5]]
// here x will not have [ 1, 2] but the whole array [1, 2, [3, 4, 5]]
```

- but this is possible

```
function foo(){
	return [1, 2, 3, [4, 5, 6] ];
}

var a, b, c, d, vals;
[ , , ,[c] ]  = [a, b, , ...vals] = foo()
```

- one thing to note is var applies only to the left most variables.

## Destructuring & Function parameters

- Both array and object destructuring is applicable to function parameters since it's essentially an assignment

```
function foo( [a, b, c] ) {
	console.log(a, b, c);
}

foo( 1, 2, 3); // will throw error

foo( [1, 2, 3] );
```

- when a function is having morethan two or three parameter it is better to replace it with object destructuring


# Looping

```
const names = ['luffy', 'light', 'goku', 'batman', 'superman']
```

## for loop

- The for loop is obviously the most common type of loop there is, so this should be a quick refresher.

```
for(const i = 0; i < names.length; i++){
	console.log(name[i])
}
```

-  the biggest downside of a for loop is having to keep track of the counter and exit condition.

## for..in

> It iterates over all keys (including the ones inherited) of an Object

- The for...in loop improves upon the weaknesses of the for loop by eliminating the counting logic and exit condition.

```
for( const index in names) {
	console.log(names[index]);
}
```
- But, you still have to deal with the issue of using an index to access the values of the array, and that stinks; it almost makes it more confusing than before.
- It also iterates over the prototype properties and all the other values

```javascript
Array.prototype.decimalfy = function() {
  for (let i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

- This is why for...in loops are discouraged when looping over arrays.


## forEach

```
names.forEach((name) => {
	console.log(name);
});
```
- forEach() is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.

## for..of [New ]

- The for...of loop is used to loop over any type of data that is iterable.
- You write a for...of loop almost exactly like you would write a for...in loop, except you swap out in with of and you can drop the index.

```javascript
for(const name of names)}{
	console.log(name);
}
```

- This makes the for...of loop the most concise version of all the for loops.
- It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection
- But that's not all

### for..of advantages

- The for...of loop also has some additional benefits that fix the weaknesses of the for and for...in loops.

- You can stop or break a for...of loop at anytime and access the values directly

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```

- And you don’t have to worry about adding new properties to objects. The for...of loop will only loop over the values in the object.

```javascript
Array.prototype.decimalfy = function() {
  for (i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```
- doesn't print the function

### for..of usage

- Array, String, Map, Set and DomCollection and any object with Symbol.iterator prop defined are iterable as of now.
- if you call names.entries() you would see that it's returning an object called ArrayIterator with a function called next.
- That object is called an iterator
- we can call that function 
```
const nameIterator = names.entries();

nameIterator.next()
// returns an object with two properties
// {
//	 value: <the next array value from current postion
//	 done: false -- tells whether all the elements are iterated already
// }
```

- if we loop over the iterator with for..of
```
for(const name of names.entries()){
	console.log(name);
}
// will output [ arrayIndex, arrayvalueAtIndex]
// [0, 'luffy']
```

- we can use destructuring along with it
```
for(const [index, name] of names.entries()){
	console.log(index, name);
}
```

- can be used for arguments inside functions..
- arguments is an array like object but not an actual array. You can understand this if you look at it's __proto__ property.
- if you put it console you can see that it has a property Symbol.iterator
- this property is a function which makes an object iterable

```
function add(){
	let total = 0;
	for(const num of arguments){
		total += num;
	}
	return num;
}

// it's better to do this with
// convert arguments to array and use reduce
// use rest operator and reduce
```

- can be used for String since it is also iterable

```
const name = 'BalaManohar.B';
for(const char in name){
	console.log(char);
}
```

- loop over DOM elements

```
const ps = document.querySelectorAll('p');
//this will return a NodeList not an array but it is still iterable since it has the Symbol.iterator prop defined.
for(const paragraph of ps){
	paragraph.addEventListener('click', function(){
		console.log(this.textContent);
	})
}
```

### what is not iterable

- plain Objects are not iterable since it doesn't have Symbol.iterator defined.
- However there is a propsosal for Object.entries/ Object.values in TC39 which in stage 4.
- So we can use polyfills with entries.

```
const fruit = {
	name: 'apple',
	color: 'red',
	size: 'medium',
	weight: 50,
	sugar: 10
}

for ( const prop of Object.keys(fruit)){
	const value = apple[prop];
	console.log(value, prop);
}
```

- it's better to use for..in instead till we have for..of defined for Objects

### Make Objects iterable

- an iterator has next() method

```javascript
var obj = {
	//concise method
	[Symbol.iterator]() {
		var index = this.start, en = this.end;

		var it = {
			//since we need to access this
			next: () => {
				if( index <= en) {
					var v = this.values[index];
					index++;
					return { value: v, done: false }
				}
				else{
					return { done: true}
				}
				
			}
		}

		return it;
	},
	values: [ 2, 4, 6, 8, 10, 12, 14, 16, 18, 20],
	start: 4,
	end: 9

}

//now this object can called on spread 

var vals = [ ...obj ]
```
# The Iterable Protocol
The iterable protocol is used for defining and customizing the iteration behavior of objects. What that really means is you now have the flexibility in ES6 to specify a way for iterating through values in an object. For some objects, they already come built-in with this behavior. For example, strings and arrays are examples of built-in iterables.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for (const digit of digits) {
  console.log(digit);
}
```

## How it Works

In order for an object to be iterable, it must implement the iterable interface. If you come from a language like Java or C, then you’re probably familiar with interfaces, but for those of you who aren’t, that basically means that in order for an object to be iterable it must contain a default iterator method. This method will define how the object should be iterated.

The iterator method, which is available via the constant [Symbol.iterator], is a zero arguments function that returns an iterator object. An iterator object is an object that conforms to the iterator protocol.

# The Iterator Protocol

The iterator protocol is used to define a standard way that an object produces a sequence of values. What that really means is you now have a process for defining how an object will iterate. This is done through implementing the .next() method.

## How it Works

- An object becomes an iterator when it implements the .next() method. The .next() method is a zero arguments function that returns an object with two properties:

    - value : the data representing the next value in the sequence of values within the object
    - done : a boolean representing if the iterator is done going through the sequence of values

- If done is true, then the iterator has reached the end of its sequence of values. If done is false, then the iterator is able to produce another value in its sequence of values.

Here’s the example from earlier, but instead we are using the array’s default iterator to step through the each value in the array.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const arrayIterator = digits[Symbol.iterator]();

console.log(arrayIterator.next());
console.log(arrayIterator.next());
console.log(arrayIterator.next());
```

# New  Methods

- These methods 'from' and 'of' are not on the Array.prototype but on the Array object itself.
- This means actual array objects will not have them.
- converts array like objects to an actual array.

## Array.from

- signature

```
Array.from(arrayLikeObject, mapFunctionForConvertedArray);
```

- map function is optional

- convert document nodeList to array.

- arguments

```
function sumAll() {
	const nums = Array.from(arguments);
	return nums.reduce((prev, next) => prev + next, 0);
}
sumAll(2,194,12,3948,1934);
```

## Array.of

- creates an array from list of comma seperated parameters and returns it

```
Array.of(comma seperated values);
```

## Array.find

- available on array prototype
- similar to filter except it returns the first value from the array where the function returned true

```
//find first even number
const nums = [1,2,3,4,5,6,7];
const firstEven = nums.find(num => num % 2 === 0)
```

## Array.findIndex

- similar to find except it returns arrayIndex instead of the value

```
//find first even number
const nums = [1,2,3,4,5,6,7];
const firstEvenIndex = nums.findIndex(num => num % 2 === 0)
```

## Array.some

- returns true if at least one element is present satisfying the condition

```
//check if the array has atelast one even number
const nums = [1,2,3,4,5,6,7];
const isEvenPresent = nums.some(num => num % 2 === 0)
```

## Array.every

- returns true if all elements of the array satisfies the condition of the function

```
// check if all elements present in are array
const nums = [2,4,6,8,10];
const isAllNumsEven = nums.some(num => num % 2 === 0)
```

# ...spread and ...rest operator

- used on any object that is iterable on assignment context
- assignment context any place where a value is getting assigned to a variable.
- the ... operator consumes iterators, so there are only two places it can go. array literals and function arguments
- destructuring also consumes iterators internally


## spread operator usage

- spread the iterable object into seperate values, (i.e) unpacks an iterable object.

- copy an array into another array instead of mistakenly using object reference
```
const nums = [1,2,3];
const numsCopy = nums;
//changing numsCopy will affect nums as well since numsCopy is just a reference and not an actual copy of values
```
- instead use it like this

```
numsCopy = [...nums];
```

- copy multiple arrays
- concat multiple arrays with some values in middle.

```
multiArray = [...arr1, someValue1, someValue2, ...arr2]
```

- pass an array as a list of parameters to function

```
function printName(fName,lName){
	return `Hi there, ${fName} ${lName}`
}

var name = ['Light', 'Yagami']

console.log(printName(...name))
```

- make string to a char array

```
let str = 'spreadme'
let strArr = [...str]
```

- can be combined with destructuring

- to ignore, remove elements from an array.

## ...rest usage (gather)

- ... can be used at the recieving end (i.e) used for collecting or packing a un packed object

```
function sum(...nums){
	return nums.reduce((prev, cur) => prev + cur, 0)
}

console.log(sum(1,2,3,4,5,6,9))
```

- can be combined with destructuring

# Object literal syntax upgrades

## concise property Names
- if property name and variable name of value we are storing are same, we can do it like this

```
let fName = 'Light';
let lName = 'Yagami';
let series = 'DeathNote';

let charDetail = {
	fName,
	lName,
	series
};
```

## concise methods

- can loose the colon and function key words
- have to remember that this is the old function and not the new arrow function, so the 'this' keyword will work as usual.

```
let objectName = {
	functionName() {
		//do something here
	}
}
```

- concise methods do not have self reference so, they can't be used for functions that calls itself inside it since they are lexically anonymous
- this is because 

```
// this is perfectly legal
var objName = {
	"hello world"() {
		//can't come up with a name to self infer for this case
	}
}
```


## computed property names

- when the property name is a value stored in a variable
- we used to do like this

```
let propName = 'prop1';
let propVal = 'myVal'
let myObj = {};

myObj[propName] = propVal;
```

- it can be done like this

```
let propName = 'prop1';
let propVal = 'myVal'
let myObj = {
	[propName] : propVal
};
```

- any value javascript expression can replace propName

```
let keys = ['size', 'color' ];
let vals = ['medium', 'red'];
let tShirt = {
	[keys.shift()]: vals.shift(),
	[keys.shift()]: vals.shift()
}
```

## computed method names

- It's bit confusing to use this.

```
var someFuncName = 'someGetter';

var obj = {
	[someFuncName]() { },
	//any valid expression can be put in those brackets
};
```

## Computed Generator function name

```
// Normal generator function
var obj = {
	foo: function*() {}
}

//concise generator

var someGeneratorName = 'someFuncName'

var obj =  {
	*foo() {},
	//normal generator function
	*[someGeneratorName]() { }
	// computed generator function
}
```

# Promises

- kind of like an iou object for async stuff
- when we use fetch statement, a promise is return
- we can pass a callback function, to the promise.

```
let resp = fetch('some url');

resp.then(data => data.json())
.then(//process data)
.catch((err) => {
	//process error
})
```

- it's basically like async response

- But how do return our own promise objects ?

## creating promise

- usually some time counsuming process is run inside promise

- resolve to return processed to data
- reject raise exception

```
const p = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve("I'm returning some data from promise");
	}, 1000)
	
})

p
	.then(data =>{
		console.log(data);
	})
```

### using promises

- when we need flow control
- usually in the backend like nodejs

```

function getDataFromDB(id) {
	//create a new promise
	return new Promise((resolve, reject) => {
		//fetch data from db
		//do something with the data, pass it to a function may be or return it directly
		if(checkData()){
			resolve(data)
		}
		else{
			reject(Error('Data not found'));
		}
	})
}

//processor function
function processPromise(){
	getDataFromDB('47294')
		.then(data => data.json())
		.catch(err => {
			//handle error
		})
}
```

### Handling multiple promises


```
const promise1 = fetch('json_response_url_1');
const promise2 = fetch('json_response_url_2');

Promise
	//this one gets triggered only when we get data for all the promises mentioned in here
	.all([promise1, promise2])
	.then(rawResponses => {
		//process the raw response 
		return rawResponses.map( resp => resp.json())
	})
	.then(json_responses => {
		// process the json formatted data
	})
	catch(err => {
		// do something with the error
	});
```

# Symbol - The seventh new data type

> A symbol is a unique and immutable data type that is often used to identify object properties.

- symbol is a unique globally unguessable value within the context of a program
- it is never revealed to the user.
- usually used when prop name collision is expected.
- the label is just a description. it can be same.

```
const someVar = Symbol('a label');
```


```
const bala = Symbol('person');
const person = Symbol('person');

bala === person // will say false. No two Symbols can be same.
```

- Symbols aren't enumerable so it will not come in for..in
- because of this it's used in private variables as well
- But if we still want to get all the symbols in an object

```
const calssRoom = {
	[symbol('adam')]: {gender: 'male', region: 'unknown'},
	[symbol('adam')]: {
		gender: 'male', region: 'genesis'
	}
}

//this won't print anything
for( person in classRoom){
	console.log(person);
}

//to get all the symbol keys of an object
const syms = Object.getOwnPropertySymbols(classRoom);
console.log(syms);
// to get the data
const data = syms.map(sym => classRoom[sym]);
console.log(data);

```

# Code Quality

- ESLint
- Different from JSHint & JSLint

```
npm install -g eslint

> eslint file_path
```

- customizable through custom rules in .eslintrc
- this is a json file which contains the rules for linting

```
{
	"env": {
		"es6": true,
		"browser": true,
		"node": true
	},
	"extends": "eslint:recommended",
	//over riding extending rules
	"rules": {
		"no-console": 2 //options
	}
}
```

- airbnb's style guide 

https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb

- see installation guide
- after installing extend airbnb instead eslint default
- customize it if needed

- fixing space

```
eslint <filepath> --fix
```

- setting globals like library variables
- put this at the beginning of the js file.

```
/* globals twttr */
```

- polyfilling, overriding prototypes
- put this at the beginning of the file

```
/* eslint-disable no-extend-native */
```

- putting it at the beginning of the will apply for the entire file

- sometimes we might need it just for a particular in that case, just include it before the block and enable again like this

```
/* eslint-disable */
// copied function from somewhere
/* eslint-enable */
```

- there are many plugins for the type of file we write

- awesome eslint collection

https://github.com/dustinspecker/awesome-eslint

## how to use in sublime

- install eslint globally
- install sublimelinter plugin - this is a frame work for all other linters
- install sublimelint-contrib-eslint

## forcing eslint before commit

- we can make that by adding checks in hooks
- hooks are points in git process
- we can put our check in commit check
- .git/hooks/ folder contains all the hooks
- you can see .git/hooks/commit-msg.sample for example
- make a file .git/hooks/commit-msg
- put this code into that file

```
#!/bin/bash
files=$(git diff --cached --name-only | grep '\.jsx\?$')

# Prevent ESLint help message if no files matched
if [[ $files = "" ]] ; then
  exit 0
fi

failed=0
for file in ${files}; do
  git show :$file | eslint $file
  if [[ $? != 0 ]] ; then
    failed=1
  fi
done;

if [[ $failed != 0 ]] ; then
  echo "🚫🚫🚫 ESLint failed, git commit denied!"
  exit $failed
fi

```

# javascript modules

- just importing functions from other file or libraries
- but browsers don't support this natively so we need a bundler to bring them together.
- package.json - configuration of libraries/ packages involved
- webpack bundles everything and creates a single js file.

## configuring webpack

 -First Install your dependencies:

```bash
npm install webpack@beta babel-loader babel-core babel-preset-es2015-native-modules --save-dev
```

- Then, Create a `webpack.config.js` file:

```js
const webpack = require('webpack');
const nodeEnv = process.env.NODE_ENV || 'production';

module.exports = {
  devtool: 'source-map',
  entry: {
    filename: './app.js'
  },
  output: {
    filename: '_build/bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015-native-modules']
        }
      }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      },
      output: {
        comments: false
      },
      sourceMap: true
    }),
    new webpack.DefinePlugin({
      'process.env': { NODE_ENV: JSON.stringify(nodeEnv) }
    })
  ]
};
```

- Setup the build npm script in `package.json`:

```json
"build": "webpack --progress --watch"
```

## Creating Modules

- variables are always scoped to that module at the top level.
- before we can use any thing from a module, it should be exported.
- there are two types of exports
  - default export - can be imported as any name we like, usually used for the main 
thing that the module does
    - only one default export is allowed per file.
    - only default exported can be imported without any curly braces

```
// config.js file
// default export
const apiKey = 'aabc18483';
export default apiKey
```

- it will be imported like this

```
// .js is not needed here
import myApiKey from 'config'
// any name could be used instead of myApiKey
```

- named export - should be imported with the name it was exported as.
	- no restrictions on the number of named exports
	- it must be imported with in { } - this is not destructuring - just the syntax used by transpilers
	- can be imported with a different name using 'as'

- consider the file

```
// config.js file
// named exports
export default const entityId = '48rkcmw9c93wwe9ciwmr30dkkc8393'
export const apiKey = 'abcd'
export conts url = 'some api url'
export function sayHi(name) {
	console.log(`Hello here ${name}`);
}
const age = '70'
const area = 'adugodi'

export { age as oldAge, area };
```

- can be imported like this

```
import entityId, { apiKey, url as apiUrl, say Hi } from 'config'

//.js is not needed
//import both default and named exports
```

## systemjs

- it enables us to run without webpack precompiling and bundling
- this is a library which dynamically bundles 
- useful for fast testing or proof of concepts
- works only on server
- sample

```
//html page
<script src="https://cdn.polyfill.io/v2/polyfill.js"></script>
<script src="https://jspm.io/system@0.19.js"></script>
<script>
	System.config({ transpiler: 'babel' });
	System.import('./main.js');
</script>

//js importing from npm directly
import {sum, kebabCase} from 'npm:loadash'
```

## babel

- a javascript compiler
- since many browsers out there haven't implement es6 features, babel is needed

```
npm init
// creates package.json with initial set up for a javascript project
```


- [checkout babel repl](https://babeljs.io/repl/)

```
npm install bable-cli@next
//include next to install the latest version (beta)
```

- this will automatically add it to the 'package.json'

### plugins

- [babel plugins](https://babeljs.io/docs/plugins/)
- every js feature is listed as plugin for compiling them into es5
- a preset is a collection of plugins
- instead of listing the plugins one by one we can use preset.
- babel-preset-env is preset which is based on environment we are going to support like chrome browser, node etc..

```
npm install bable-preset-env
```

- instead of including a seperate .babelrc configuration, it can be added to package.json file itself by including 'babel' key

## Polyfill

- transpiler only converts the es6 syntax to es5
- but there are es6 methods
- these needs to be implement by us where the browsers don't support.
- usually mdn repo lists the polyfills for all methods.
- but this can be managed by polyfill scripts.
  - polyfill.io
    - this detects the user agent and sends the respective polyfill for it
  - babel polyfill

# Prototypal Inheritance Briefing

```
//constructor function

fuunction Adt(name){
	this.name = name;
}

let customArray = new Adt('customArray');
customArray.toString();
// customArray.toString is still acessible here

Adt.prototype.toString = function(){
	console.log('custom to String method');
}
```

# Classes

## ES5 "Class" Recap

Since ES6 classes are just a mirage and hide the fact that prototypal inheritance is actually going on under the hood, let's quickly look at how to create a "class" with ES5 code:

```javascript
function Plane(numEngines) {
  this.numEngines = numEngines;
  this.enginesActive = false;
}

// methods "inherited" by all instances
Plane.prototype.startEngines = function () {
  console.log('starting engines...');
  this.enginesActive = true;
};

const richardsPlane = new Plane(1);
richardsPlane.startEngines();

const jamesPlane = new Plane(4);
jamesPlane.startEngines();
```

In the code above, the Plane function is a constructor function that will create new Plane objects. The data for a specific Plane object is passed to the Plane function and is set on the object. Methods that are "inherited" by each Plane object are placed on the Plane.prototype object. Then richardsPlane is created with one engine while jamesPlane is created with 4 engines. Both objects, however, use the same startEngines method to activate their respective engines.

Things to note:

- the constructor function is called with the new keyword
- the constructor function, by convention, starts with a capital letter
- the constructor function controls the setting of data on the objects that will be created
"inherited" methods are placed on the constructor function's prototype object

Keep these in mind as we look at how ES6 classes work because, remember, ES6 classes set up all of this for you under the hood.

## ES6 Classes
Here's what that same Plane class would look like if it were written using the new class syntax:

```javascript
class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}
```

## Class is just a function

Just to prove that there isn't anything special about class, check out this code:

```javascript
class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}

typeof Plane; // function
```

## Usage

> Commas are not needed for class syntax


```
class Adt {
	constructor(name) {
		this.name = name;
	}

	toString() {
		console.log('this is a custom toString method');
	}
}

let customArray = new Adt('customArray');
customArray.toString();
```

## static methods

- similar to Array.of and Array.from
- these are similar to class methods in ruby.
- can be called only on the class directly

```
class Adt {
	static info() {
		console.log('This is a class for creating custom abstract data type');
	}
}

let customArray = new Adt();
customArray.info()
// this will throw error since it can be called // only on Adt itself.
// it should be called like this

Adt.info();
```

## getters and setters

```
class Adt {
	get description() {
		return `this is ${this.name} object created out of Adt`;
	}
	set name(value) {
		this.name = value;
	}
	get name() {
		return this.name;
	}
}

let customArray = new Adt('customArray');
customArray.name = 'newArray';
```

## Inheritance in ES5 (using prototype)

Compared to ES5 subclasses
Let's see this same functionality, but written in ES5 code:

```javascript
function Tree(size, leaves) {
  this.size = (typeof size === "undefined")? 10 : size;
  const defaultLeaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null};
  this.leaves = (typeof leaves === "undefined")?  defaultLeaves : leaves;
  this.leafColor;
}

Tree.prototype.changeSeason = function(season) {
  this.leafColor = this.leaves[season];
  if (season === 'spring') {
    this.size += 1;
  }
}

function Maple (syrupQty, size, leaves) {
  Tree.call(this, size, leaves);
  this.syrupQty = (typeof syrupQty === "undefined")? 15 : syrupQty;
}

Maple.prototype = Object.create(Tree.prototype);
Maple.prototype.constructor = Maple;

Maple.prototype.changeSeason = function(season) {
  Tree.prototype.changeSeason.call(this, season);
  if (season === 'spring') {
    this.syrupQty += 1;
  }
}

Maple.prototype.gatherSyrup = function() {
  this.syrupQty -= 3;
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
```

Both this code and the class-style code above achieve the same functionality.

## Inheritance in ES6 - using super and extends

```
class Tree {
  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
    this.size = size;
    this.leaves = leaves;
    this.leafColor = null;
  }

  changeSeason(season) {
    this.leafColor = this.leaves[season];
    if (season === 'spring') {
      this.size += 1;
    }
  }
}

class Maple extends Tree {
  constructor(syrupQty = 15, size, leaves) {
    super(size, leaves);
    this.syrupQty = syrupQty;
  }

  changeSeason(season) {
    super.changeSeason(season);
    if (season === 'spring') {
      this.syrupQty += 1;
    }
  }

  gatherSyrup() {
    this.syrupQty -= 3;
  }
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
```

> super creates a new object of the parent

Both Tree and Maple are JavaScript classes. The Maple class is a "subclass" of Tree and uses the extends keyword to set itself as a "subclass". To get from the "subclass" to the parent class, the super keyword is used. Did you notice that super was used in two different ways? In Maple's constructor method, super is used as a function. In Maple's changeSeason() method, super is used as an object!

### super - constraints

> super must be called before this

In a subclass constructor function, before this can be used, a call to the super class must be made.

```
class Apple {}
class GrannySmith extends Apple {
  constructor(tartnessLevel, energy) {
    this.tartnessLevel = tartnessLevel; // `this` before `super` will throw an error!
    super(energy); 
  }
}
```

## Another example

```
class Animal {
	constructor(name) {
		this.name = name;
		this.thirst = 100;
		this.belly = [];
	}

	drink() {
		this.thirst -= 10;
		return this.thirs;
	}

	eat(food) {
		this.belly.push(food);
		return this.belly;
	}
}

class Dog extends Animal {
	constructor(name, breed) {
		super(name);
		// before using this - super must be 
		this.breed = breed;
	}

	bark() {
		console.log('Woof Woof');
	}
}

let rhino = new Animal('Rhiney');

rhino.eat('shawarma roll');
let snickers = new Dog('snickers', 'King Charles');
```

- it's a good practice to not deeply extend.

## Extending native class

```
  class MovieCollection extends Array {
    constructor(name, ...items) {
      super(...items);
      this.name = name;
    }
    add(movie) {
      this.push(movie);
    }
    topRated(limit = 10) {
      return this.sort((a, b) => (a.stars > b.stars ? -1 : 1)).slice(0, limit);
    }
  }

  const movies = new MovieCollection('Wes\'s Fav Movies',
    { name: 'Bee Movie', stars: 10 },
    { name: 'Star Wars Trek', stars: 1 },
    { name: 'Virgin Suicides', stars: 7 },
    { name: 'King of the Road', stars: 8 }
  );

  movies.add({ name: 'Titanic', stars: 5 }); 
```

## Benefits of classes

### Less setup

- There's a lot less code that you need to write to create a function
- Clearly defined constructor function
- Inside the class definition, you can clearly specify the constructor function.

### Everything's contained

- All code that's needed for the class is contained in the class declaration. 
- Instead of having the constructor function in one place, then adding methods to the prototype one-by-one, you can do everything all at once!

## Things to look out for when using classes

1. class is not magic
    - The class keyword brings with it a lot of mental constructs from other, class-based languages. 
	- It doesn't magically add this functionality to JavaScript classes.
2. class is a mirage over prototypal inheritance
    - under the hood, a JavaScript class just uses prototypal inheritance.
3. Using classes requires the use of new
When creating a new instance of a JavaScript class, the new keyword must be used

# Sets

In ES6, there’s a new built-in object that behaves like a mathematical set and works similarly to an array. This new object is conveniently called a "Set". The biggest differences between a set and an array are:

- Sets are not indexed-based - you do not refer to items in a set based on their position in the set
- items in a Set can’t be accessed individually

Basically, a Set is an object that lets you store unique items. You can add items to a Set, remove items from a Set, and loop over a Set. These items can be either primitive values or objects.

- similar to array 
- is collection which stores only unique elements.
- it is not based on index like array, however it is iterable

To create a set

```
const games = new Set();
console.log(games);
```

If you want to create a Set from a list of values, you use an array:

```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);
```

## set - methods

- add() // add new value
- delete() // delete a value

```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');
games.add('Age of Empires');
games.delete('Super Mario Bros.');

console.log(games);
```
- clear() // empty the set - delete all elements
- size // to get the size - similar to length in Array

```
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
console.log(months.size);
```

- has() // check if the element exists - returns true or false

```
console.log(months.has('September'));
```

- values() // returns iterator .keys() is an alias for values()

```
console.log(months.values());
```

## Looping through Sets

If you remember back to our discussion on the new iterable and iterator protocols in ES6, then you’ll recall that Sets are built-in iterables. This means two things in terms of looping:

- You can use the Set’s default iterator to step through each item in a Set, one by one.
- You can use the new for...of loop to loop through each item in a Set.

### Using the SetIterator

Because the .values() method returns a new iterator object (called SetIterator), you can store that iterator object in a variable and loop through each item in the Set using .next().

```
const iterator = months.values();
iterator.next();
```
> Object {value: 'January', done: false}

And if you run .next() again?
```
iterator.next();
```
> Object {value: 'February', done: false}

And so on until done equals true which marks the end of the Set.

### Using a for...of Loop

An easier method to loop through the items in a Set is the for...of loop.

```
const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
for (const color of colors) {
  console.log(color);
}
```

## Weak Sets

- can only contain objects
- is not iterable i.e cannot be used in for..of
- a WeakSet does not have a .clear() method
- if the object stored in weak set is garbage collected i.e no longer used then it is removed from the weak set automatically
- You can create a WeakSet just like you would a normal Set, except that you use the WeakSet constructor.

```
let student1 = { name: 'James', age: 26, gender: 'male' };
let student2 = { name: 'Julia', age: 27, gender: 'female' };
let student3 = { name: 'Richard', age: 31, gender: 'male' };

const roster = new WeakSet([student1, student2, student3]);
console.log(roster);
```

> if you try to add something other than an object, you’ll get an error!

This is expected behavior because WeakSets can only contain objects. But why should it only contain objects? Why would you even use a WeakSet if normal Sets can contain objects and other types of data? Well, the answer to that question has more to do with why WeakSets do not have a .clear() method...

#### Garbage Collection

In JavaScript, memory is allocated when new values are created and is "automatically" freed up when those values are no longer needed. This process of freeing up memory after it is no longer needed is what is known as garbage collection.

WeakSets take advantage of this by exclusively working with objects. If you set an object to null, then you’re essentially deleting the object. And when JavaScript’s garbage collector runs, the memory that object previously occupied will be freed up to be used later in your program.

```
student3 = null;
console.log(roster);
```

What makes this so useful is you don’t have to worry about deleting references to deleted objects in your WeakSets, JavaScript does it for you! When an object is deleted, the object will also be deleted from the WeakSet when garbage collection runs. This makes WeakSets useful in situations where you want an efficient, lightweight solution for creating groups of objects.

# Map

- similar to Objects like how Sets are similar to Arrays
- has key value pairs

## Map - methods

- set method

```
let phonebook = new Map();

phonebook.set('Clark', 384930482);
phonebook.set('Kent', 739209384);
```

- delete method

```
phonebook.delete('Kent');
```

- clear method - To delete all keys

```
phonebook.clear();
console.log(phonebook);
```

>If you .set() a key-value pair to a Map that already uses the same key, you won’t receive an error, but the key-value pair will overwrite what currently exists in the Map. Also, if you try to .delete() a key-value that is not in a Map, you won’t receive an error, and the Map will remain unchanged.

>The .delete() method returns true if a key-value pair is successfully deleted from the Map object, and false if unsuccessful. The return value of .set() is the Map object itself if successful.

- has method - to check if a key exists - returns true or false

```
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));
```

- get() - method to retrieve the value of any key

```
console.log(members.get('Evelyn'));
```

## Looping through Map

You’ve created a Map, added some key-value pairs, and now you want to loop through your Map. Thankfully, you’ve got three different options to choose from:

1. Step through each key or value using the Map’s default iterator
2. Loop through each key-value pair using the new for...of loop
3. Loop through each key-value pair using the Map’s .forEach() method

### Using the MapIterator

Using both the .keys() and .values() methods on a Map will return a new iterator object called MapIterator. 

You can store that iterator object in a new variable and use .next() to loop through each key or value. Depending on which method you use, will determine if your iterator has access to the Map’s keys or the Map’s values.

```
let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();
```
> .keys() method like the name suggests, iterates through the keys till it is done.

> .values() method similarly iterates through the keys till it is done.

### Using a for...of Loop
Your second option for looping through a Map is with a for...of loop.

```
for (const member of members) {
  console.log(member);
}
```

- However, when you use a for...of loop with a Map, you don’t exactly get back a key or a value. Instead, the key-value pair is split up into an array where the first element is the key and the second element is the value.
- Remember destructuring ?

```
for (const [key, value] of members) {
     console.log(key, value);
}
```

### Using forEach loop

Your last option for looping through a Map is with the .forEach() method.

```
members.forEach((value, key) => console.log(key, value));
```

> Notice how with the help of an arrow function, the forEach loop reads fairly straightforward. For each value and key in members, log the value and key to the console.


## Usage

- it can have objects as keys.
- used for storing meta information about an object (i.e) usually dom nodes.

## WeakMap

> WeakMaps exhibit the same behavior as a WeakSets, except WeakMaps work with key-values pairs instead of individual items.

- a WeakMap can only contain objects as keys,
- a WeakMap is not iterable which means it can’t be looped and
- a WeakMap does not have a .clear() method.

```
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };

const library = new WeakMap();
library.set(book1, true);
library.set(book2, false);
library.set(book3, true);

console.log(library);
```

- If you try to add other than object it'll throw error.

- The garbage collection stuff and everything else is pretty much the same as Sets

# Promise - aysnc and wait

## Promises

A JavaScript Promise is created with the new Promise constructor function - new Promise(). A promise will let you start some work that will be done asynchronously and let you get back to your regular work. When you create the promise, you must give it the code that will be run asynchronously. You provide this code as the argument of the constructor function:

```javascript
new Promise(function () {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
    }, Math.random() * 2000);
});
```

This code creates a promise that will start in a few seconds after I make the request. Then there are a number of steps that need to be made in the createSundae function.

Indicated a Successful Request or a Failed Request
But once that's all done, how does JavaScript notify us that it's finished and ready for us to pick back up? It does that by passing two functions into our initial function. Typically we call these resolve and reject.

The function gets passed to the function we provide the Promise constructor - typically the word **"resolve"** is used to indicate that this function should be called when the request completes successfully. Notice the resolve on the first line:

```javascript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        resolve(sundae);
    }, Math.random() * 2000);
});
```

Now when the sundae has been successfully created, it calls the resolve method and passes it the data we want to return - in this case the data that's being returned is the completed sundae. So the resolve method is used to indicate that the request is complete and that it completed successfully.

If there is a problem with the request and it couldn't be completed, then we could use the second function that's passed to the function. Typically, this function is stored in an identifier called **"reject"** to indicate that this function should be used if the request fails for some reason. Check out the reject on the first line:

```javascript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});
```

So the reject method is used when the request could not be completed. Notice that even though the request fails, we can still return data - in this case we're just returning text that says we don't have the desired ice cream flavor.

A Promise constructor takes a function that will run and then, after some amount of time, will either complete successfully (using the resolve method) or unsuccessfully (using the reject method). When the outcome has been finalized (the request has either completed successfully or unsuccessfully), the promise is now fulfilled and will notify us so we can decide what to do with the response.

> Promises Return Immediately .The first thing to understand is that a Promise will immediately return an object.

```
const myPromiseObj = new Promise(function (resolve, reject) {
    // sundae creation code
});
```

That object has a .then() method on it that we can use to have it notify us if the request we made in the promise was either successful or failed. The .then() method takes two functions:

- the function to run if the request completed successfully
- the function to run if the request failed to complete

```javascript
mySundae.then(function(sundae) {
    console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
    console.log(msg);
    self.goCry(); // not a real method
});
```

As you can see, the first function that's passed to .then() will be called and passed the data that the Promise's resolve function used. In this case, the function would receive the sundae object. The second function will be called and passed the data that the Promise's reject function was called with. In this case, the function receives the error message "Sorry, we're out of that flavor :-(" that the reject function was called with in the Promise code above.

## Examples 

```
document.write('<video controls class="video_element"></video>')
const video = document.querySelector('.video_element');

navigator.mediaDevices.getUserMedia({ video: true }).then(mediaStream => {
  video.srcObject = mediaStream;
  video.load();
  video.play();
}).catch(err => {
  console.log(err);
})
```

## Calling multiple promises

```
function breathe(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('That is too small of a value');
    }
    setTimeout(() => resolve(`Done for ${amount} ms`), amount);
  });
}

breathe(1000).then(res => {
  console.log(res);
  return breathe(500);
}).then(res => {
  console.log(res);
  return breathe(600);
}).then(res => {
  console.log(res);
  return breathe(200);
}).then(res => {
  console.log(res);
  return breathe(500);
}).then(res => {
  console.log(res);
  return breathe(2000);
}).then(res => {
  console.log(res);
  return breathe(250);
}).then(res => {
  console.log(res);
  return breathe(300);
}).then(res => {
  console.log(res);
  return breathe(600);
}).catch(err => {
  console.error(err);
  console.error('YOU SCREWED');

})
```

## Changing with Async Await

- it's built on top of promises.
- it can't be used at the top level.
- must be in a function which is marked as async

```
function breathe(amount) {
  return new Promise((resolve, reject) => {
    if (amount < 500) {
      reject('That is too small of a value');
    }
    setTimeout(() => resolve(`Done for ${amount} ms`), amount);
  });
}

function catchErrors(fn) {
  return function (...args) {
    return fn(...args).catch((err) => {
      console.error('Ohhhh nooo!!!!!');
      console.error(err);
    });
  }
}

async function go(name, last) {
  console.log(`Starting for ${name} ${last}!`);
  const res = await breathe(1000);
  console.log(res);
  const res2 = await breathe(300);
  console.log(res2);
  const res3 = await breathe(750);
  console.log(res3);
  const res4 = await breathe(900);
  console.log(res4);
  console.log('end');
}

const wrappedFunction = catchErrors(go);

wrappedFunction('Light', 'Yagami');
```

## Awaiting multiple promises

```
// async function go() {
//   const p1 = fetch('https://api.github.com/users/wesbos');
//   const p2 = fetch('https://api.github.com/users/stolinski');
//   // Wait for both of them to come back
//   const res = await Promise.all([p1, p2]);
//   const dataPromises = res.map(r => r.json());
//   const [wes, scott] = await Promise.all(dataPromises);
//   console.log(wes, scott);
// }

// go();

async function getData(names) {
  const promises = names.map(name => fetch(`https://api.github.com/users/${name}`).then(r => r.json()));
  const people = await Promise.all(promises);
  console.log(people);
}

getData(['wesbos', 'stolinski', 'darcyclarke']);
```

## Promisifying functions

```
// navigator.geolocation.getCurrentPosition(function (pos) {
//   console.log('it worked!');
//   console.log(pos);
// }, function (err) {
//   console.log('it failed!');
//   console.log(err);
// });

function getCurrentPosition(...args) {
  return new Promise((resolve, reject) => {
    navigator.geolocation.getCurrentPosition(...args, resolve, reject);
  });
}

async function go() {
  console.log('starting');
  const pos = await getCurrentPosition();
  console.log(pos);
  console.log('finished');
}


go();
```

# Proxies!

 Reference : [proxy mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

To create a proxy object, we use the Proxy constructor - new Proxy();. The proxy constructor takes two items:

- the object that it will be the proxy for
an object containing the list of methods it will handle for the proxied object
- The second object is called the handler.

## A Pass Through Proxy

The simplest way to create a proxy is to provide an object and then an empty handler object.

```javascript
var richard = {status: 'looking for work'};
var agent = new Proxy(richard, {});

agent.status; // returns 'looking for work'
```

The above doesn't actually do anything special with the proxy - it just passes the request directly to the source object! If we want the proxy object to actually intercept the request, that's what the handler object is for!

The key to making Proxies useful is the handler object that's passed as the second object to the Proxy constructor. The handler object is made up of a methods that will be used for property access. Let's look at the get:

## Get Trap
The get trap is used to "intercept" calls to properties:

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};

const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```

In the code above, the handler object has a get method (called a "trap" since it's being used in a Proxy). When the code agent.status; is run on the last line, because the get trap exists, it "intercepts" the call to get the status property and runs the get trap function. This will log out the target object of the proxy (the richard object) and then logs out the name of the property being requested (the status property). And that's all it does! It doesn't actually log out the property! This is important - if a trap is used, you need to make sure you provide all the functionality for that specific trap.

Accessing the Target object from inside the proxy
If we wanted to actually provide the real result, we would need to return the property on the target object:

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName];
    }
};


const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```

Notice we added the return target[propName]; as the last line of the get trap. This will access the property on the target object and will return it.

Having the proxy return info, directly
Alternatively, we could use the proxy to provide direct feedback:

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        return `He's following many leads, so you should offer a contract as soon as possible!`;
    }
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`
```

With this code, the Proxy doesn't even check the target object, it just directly responds to the calling code.

So the get trap will take over whenever any property on the proxy is accessed. If we want to intercept calls to change properties, then the set trap needs to be used!

The set trap is used for intercepting code that will change a property. The set trap receives: the object it proxies the property that is being set the new value for the proxy

```
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
```

In the code above, notice that the set trap checks to see if the payRate property is being set. If it is, then the proxy (the agent) takes 15 percent off the top for her own commission! Then, when the actor's pay is set to one thousand dollars, since the payRate property was used, the code took 15% off the top and set the actual payRate property to 850;

## Other Traps
So we've looked at the get and set traps (which are probably the ones you'll use most often), but there are actually a total of 13 different traps that can be used in a handler!

the get trap - lets the proxy handle calls to property access
the set trap - lets the proxy handle setting the property to a new value
the apply trap - lets the proxy handle being invoked (the object being proxied is a function)
the has trap - lets the proxy handle the using in operator
the deleteProperty trap - lets the proxy handle if a property is deleted
the ownKeys trap - lets the proxy handle when all keys are requested
the construct trap - lets the proxy handle when the proxy is used with the new keyword as a constructor
the defineProperty trap - lets the proxy handle when defineProperty is used to create a new property on the object
the getOwnPropertyDescriptor trap - lets the proxy handle getting the property's descriptors
the preventExtenions trap - lets the proxy handle calls to Object.preventExtensions() on the proxy object
the isExtensible trap - lets the proxy handle calls to Object.isExtensible on the proxy object
the getPrototypeOf trap - lets the proxy handle calls to Object.getPrototypeOf on the proxy object
the setPrototypeOf trap - lets the proxy handle calls to Object.setPrototypeOf on the proxy object
As you can see, there are a lot of traps that let the proxy manage how it handles calls back and forth to the proxied object.

## Proxies vs ES5 Getters and Setters

Initially, it can be a bit unclear as to why proxies are all that beneficial when there are already getter and setter methods provided in ES5. With ES5's getter and setter methods, you need to know before hand the properties that are going to be get/set:

```javascript
var obj = {
    _age: 5,
    _height: 4,
    get age() {
        console.log(`getting the "age" property`);
        console.log(this._age);
    },
    get height() {
        console.log(`getting the "height" property`);
        console.log(this._height);
    }
};
```

With the code above, notice that we have to set get age() and get height() when initializing the object. So when we call the code below, we'll get the following results:

```javascript
obj.age; // logs 'getting the "age" property' & 5
obj.height; // logs 'getting the "height" property' & 4
```

But look what happens when we now add a new property to the object:

```
obj.weight = 120; // set a new property on the object
obj.weight; // logs just 120
```

Notice that a getting the "weight" property message wasn't displayed like the age and height properties produced.

With ES6 Proxies, we do not need to know the properties beforehand:

```javascript
const proxyObj = new Proxy({age: 5, height: 4}, {
    get(targetObj, property) {
        console.log(`getting the ${property} property`);
        console.log(targetObj[property]);
    }
});

proxyObj.age; // logs 'getting the age property' & 5
proxyObj.height; // logs 'getting the height property' & 4
```

All well and good, just like the ES5 code, but look what happens when we add a new property:

```javascript
proxyObj.weight = 120; // set a new property on the object
proxyObj.weight; // logs 'getting the weight property' & 120
```

See that?!? A weight property was added to the proxy object, and when it was later retrieved, it displayed a log message!

So some functionality of proxy objects may seem similar to existing ES5 getter/setter methods. But with proxies, you do not need to initialize the object with getters/setters for each property when the object is initialized.

# Generator functions

- a function which can be started and paused
- returns the next element in an object

```
{
	value: 'someval',
	done: 'true or false' // denotes if all elements are done.
}
```

- pause, unpause, get/yield, pause again

```
function *main() {
	console.log("hello");
	yield 10;
	console.log("hello again");
	yield 11;
}

// when main is called
// instead of executing it returns an iterator

var it = main()

it.next() // returns { value: 10, done: false} and pauses at line yeild 10
it.next() // returns { value: 11, done: false}
it.next() // returns { value: undefined, done: true}

```


- a loop with yield

```
function* incrementor(){
	let count = 1;
	while(true){
		yield count++;
	}
}

let counter = incrementor();
counter.next();
```

## Use cases for generator functions

- using ajax calls in sequence. (i.e) when the next call depends on the response of previous call.
- usually we do this with call back which often results in callback hell.


## for..of with generators

```
 function* lyrics(){
 	yield `But don't tell my heart`;
	yield `My achy breaky heart`;
	yield `I just don't think he'd understand`;
	yield `And if you tell my heart`;
	yield `My achy breaky heart`;
	yield `He might blow up and kill this man`;
  }

const achy = lyrics();

for (const line of achy) {
	console.log(line);
}
```

## custom iterators for objects

- generators make it easier to write custom iterators

```
var obj = {
	//concise method
	*[Symbol.iterator]() {
		for(let i = this.start; i <= this.end; i++){
			yield this.values[i];
		}
	},
	values: [ 2, 4, 6, 8, 10, 12, 14, 16, 18, 20],
	start: 4,
	end: 9

}

//now this object can called on spread 

var vals = [ ...obj ]
```

## Usage

- can do something like trim before setting value;
- can format when getting
- put checks for setters


# Class Properties

- not a part of es6 yet but heavily adopted by react community and bable supports this.

[Class Properties](https://babeljs.io/docs/plugins/transform-class-properties/)


# Padding Strings

- helps in alignment purposes

```
'test'.padStart(5);
'test'.padEnd(10);
```

# Exponential Operator

- **
- can be used as a replaced with **

# Trailing/Dangling comma

- usefull for git diff

```
const names = [
  'wes',
  'kait',
  'lux',
  'poppy',
];

const people = {
  wes: 'Cool',
  kait: 'EVen Cooler!',
  lux: 'Coolest',
  poppy: 'Smallest',
  snickers: 'Bow wow',
}

function family(
  mom,
  dad,
  children,
  dogs,
) {
	// do something here
}

```

# Object.entries() and Object.values()

- new static methods on object

```
const inventory = {
  backpacks: 10,
  jeans: 23,
  hoodies: 4,
  shoes: 11
};

// Make a nav for the inventory
const nav = Object.keys(inventory).map(item => `<li>${item}</li>`).join('');
console.log(nav);

// tell us how many values we have
const totalInventory = Object.values(inventory).reduce((a, b) => a + b);
console.log(totalInventory);

// Print an inventory list with numbers
Object.entries(inventory).forEach(([key, val]) => {
  console.log(key, val);
});

for (const [key, val] of Object.entries(inventory)) {
  console.log(key);
  if (key === 'jeans') break;
}
```

- cannot break away in forEach