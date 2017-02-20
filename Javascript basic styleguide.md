# Javascript basic styleguide

`Work in progress ...` 

This is one article from a series that covers all front end basic style guide:

* [HTML/CSS basic style guide](https://assist-software.net/blog)
* Javascript basic styleguide
* [Tools to enforce HTML/CSS guidelines](https://assist-software.net/blog)
* [Tools to enforce the JS guidelines](https://assist-software.net/blog)
* [Git hooks for automation](https://assist-software.net/blog)

This is just another article in the wild web about guidelines.
From my experience all the discussions around style guides are mostly subjective, and a matter of prefference/habit. We have different backgrounds or learning paths, ...
This is wanted to be just a basic styleguide, which is generally valid for both plain Javascript and ES6.

## The "Rules":

### Use 2 spaces for indentation.

```js
// Right:
function add(a, b) {
  return a+b;
}

// Wrong:
function add(a, b) {
    return a+b;
}
```

We all have different prefferences when comes to text editors and IDE's, but configure it wrong and your first commit will result in a crazy diff that most likely will be very hard to reason about(i mean if you practice the code reviews and you should, trust me).

### No unused variables.
Unused variables will polute the context and will make the code harder to reason about.

### Use semicolons
I know is old style, but we sometimes work on legacy code, and in some cases can provide some information about where a statement ends.

### Write each declaration in its own statement.

```
// Right:
var userPermissions = require('db').Permissions(currentUser);
var hasAccess = require('security').AccessFactory(userPermissions);
var errors = requre('errors').security;

 
// Wrong:
var userPermissions = require('db').Permissions(currentUser), hasAccess = require('security').AccessFactory(userPermissions), errors = requre('errors').security;

// or:
var userPermissions = require('db').Permissions(currentUser),
    hasAccess = require('security').AccessFactory(userPermissions),
    errors = requre('errors').security;

```

I made the above example a bit more complex only to emphasize the fact that in a real-life-ish situations you would need to pay extra attention reading the second declaration, and you would have to reason about if the statement is a declarion or an assignation in the last example. I know most of the operations in the above example will happen asyncronuous, that's why i put an "ish" after real-life.

### Use single quotes, unless you are writing JSON.

```js
// Right
var message = 'Okay';

//Wrong
var message = "Im a bad example";
```

I have no practical reason for this one, is just for consistency.

### Use === and avoid ==

```js
var isAdmin = true;
var stupidMistake = 1;

//Right
if(isAdmin === stupidMistake) {
  launchNuke();
}

//Wrong
if(isAdmin == stupidMistake) {
  launchNuke(); // congrat's you just stared WWx
}
```
The example above sucks, i need a better one.

### Use multi-line ternary operator

```js
//Right:
var numPixels = (config && config.pixels)
 ? config.pixels
 : 100;

//Wrong:
var numPixels = (config && config.pixels) ? config.pixels : 100;
```
