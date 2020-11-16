---
title: "Dart Notes"
date: 2020-06-16T17:18:51+02:00
draft: false

categories: []
tags: []
author: "Dee"
---
Everything in Dart are objects!

`import 'dart::io'`

`var` is like `auto` in cpp.
- `var v2 = v1` is not copying, but pointing
- `var v2 = [...v1]` is copying

use `dynamic` to make an object flexible.

`num` is `int` and `double`

- stdout.writeln('');
- stdin.readLineSync();
- print('some randome stuff + `$variable` ');  `$` can also use in `string`

`'''` or `"""` can be used to output multiline

type conversion:
- varaibletype.parse(variable);
    
    example:
 `var one = int.parse('1');`

- int.toString();
    
    example:
 `String one = 1.toString();`

- double.toStringAsFixed( int );
    
    example:
 `String pi = 3.1415926.toStringAsFixed(2);`

`const` does not need to use `var` or variable name specifically

operators: `?.` `??` `??=`
- `?.`: unclear some `var` has a property or not
- `??`: when the previous `?.` part is `null`, add value after `??` to make it the value temporarily
- `??=`: like `??` but actually assign the value to the object

Ternary operator
like `macro` 
    example: 
        `int x = 100`
        `var result = x % 2 == 0 ? 'even' : 'odd';`

positional parameter has to include `{}`
example: `dynamic sum(var one, {var two = 2}) => one + two;`
        or `dynamic sum(var one, {var two}) => one + (two ?? 3);`

optional parameter `[]`
example: `dynamic sum(var one, [var two = 2]) => one + two;`
        or `dynamic sum(var one, [var two]) => one + (two ?? 2);`

class 
`final`: you can only change the property at the initial once
`static`: apply for all objects in this class
`extend`: inherit a class
`super`： pass parameter
`@override`S
`get`: num get right => left + width;
`set`: set right(num value) => left = value - width; 

REFERENCE: https://www.youtube.com/watch?v=Ej_Pcr4uC2Q