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
* Variables in smaller case with words separated by _

```javascript
//bad
var variableNotLikeThis;
var Variable_Not_Like_This;

//good
var variables_like_this;
```

* Objects should be in camecase
```javascript
//bad
var a = new this_is_an_object();
var b = new This_Is_An_Object();

//good
var a = new ThisIsAnObject();
```
