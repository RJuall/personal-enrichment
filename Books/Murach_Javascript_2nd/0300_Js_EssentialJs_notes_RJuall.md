# Getting Started with Javascript

*Murach's Javascript, 2nd Edition*
*Mary Delamater*
page 83

***

## How to Code Basic Control Statements

*Like all programming languages, Javascript provides control statements that let one control how information is processed in an application.*

`isNaN("String") == false`

`isNaN(12.345) == true`

`!isNaN("String") == true`

`x && y == x AND y`

`x || y == x OR y`

`!x == NOT x`

```javascript
if (*condition*) {
    *statement*;
} else if (*condition*) {
    *statement*;
} else {
    *statement*;
}
```

`if (bool == true) == if (bool)`

```javascript
while (*condition*) {
    *statement*;
    *etc*;
}

do {
    *statement*;
    *etc*;
} while (*condition*);
```

```javascript
for (*counter*; *condition*; *increment*) {
    *statement*;
    *etc*;
}

for (var i = 0; i < 10; i++) {
    accumulator += i;
}
```

## How to Work with Arrays

*An array is an object that contains one or more items called elements, which can be primitive data types or objects. The length of an array indicates the number of elements that it contains*

`var arrayName = new Array(*length*);`

`var arrayName = [];`

`arrayName.length`

```javascript
var arrayName = [];
arrayName[0] = 1;
arrayName[1] = 2;
arrayName[2] = 3;
arrayName.length == 3;
arrayName[arrayName.length] = 4;
```

***

### END CHAPTER
Robert Juall
10OCT2016