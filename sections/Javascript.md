[Back to Home](../README.md)
# Javascript

As described in the general rules, consistency will always win over style. In the end it does not matter which style you are using, you just have to be consistent in order for your code to be more readable by others, because they will get used to it.

Following text is not a set of rules, but rather just recommendations how to write javascript code in general.

## ECMA what?

Nowadays, you can use two styles when writing Vanilla Javascript or NodeJS code. Traditional, old `ECMAScript5` syntax or new `ECMAScript2015` syntax. Even though most of the new syntax is just syntactic sugar, there are some differences in what some syntax actually means.

In order to ensure the compatibility with older web browsers, new syntax is usually being translated into the old one anyway. But some of the differences will be present even then.

At Sleighdogs, we are enthusiastic about new things and I would recommend using the new syntax over the old one. But beware, always try to use translators for production code in order to maximize compatibility.

From now on, I will try to explain some new syntax constructs examples and where possible - accompanied with old syntax to give you a sneak peek how much better the new syntax is.

**Recommendation #1: Prefer new syntax over old one where possible.**

## Semicolons

Javascript syntax is a C-like syntax. Usually, statements and expressions are terminated with semicolon character `';'`. Even though javascript interpreter does not require semicolon to be present in the code, it is a nice rule to end all the expressions and statements with semicolon. Here is an example:

```
#!javascript
var _ = require('lodash');

var firstArray = [0, 1, 2, 3, 4];
var secondArray = [5, 6, 7, 8, 9];

var concatenatedArray = _.concat(firstArray, secondArray);

console.log(concatenatedArray);
// => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

However, with the rise of new syntax, semicolons are usually omitted and are inserted only in specific circumstances where you need to put more expressions or statements in one row. While new syntax is usually translated into old one when going into production, the translator usually adds all the semicolons for us anyway. Here is an example of the code above written in the new syntax:

```
#!javascript
import _ from 'lodash'

const firstArray = [0, 1, 2, 3, 4]
const secondArray = [5, 6, 7, 8, 9]

const concatenatedArray = _.concat(firstArray, secondArray)

console.log(concatenatedArray)
// => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

For now, please do mind just the semicolons, we will get to other things later.

** Recommendation #2: With old syntax use semicolons, with new syntax use only where needed specifically.**

## Variables

In older syntax you had only one type of variable which had to be declared with keyword `var`. The variable created in this way is subject to a process called `variable hoisting` and such variable would have `function scope` or a `global scope` if not defined within a function's body. Usually a variable declaration together with an assignment would look like this:

```
#!javascript
var variableName = 60;
```

In new syntax you can use three types of variables. There is the old `var` type and two new ones - `const` and `let`. With the old `var` has the same behavior as in old syntax. However, it is highly recommended to use either `let` or `const` instead of 'var' where possible to make your code more efficient and performant. Here are some new syntax declarations with assignments:

```
#!javascript
var functionScopeVariable = 60
let blockScopeVariable = 30
const constantVariable = 'ECMAScript2015 FTW'
```

You use `const` when you are certain, that the variable will not change after it assigned a value. In essence, you are making it a constant.

You use `let` when you are certain, that the variable might or will be reassigned with new value. You might think, well, for this purpose I have `var` here, don't I? Well, yes and no. Variables created with `let` have a different scope and that is `block scope` - here, there is your difference, and it is a big one.

**Recommendation #3: Prefer using `const` or `let` over `var` where possible.**

## Functions

In old syntax you had couple of ways how to define a function but each one of them have been pretty verbose and involved using a keyword `function`, here are some examples:

```
#!javascript
// anonymous function declaration
function(a) {
  return a++;
}

// named function declaration
function add(a, b) {
  return a + b;
}

// anonymous function statement
var subtract = function(a, b) {
  return a - b;
}

// named function statement
var multiply = function multiply(a, b) {
  return a * b;
}
```

As you can see, the code is pretty verbose and each function declaration / statement involves usage of `function` keyword.

New syntax however introduces `arrow functions`, which tries to be more concise and shrinks the syntax where possible to bare minimum. See for yourselves:

```
#!javascript
// anonymous function declaration
(a) => a++

//anonymous function statement
const add = (a, b) => a + b
```

See? Much less code. But beware! There are myriads of differences you have to be aware of. What are the differences? Well one might spot the first one right from the example. There are no named declarations and no named statements for arrow functions. Arrow functions have different scope of special `this` variable inside the function. One cannot use them as constructors with `new` operator, and to top it even more, they don't have special variable called `arguments`. If you are aware of these tradeoffs and you are willing to sacrifice them (you usually are), you can switch the old function syntax for the new arrow function syntax.

**Recommendation #4: Prefer using arrow syntax over traditional function syntax where possible.**

## Default argument values

Having default parameters values is a pretty common feature of other programming languages. Javascript however does not have this feature. For a long time people have been emulating this behavior like so:

```
#!javascript
function createPersonObject(name, age) {
  name = name || 'John Doe';
  age = age || 24;

  return {
    name: name,
    age: age,
  };
}
```

Even though I used the most concise syntax possible, this is still to verbose. So lets have a look how we can give parameters their default values in new syntax:

```
#!javascript
const createPersonObject = (name = 'John Doe', age = 24) => {  
  return {
    name: name,
    age: age,
  }
}
```

**Recommendation #5: Prefer using default parameters over being too verbose.**

## Object creation

New syntax goes even further when verbosity is at stake. Remember the previous example in new syntax? Isn't it too much that you have to write the variable names for name and age twice? Well, say hello to new syntax naming feature. If you ever find yourself in a situation when you are creating an object with properties with the same name as your variables or arguments, you can write them just once, the interpreter will figure it out. So our previous example can be written in even more concise way:

```
#!javascript
const createPersonObject = (name = 'John Doe', age = 24) => {  
  return {
    name,
    age,
  }
}
```

**Recommendation #6: Prefer new syntax naming feature where possible.**

## Destructors
There is no such thing in older javascript syntax, but I am pretty sure you have been emulating it in some way. Let's have an example:

```
#!javascript
var extractPostalInfo = function(user) {  
  var name = user.name;
  var surname = user.surname;
  var street = user.address.street;
  var number = user.address.number;
  var zip = user.address.zip;
  var city = user.address.city;
  var country = user.address.country;

  return {
    name: name + ' ' + surname;
    address: street + ' ' + number + ', ' + zip + ' ' + city + ', ' + country;
  };
}
```

Here you can see there are series of variable declarations and extracting them from object. Perhaps you hvae done in million times, maybe never and use another technique, but know this. New syntax destructors feature to the rescue. What destructors do, is that they look at an object and grab some properties from it and making them available as variables. In other words it does exactly the same as above, but in much more concise way. See for yourselves:

```
#!javascript
var extractPostalInfo = (user) => {
  const { name, surname, address: { street, number, zip, city, country } } = user

  return {
    name: name + ' ' + surname;
    address: street + ' ' + number + ', ' + zip + ' ' + city + ', ' + country;
  }
}
```

Isn't that fantastic? As you can see you can even go deeper into embedded objects as in address's case.

**Recommendation #6: Prefer destructors when accessing objects properties and referencing them through variables.**

## Spread operator

Oh boy, I wish older syntax had something like this. If you are doing javascript for a while, you surely have written similar piece of code (Please bare in mind that this is just for the sake of an example, I would use some library like `underscore` or `lodash` in real world for this):

```
#!javascript
const composedObject = {}

for (var property in firstObject) {
  if (firstObject.hasOwnProperty(property)) {
     composedObject[property] = firstObject[property];
  }
}

for (var property in secondObject) {
  if (secondObject.hasOwnProperty(property)) {
     composedObject[property] = secondObject[property];
  }
}
```

Spread operator or `...variableName` is used when you need to iterate over object properties or an array and add or copy them to another object / array. This feature can be heavily used in array concatenations, or object composition situations. This piece of code is much more concise than the previous one

```
#!javascript
const composedObject = { ...firstObject, ...secondObject }

```

See what I am talking about?

**Recommendation #7: Use spread operator where possible, it will make your life easier.**

## Where to go from here?

Even though we went through a lot together, there are a lot more things in new syntax.

**DISCLAIMER:** Be sure to have a deeper look at those features on MDN (Mozilla Developer Network) site, because there are all the bits and pieces of the new functionalities. You might save yourself a lot of time and a lot of hair, when you will know exactly what is going on, instead just relying on this - really short -guide.
