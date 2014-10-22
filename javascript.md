## Indenting
* Never mix tabs and spaces
* Use 2 spaces for indenting

## Data types
* Never use `new` to create a new variable. use [] for array, {} for object

```javascript
// bad
var item = new Object(),
  array = new Array(),
  string = new String();

// good
var item = {},
  array = [],
  string = '';
```

## Functions
* Always try to initiate variables in the first line

```javascript
// bad
var foo = function () {
  function2();
  var a = 1;
  function3(a);
}
// good
var foo = function() {
  var a = 1;

  function2();
  function3(a);
}
```

* Group `var` statements

```javascript
// bad
var foo = 1;
var bar = 2;

// good
var foo = 1,
  bar = 2;
```
## Class
* Define private variables and private functions on top, add an empty line after private properties.

```javascript
// bad
(function () {
  var obj = {};
  obj.foo = function () {
    bar();
  };
  i = 0;
  bar = function () {
    i += 1;
  };
  return obj;
}());

// good
(function () {
  var obj = {},
    i = 0,
    bar = function () {
      i += 1;
    };

  obj.foo = function () {
    bar();
  };
  return obj;
}());
```

## Chaining
* Chain function calls on new lines

```javascript
//bad
animate().now()
  .then();

//good
animate()
  .now()
  .then();
```

## Naming Conventions
* file names in smaller case with _ seperator
* Variables in smaller case with words separated by _

```javascript
//bad
var variableNotLikeThis;
var Variable_Not_Like_This;

//good
var variables_like_this;
```

* functions should be in lower camelcase

```javascript
//bad
function IDoSomething() {
}

function i_do_something() {
}


//good
function iDoSomething() {
}
```

* Pseudo Classes should be in upper camelcase

```javascript
//bad
var a = new this_is_an_object();
var b = new This_Is_An_Object();

//good
var a = new ThisIsAnObject();
```

## Spacing and Empty lines
* Give necessary empty lines to make code more readable

```javascript
//bad
/* global ButtonView */
'use strict';
var a = require('foo'),
    b = 1;
    c = function () {
        return 2;
    },
    d = function () {
        return 3
    };
a.operation();
return b;

//good
/* global ButtonView */

'use strict';

var a = require('foo'),
    b = 1,

    c = function () {
        return 2;
    },

    d = function () {
        return 3
    };

a.operation();

return b;
```

* break line on var chain if there will be a value assigned to it.
```javascript
//bad
var a = foo(), b = bar(), c = 1, d, e;

//good
var a = foo(),
    b = bar(),
    c = 1,
    d, e;
```
