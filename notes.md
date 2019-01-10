## require vs import

require loads the entire file but import can load the only required functions

## Named exports

http://exploringjs.com/es6/ch_modules.html

### Exporting

#### way 1

export const myVar = "val1";
export const myVar1 = "val2";

export const myFunct = () => "yo";

#### way 2

export const { myVar, myVar1 }

### importing

#### way 1

import { myVar, myFunc } from "package_path"

#### way 2 with alias

import { myVar as myCustomVar, myFunc as myCustomFunc } from "package_path"

#### way 3

import * as MyModule from "./MyComponent";
// use MyModule.MyVar and MyModule.myFunc

## Default Export

- cannot be used on var, let and const
- a file can have only one default export

```
// import
import MyDefaultComponent from "./MyDefaultExport";

// export
const MyComponent = () => {}
export default MyComponent;
```


## Regex

- using test on regex string
- using match on a string with regex
- using [] for defining character classes
- using [^negationString] for defining character classes
- using ^ and $ for identifying beginning and end of sring
- \w = [A-Za-z0-9_]
- \W = [^A-Za-z0-9_]
- \d = [0-9]
- \D = [^0-9]
- \s = [ \r\t\f\n\v]
- \S = [^ \r\t\f\n\v]
- specifying range for a pattern {start, end} inclusive of start.
- {3,} - 3 times or above
- {3} - exactly 3 times.
- positive look ahead and negative look ahead ?!= and ?=
- replace method

## Debugging

JavaScript recognizes six primitive (immutable) data types: Boolean, Null, Undefined, Number, String, and Symbol (new with ES6) and one type for mutable items: Object. Note that in JavaScript, arrays are technically a type of object.

- console.log()
- console.clear()
- typeof operator

### Truthy and Falsy values

#### Falsy Values

- false
- 0
- "" (an empty string)
- NaN
- undefined
- null

#### Truthy Values

- Everything except falsy values are true

### Common Mistakes

- variable name mis-spell
- matching (), {}
- using = instead of == or ===
- missing () at the end of calling function
- wrong order of passing arguments to function
- off by one error. array index starts at zero
- failing to re-initialize variable inside loop. consider 2-d array
- wrong terminating condition inside a loop

## Array Methods

- push
- pop
- shift
- unshift
- splice(startIndex, numberOfElementsToDelete, elementToBeInserted,elementToBeInserted..)
- slice(startIndex, endIndex+1)

## Copying Arrays

- slice can copy array
- [...myArrToBeCopied] also creates a copy of the array.
- [1,2,"one",...myArrToBeCopied, "five", 6]

## finding Elements in array

- indexOf(elementToBeLookedUp) - returns -1 if not found else index of element

## Objects

### Accessing

```
var myObj = { key1: 100, key2: 200};
myObj.key1 = 1000
myObj[key1] = 2000// used mostly when passing arguments or when the key name has space or other characters
```

```
for (let user in users){
  //user is the key
  //can be accessed like users[user]
}
```

```
Object.keys(myObject) //returns array of keys of an myObject
```

## Some handy functions

- map

```
result = arr.map((arrElement) => operateOn(arrElement) )
```

- reduce

```
result = arr.reduce((accumulator, currentVal) => accumulator + currentVal, initialValue);
```

- max

```
Math.max(1,2,3)
Math.max(...arr)
```

### Object constructor

```
function MyObjectConstructor() {
  this.key1 = "value1";
  this.key2 = "value2"'
}
```
to call this

```
let obj1 = new MyObjectConstructor();
```

- only with the new key "this" will mean to a new object.

### methods on objects

- instanceof 
- returns true or false to verify whether a newly created object was created by a constructor.

```
obj1 instanceof MyObjectConstructor;
```

- hasOwnProperty

```
myObj1.hasOwnProperty(propName)
```

- prototype property on constructor function. keys added to this are common to all objects created by the constructor

```
MyObjectConstructor.prototype.commonKey1 = "yolo";
```

- constructor property on every object refers to its contructor function. But this can be over written.

```
myObj1.constructor === myObjectConstructor
```

- bulk assigning of keys on prototype

```
MyObjectConstructor.prototype = {
  commonKey1: "some val 1",
  commonKey2: "soe val 2"
  .
  .
  .
  constructor: MyObjectConstructor
}
```

- it is necessary to manually set the constructor key since it will be over ridden.

- isPrototypeOf - to find if an object has the prototype of a Constructor

```
function Dog(name) {
  this.name = name;
}

let beagle = new Dog("Snoopy");

// Add your code below this line
Dog.prototype.isPrototypeOf(beagle)
```
- Every object has prototypes except a few. So prototype itself can have prototype. Object.prototype is the super prototype. For eg: hasOwnProperty is part of Object.prototype