# A Javascript Subset for jQuery Users

*Murach's Jquery, 2nd Edition*
*Zak Ruvalcaba and Anne Boehm*
page 49

***

## The Basics of Javascript

An *external Javascript file* is referenced inside an HTML document, but lives seperately

*Embedded Javascript* is coded in an HTML document.

Javascript files or embedded code run in the order that they appear

Some put Javascript references at the end of the body tag in order to ensure that the document loads before the Javascript, but it may not be the best choice for every situation

Javascript is case-sensitive

Every Javascript statement ends with a semicolon

Javascript ignores extra whitespace between statements

Single line comments - `//`

Multi-line comments - `/* */`

Identifiers (variables, etc.)
    * can only contain letters, numbers, the underscore, and the dollar sign
    * can't start with a number
    * are case-sensitive
    * cannot be the same as *reserved words*

Camel Casing - `camelCaseUpperCase`

Three primitive data types - number, string, and boolean

In Javascript, decimal point numbers are stored as *floating-point* numbers

Order of Operations - Paren, Increment/Decrement, Mult/Div/Mod, Add/Sub

create a variable with the `var` keyword

The `+` operator will concatenate strings in addition to addition

`NaN` is a value indicating "Not a Number"

*Method chaining* is the use of multiple method calls into one statement

`var varName = new *ObjectType*();` - syntax for creating new objects

`isNaN(*expression*)` - returns 'true' if *expression* is not a number

`var arrayName = new Array(*length*);` or `var arrayName = [];`

`arrayName[arrayName.length] = *something*` will add an item to the end of an array

`var varName = function(*parameters*) {...;}` - to declare a *function expression*

`function functionName(*parameters*) {...return *x*;}` - *function declaration*

Declaring a variable without the preceding `var` leads to the Javascript engine creating that variable as global

`use strict;` is declared at the beginning of a Javascript document and solves the preceding issue

`objectVariable.onEventName = eventHandlerName;`

***

### END CHAPTER
Robert Juall
__OCT2016