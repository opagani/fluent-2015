# ES6 in Thoery and Practice
[Axel Rauschmayer (Ecmanauten)](http://ecmanauten.de/), [Aaron Frost (Domo)](http://domo.com/)  
[Details](http://fluentconf.com/javascript-html-2015/public/schedule/detail/38811)  
[Slides](https://speakerdeck.com/btholt/react-with-es6)  
[Github](https://github.com/aaronfrost/es6-workshop)  

Learn about ECMAScript6 new features.

## Notes

#### Background
* ECMAScript:  official name of JavaScript  
* ECMAScript5:  ES5 - the default JavaScript now  
* ECMAScript6:  ES6 or ECMAScript2015  - it is done  
* ECMAScript Harmony:  improvements after ECMAScript5, ECMAScript 6 and later  
* ES7:  coming soon  
* [ES6 browser compatibility table](https://kangax.github.io/compat-table/es6/) 

The goal for ES6 is to make JavaScript better for:  complex applications and libraries.

#### New Features in ES6
* Better syntax
  * Block-scoped variables
  * Destructuring 
  * Modules
  * Parameter handling
  * Arrow functions
  * Classes
  * Template literals
  * Object.assign()


* Better Library
  * new methods for strings and arrays
  * promises
  * maps, sets

*  Completely new
  * Generators
  * Proxies
  * WeakMaps   

#### Block-scoped variables
```
// ES5 - default JavaScript in the browsers now
// Function scope (var)

function order(x, y) {
  if (x > y) {
    var tmp = x;
    x = y;
    y = tmp;
  }
  console.log(tmp===x);  // true
}
```

```
//This is what really happens:
// Function scope (var)

function order(x, y) {
  var tmp;  //  undefined
  if (x > y) {
    tmp = x;
    x = y;
    y = tmp;
  }
  console.log(tmp===x);  // true
}
```
```
// ES6
// Block scope (var)

function order(x, y) {
  if (x > y) {
    let tmp = x;
    x = y;
    y = tmp;
  }
  console.log(tmp===x);  // ReferenceError;  tmp is not defined
}
```

#### Destructuring
##### Destructuring Objects
```
function getAddress(){
  return {
    city: "Salt Lake City",
    state: 'UT',
    zip: 84115,
    coords: {
      lat: 40.776608,
      long: -111.920485
    }
  };
}

// Call `getAddress()` and create a 'city', 'state' and 'zip' variable.
// Without destructuring:  ES5

var address = getAddress();      
var city = address.city;         // city: "Salt Lake City"
var state = address.state;       // state: "UT"
var zip = address.zip;           // zip: 84115

// With destructuring: ES6

var {city, state, zip} = getAddress();     //  city: "Salt Lake City", state: "UT", zip: 84115
```

##### Destructuring Arrays
```
function getNumbers(){
  return [1, 2, 3, 4, 5, 6];
}

// Call getNumbers and pull the first value out as `one` and the second as `two` - ES6
[one, two] = getNumbers();     //  one is 1, and two is 2

[one, ,three] = getNumbers();  //  you can skip values, one is 1 and three is 3

```

#### Modules
```
// lib/math.js
var notExported = 'abc';

export function square(x) {
  return x * x;    
}

export const MY_CONSTANT = 123;
```

```
// main1.js
import {square} from 'lib/math';
console.log(square(3));    // 9
```

```
// main1.js
import * as math from 'lib/math';
console.log(math.square(3));    // 9
```

#### Parameter handling
##### Parameter default values
```
// Use a default if parameter is missing

function func1(x, y='default') {
  return [x, y];  
}

// Interaction:

> func1(1,2)
[1, 2]

> func1()
[undefined, 'default']
```

##### Rest parameters
```
// Put trailing parameters in an array

function func2(arg0, ...others) {
  return others;  
}

// Interaction:

> func2('a', 'b', 'c', 'd')
['b', 'c', 'd']

> func2()
[]
```

##### NO need for arguments anymore!!

```
// ES5
function func() {
  [].forEach.call(arguments,         // using call to invoke an anonymous function 
    function(x) {...});              // use call to invoke an anonymous function on every object of the array
  ...  
}
```

```
//ES6
function func(...args) {
  for (let arg of args) {
    ...
  }
}
```

#### Spread operator (...)
##### function arguments
```
//Turn an array into function arguments -  the inverse of rest parameters

Math.max(...[7, 4, 11]);  // 11  very useful for really long arrays
```

```
let arr1 = ['a', 'b'];
let arr2 = ['c', 'd'];

arr1.push(...arr2);      // arr1 is now ['a', 'b', 'c', 'd']
```

```
// Also works in constructors!
new Date(...[1912, 11, 24])   // Christmas Eve 1912
```

##### array elements
```
let a = [1, ...[2,3], 4];    // [1, 2, 3, 4]

// Concatenate arrays
let x = ['a', 'b'];
let y = ['c'];
let z = ['d', 'e'];

let xyz = [...x, ...y, ...z];    // ['a', 'b', 'c', 'd', 'e']
```

#### Arrow functions
##### less to type
```
let arr = [1, 2, 3];
let squ;

// ES5
sqt = arr.map(function(a) {        // map is an existing feature of ES5
  return a * a;                    // it performs an operation on every element of the array
});                                // it returns a new array

// ES6
squ = arr.map(a => a * a);
```

##### lexical this, no more that=this
```
function UiComponent {
  var that = this;
  var button = document.getElementById('myButton');
  button.addEventListener('click', function() {
    console.log('CLICK');
    that.handleClick();
  });
}

UiComponent.prototype.handleClick = function() { ... };
```
```
UiComponent {
  let button = document.getElementById('myButton');
  button.addEventListener('click', () => {
    console.log('CLICK');
    this.handleClick();
  });
}

UiComponent.prototype.handleClick = function() { ... };
```

#### Classes
```
// ES5

function Person(name) {
    this.name = name;
}

Person.prototype.describe = function() {
  return 'Person called ' + this.name;
};

var person = new Person('Oscar');
person.describe();
```

```
// ES6

class Person {
  constructor(name) {
    this.name = name;
  }
  describe() {
    return 'Person called ' + this.name;
  }
}

let person = new Person('Oscar');
person.describe();
```

##### Subclassing
```
// ES6

class Employee extends Person {
  constructor(name, title) {
    super(name);
    this.title = title;
  }
  describe() {
    return super.describe() + ' (' + this.title + ')';
  }
}

let employee = new Employee('Oscar', 'Engineer');
employee.describe();
```

```
// ES5

function Employee(name, title) {
  Person.call(this, name);
  this.title = title;
}

Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee;

Enployee.prototype.describe = function() {
  return Person.prototype.describe.call(this) + ' (' + this.title + ')';
};

var employee = new Employee('Oscar', 'Engineer');
employee.describe();

```

#### Template literals
```
// String interpolation
// ES6

if (x > MAX) {
  throw new Error(
    `At most ${MAX} allowed: ${x}!`
  );  
}
```

```
// ES5

if (x > MAX) {
  throw new Error(
    'At most ' + MAX + ' allowed: ' + x + '!''
  );  
}
```

#### Object.assign()
* Object.assign(target, source_1, source_2, ...)
  * Merge source_1 into target
  * Merge source_2 into target
  * etc.
  * return target

#### ES6 vs lodash or Underscore.js
```
let obj = { foo: 123 };

// ES6
Object.assign(obj, { bar: true });      // obj is now { foo: 123, bar: true }  

// lodash/Underscore.js
_.extend(objs, { bar: true });          // also:  _.assign(...)
```

#### ES6 tools
* Transpiler
  * [Babel] (https://babeljs.io/)
  * Traceur
  * TypeScript

* Package manager
  * np
  * jspm

* Module system
  * [webpack] (http://webpack.github.io/)
  * [Browserify] (http://browserify.org/)
  * RequireJS

* Linter
  * ESLint
  * JSHint
  * JSLint 

* Shims for ES5
  * es6-shim

#### Babel
Babel is a JavaScript compiler that uses next generation of JavaScript.

##### Running Babel from CLI 

```
// Install
$ npm install -g babel


// Usage
$ babel script.js
```

##### Running Babel from the Browser
```
// Install
Available from browser.js inside the folder of a babel-core npm release.

// Usage
Add the type="text/babel" attribute to your <script> tags. For example:
```
```
<script src="node_modules/babel-core/browser.js"></script>
<script type="text/babel">
  class Test {
    test() {
      return "test";
    }
  }

  var test = new Test;
  test.test(); // "test"
</script>
```

##### Running Babel from Browserify
```
// Install
$ npm install --save-dev babelify

// Usage
$ browserify script.js -t babelify --outfile bundle.js
```

##### Running Babel from Webpack
```
// Install
$ npm install --save-dev babel-loader

// Usage via config
module: {
  loaders: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader"}
  ]
}
```

#### Webpack
Module bundler.

```
// Install: This makes the webpack command available.

$ npm install webpack -g
```

```
// Example:  Start with a empty directory. Create these files:

// entry.js
document.write("It works.");
```

```
// index.html
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <script type="text/javascript" src="bundle.js" charset="utf-8"></script>
  </body>
</html>
```

```
// Usage
$ webpack ./entry.js bundle.js

// open index.html in your browser.  It should display:  It works.
```

#### Browserify
* Browserify lets you require('modules') in the browser by bundling up all of your dependencies.  
* Browsers don't have the require method defined, but Node.js does. 
* With Browserify you can write code that uses require in the same way that you would use it in Node.

```
// Install
$ npm install -g browserify
```

```
// Example - from browserify.org
// file:  main.js

var unique = require('uniq');

var data = [1, 2, 2, 3, 4, 5, 5, 5, 6];

console.log(unique(data));
```
```
// Install the uniq module with npm:
$ npm install uniq

// Bundle up all the required modules starting at main.js into a single file called bundle.js
$ browserify main.js -o bundle.js

// Add this to the index.html file
<script src="bundle.js"></script>
```















