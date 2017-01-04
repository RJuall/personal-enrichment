# Getting Started with Javascript

*Murach's Javascript, 2nd Edition*
*Mary Delamater*
page 51

***

## How to Include Javascript in an HTML Document

*There are three different ways to include javascript into an HTML document*

The first way is by writing an external .js file & including a reference to it in the HTML.

```javascript
<script src="somewhere/some.js"><//script>
```

Javascript can also be coded into the head element directly, instead of a reference to an external file containing javascript - known as *embedded javascript*

References or embedded javascript can also be placed in the body element of an HTML document.

Placing javascript at the end of the HTML document can be helpful in making the web page load faster, but it may not work depending on the page's needs.

The `<noscript></noscript>` element will load if a browser does not have javascript enabled.

```javascript
<p>
  <script>
    var today = new Date();
    document.write("Current date: ");
    document.write(today.toDateString());
  <//script>
<//p>
<p>&copy;&nbsp;
  <script>
    var today = new Date();
    document.write( today.getFullYear() );
  <//script>
  <noscript>2015<//noscript>
, San Joaquin Valley Town Hall
<//p>
```

```javascript
<h2><noscript>To get the most from this web site, please enable Javascript<//noscript><//h2>
```

## The Javascript Syntax

*The syntax of Javascript refers to the rules that must be followed as one codes statements in Javascript*

**The basic Javascript rules:**
 * Javascript is case-sensitive
 * Each Javascript statement ends with a semicolon
 * Javascript ignores extra whitespace within statements

Whitespace refers to spaces, tabs, and return characters.

In some cases, Javascript will try to correct what it thinks is a missing semicolon by adding a semicolon at the end of a split line. To avoid this:
  * Split a statment after an arithmetic or relational operator, an opening brace/bracket/parenthesis
  * Do not split a statement after an identifier, a value, the *return* keyword, or closing bracket or parenthesis

An *identifier* is the name given by a programmer to variables, functions, objects, properties, methods, and events

**Rules for creating identifiers:**
  * Identifiers can only contain letters, numbers, underscores, or dollar signs
  * Identifiers can not start with a number
  * Identifiers are case-sensitive
  * Identifiers can be any length
  * Identifiers can not be the same as *reserved words*
  * Avoid using global properties and methods as identifiers

Use meaningful names for identifiers and be consistent in the naming convention used

```javascript
/*
Multi-line comments
*/

//Single line comments
```

An *object* is a collection of methods and properties

A *method* performs a function or does an action

A *property* is a data item that relates to the object

The syntax for calling a method of an object: `objectName.methodName(parameters)`

The syntax for accessing a property of an object: `objectName.propertyName`

```javascript
//Using the alert method of the window object
window.alert("This is a test");
```

The `write` and `writeln` methods of the *document object* write their data into the body of the document so it's displayed in the browser window

HTML tags can be passed into these methods

Normally these statements would be coded within elements of the body

```javascript
<head>
  <title>Write Testing<//title>
  <script>
    var today = new Date();
    document.write("<h1>Welcome to our site!</h1>");
    document.write("Today is ");
    document.write(today.toDateString());
    document.write("<br>");
    document.writeln("Today is: ");
    document.writeln(today.toDateString());
    document.write("<br>")
  <//script>
<//head>
<body>
  <script>
    document.writeln("Welcome to our site!");
    document.writeln("Today is Monday.");
  <//script>
  <script>
    document.writeln("<pre>Welcome to our site!");
    document.writeln("Today is Monday.</pre>");
  <//script>
<//body>
```

The *document object* is the object that lets you work with the Document Object Model (DOM) that represents all of the HTML elements of the page.

The `writeln` method doesn't skip to the next line unless it is coded within a `<pre></pre>` element. However, you can code `<br>` tags within the output to provide for line spacing.

## How to work with Javascript data

*Data is frequently used by Javascript, especially when utilizing forms. There are three types of Javascript data*

Javascript provides for three *primitive data types*
  * The *number* data type for numerical data
  * The *string* data type for character data
  * The *boolean* data type for T/F values

**Examples of number values:**
  * 15
  * -21
  * 21.5
  * -124.82
  * -3.7e-9

Strings can be enclosed in either double or single quotes

Boolean values are represented by either `true` or `false`

In javascript, decimal values are stored as *floating-point numbers*

**Arithmetic Operators:**
  * `+`  - Addition
  * `-`  - Subtraction
  * `*`  - Multiplication
  * `/`  - Division
  * `%`  - Modulus
  * `++` - Increment
  * `--` - Decrement

Order of operations as usual (PEMDAS), except increment/decrement are always first

**Javascript Assignment Operators (MSDN)**
  * `=`     - Assignent Operator
  * `+=`    - Addition
  * `&=`    - Bitwise AND
  * `|=`    - Bitwise OR
  * `^=`    - Bitwise XOR
  * `/=`    - Division
  * `<<=`   - Left Shift
  * `%=`    - Modulus
  * `*=`    - Multiplication
  * `>>=`   - Right Shift
  * `-=`    - Subtraction
  * `>>>=`  - Unsigned Right Shift

Declare a variable in Javascript using `var` - `var variableName = value;`

Declaring multiple variables - `var varName1, varName2, varName3;`

The addition operator `+` adds numbers or concatenates strings/mixed types involving strings

Because of how javascript stores numbers, arithmetic operations are sometimes slightly imprecise

`\` is the escape character - i.e. `\n` == newline, `\'` == single quote, `\t` == tab, etc.

```javascript
var firstName = "Grace", lastName = "Hopper";
var fullName = lastName;
fullName += ", ";
fullName += firstName;
//fullName == "Hopper, Grace"
```

`parseInt` and `parseFloat` methods are used to convert strings to numbers, integers and floats, repectivey

If a string cannot be converted to a number by these methods `NaN` is returned (Not a Number)

***

### END CHAPTER
Robert Juall
09OCT2016