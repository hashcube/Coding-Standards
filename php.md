## Indenting
* Never mix tabs and spaces
* Use 2 spaces for indenting

## Functions
* Always try to initiate variables in the first line
* Always put a space between arguments of function
* Opening brace of function in new line
* Don't use class name as constructor

```php
//Bad
public function foo($a,$b) {
  function2();
    $a = 1;
    function3($a);
}

//Good
public function foo($a, $b)
{
  $a = 1;

  function2();
  function3($a);
}

//Bad
class Foo()
{
  //Constructor declaration
  function Foo()
  {
    //Do stuffs
  }
}

//Good
class Foo()
{
  //Constructor declaration
  function __construct()
  {
    //Do stuff
  }
}
```
##Statements
* Use spaces before and after operators
* Don't use if-else statements without curly braces

```php
//Bad
$a='Foo';

//Good
$a = 'Foo';

//if-else statement

//Bad
if($a > $b)
  //execute single line

//Good
if($a > $b)
{
  //execute single line or multiple
}
```
* Use only lower case for true, false, null
```php
//Bad
$a = TRUE;
$b = True;
$c = FALSE;
$d = False;
$e = NULL;
$f = Null;

//Good
$a = true;
$b = false;
$c = null;
```

##Naming Conventions

* function and class name should be lowercamel case
```php
//Bad
class ClassName()
{
  //Do stuffs
}

class class_name()
{
  //Do stuffs
}

//Good
class className()
{
  //Start Doing
}

//Bad
function IDoSomthing()
{
  //Do stuffs
}

function i_do_somethng()
{
  //Do stuffs
}

//Good
function iDoSomething()
{
  //Now start something good
}
```

* Variable names should be in lowercae seprated by _
```php
//Bad
$VariableNotLikeThis = 0;
$Variable_Not_Like_This = 0;

//Good
$variable_like_this = 0;
```
## Spacing and empty lines

* Give necessary empty lines to make code more readble

```php
<?php

//Bad
class Foo
{
  public function __construct()
  {
    $a = "bar";
  }

  private function printFoo()
  {
    $foo = "Foo";
    $foo = $this->updateFoo($foo);
  }

  private function updateFoo($foo)
  {
    $updated_foo = $foo . "bar";
    return $updated_foo;
  }
}

//Good
class Foo
{

  public function __construct()
  {
    $a = "bar";
  }

  private function printFoo()
  {
    //Variables
    $foo = "Foo";

    //function calls
    foo = $this->updateFoo($foo);
  }

  private function updateFoo($foo)
  {
    $updated_foo = $foo . "bar";

    return $updated_foo;
  }
}
