# Javascript basic coding style guideline

`Work in progress ...` 

This post is part of the "Basic Frontend Coding Style Guide" which will cover all front end basic style guide, and some tools to help us with automation:

* [HTML/CSS basic style guide](https://assist-software.net/blog)
* Javascript basic styleguide
* [Tools to enforce HTML/CSS guidelines](https://assist-software.net/blog)
* [Tools to enforce the JS guidelines](https://assist-software.net/blog)
* [Git hooks for automation](https://assist-software.net/blog)

## The burden of a dynamic environment
I'm talking about software development ofcourse. How can we maintain consistency in long term projects? Given that, people will come and go, projects will come and go, frameworks will come and gues what, they will be phased out. Well following the same style guide will be a good start, and will provide consistency across projects, or at least across one project.
From my experience all the discussions around style guidelines are mostly subjective, and a matter of prefference/habit. We have different backgrounds or learning paths and this models our perception about what we consider to be readable or easy to reason about. 

> Any fool can write code that a computer can understand. Good programmers write code that humans can understand.

_Martin Fowler_

The machines are all the same, and they will understand the same thing from your code, no matter how is written. We are humans and we are all different and that's a good thing. So when it comes to writing readable code for humans there is no one set of rules to fit them all. So lets think about the guidelines below more as a convention, and less as a best practice.

## The goal

* To be just a basic styleguide, which is generally valid for both plain Javascript and ES6.
* To have a very low friction with the process of learning/adaptation.

## The "Rules":

### Use 2 spaces for indentation.

```js
// ok:
function add(a, b) {
  return a + b;
}

// avoid:
function add(a, b) {
    return a + b;
}
```

We all have different prefferences when comes to text editors and IDE's, but configure it wrong and your first commit will result in a crazy diff that most likely will be very hard to reason about(i mean if you practice the code reviews and you should, trust me).

### No unused variables.
Unused variables will polute the context and will make the code harder to reason about.

### Use semicolons
I know is old style, but we sometimes maintain legacy code, and in some cases can provide some information about where a statement ends.

### Write each declaration in its own statement.

```js
// ok:
var userPermissions = require('db').Permissions(currentUser);
var hasAccess = require('security').AccessFactory(userPermissions);
var errors = requre('errors').security;

 
// avoid:
var userPermissions = require('db').Permissions(currentUser), hasAccess = require('security').AccessFactory(userPermissions), errors = requre('errors').security;

// or:
var userPermissions = require('db').Permissions(currentUser),
    hasAccess = require('security').AccessFactory(userPermissions),
    errors = requre('errors').security;

```

I made the above example a bit more complex only to emphasize the fact that in a real-life-ish situations you would need to pay extra attention reading the second declaration, and you would have to reason about if the statement is a declarion or an assignation in the last example. I know most of the operations in the above example will happen asyncronuous, that's why i put an "ish" after real-life.

### Use single quotes, unless you are writing JSON.

```js
// ok:
var message = 'Okay';

// avoid:
var message = "Im a bad example";
```

I have no practical reason for this one, is just for consistency.

### Use === and avoid ==

```js
var isAdmin = true;
var stupidMistake = 1;

// ok:
if(isAdmin === stupidMistake) {
  launchNuke();
}

// avoid:
if(isAdmin == stupidMistake) {
  launchNuke(); // congrat's you just stared WWx
}
```
The example above sucks, i need a better one.

### Use multi-line ternary operator

```js
// ok:
var numPixels = (config && config.pixels)
 ? config.pixels
 : 100;

// avoid:
var numPixels = (config && config.pixels) ? config.pixels : 100;
```

You can easely separte the condition and the possible outcomes.

### Space infix operators

```js
// ok:
var x = 2;
var square = x * x;

// avoid:
var x=2;
var square=x*x; 
```
So the code doesn't look like a cryptic message, and also you can navigate more easely using only the keyboard.

### Commas should have a space after

```js
// ok:
var max = Math.max(10, 20);
var magicNumbers = [1, 4, 6, 88];
var users = getUsers(companyId, role);

// avoid:
var max = Math.max(10,20);
var magicNumbers = [1,4,6,88];
var users = getUsers(companyId,role);
```

### Else statements should be on the same line as their curly braces.

```js
// ok:
if(hasAccess) {
  executeAction();
} else {
  doNothing();
}

// avoid:
if(hasAccess) {
  executeAction();
} 
else {
  doNothing();
}
```

Is easier to follow the code path. In some cases, based on the lines visible in the view port and your boredom, you may suppose there is no else statement, if the closed curly brace is alone on the line.

### Always prefix custom globals
