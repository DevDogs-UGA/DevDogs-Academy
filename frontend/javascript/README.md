Outline/TOC/TODO
- [ ] Intro
- [ ] Overview
    - [ ] Primitives and common operations
    - [ ] Variables
    - [ ] Arrays
    - [ ] Conditionals
        - [ ] Truthiness
    - [ ] Loops
    - [ ] Dictionaries/maps
    - [ ] Classes/objects
- [ ] Functions
    - [ ] Normal functions
    - [ ] Lambdas
    - [ ] Async/promises
- [ ] Interacting with the DOM
    - [ ] Selecting elements
    - [ ] Binding to events
- [ ] React
    - [ ] What is React?
    - [ ] Components
    - [ ] Passing state (props)
    - [ ] Sharing state (lifting)
- [ ] More resources

# JavaScript in a Nutshell
JavaScript (JS for short) is a dynamically typed, interpreted, multiparadigm language. It also happens to be the *lingua franca* of the web. All the major browsers can run it to make the webpages they display interactive, and you can even use [some tooling](https://en.wikipedia.org/wiki/Node.js) to run it on a server for backend services. We'll be using JS extensively in this club to create our frontends, so it'll serve you well to get familiar with it. This article is meant to help you hit the ground running. If you're here to review something specific, or you already feel good with your JavaScript abilities, please feel free to aggressively utilize the table of contents in the top right corner to skip to the juicy bits. Let's get in to it!

## Language overview
JavaScript's syntax is generally C-flavored, so if you have experience in languages like C, C++, C#, or Java, you'll feel right at home. That being said, there are some differences that you should be aware of.
### Comments
Comments are sections of your source code that the interpreter won't run. They're typically used for documentation and other things that are intended for developers to read, not the computer. Single line comments start with two slashes (`//`) and run until the end of a line. Multiline comments start with a slash and asterisk (`/*`) and run until the next asterish and star (`*/`).
```js
"something here will be run" // but this wont!
/*
multiline comments are nice because they let you
break
things
up
*/
```
### Primitives and common operations
JavaScript's most basic units of information are categorized into a few primitives[^0]: `boolean`, `number`, `string`, `undefined`, and `null`.

Booleans are values of `true` or `false`. They're used in conditional statements, which we'll cover later.
```js
// true!!!
true
// false...
false
// logical or, yields true
true || false
// logical or, yields false
true && false
// logical not, yields false
!true
```

Numbers are stored as double-precision floating point numbers (think `double` in your aforementioned C-style language of choice). They look like:
```js
// 1
1
// 2
2.
// 3
3.0
// 4 (scientific notation)
400e-2
// 5 (hexadecimal)
0x5
// 6 (binary)
0b110
// you can separate digits with an underscore (_) for readability
// this yields 1000000 (one million)
1_000_000
// addition, yields 3
1 + 2
// subtraction, yields -1
1 - 2
// multiplication, yields 2
1 * 2
// division, yields 0.5
1 / 2
// modulo, yields 1
1 % 2
```
Please keep in the back of your mind that these are floats, and come with all the usual float weirdness (imprecision, nonassociativity, signed zeroes, infinities, NaNs). You should almost never have to worry about these things, but it's good to know that they exist just in case you ever do.

Strings look like this:
```js
// double quotes
"this is a string"
// single quote
'this is also a string'
// backticks (that thing to the left of your 1 key)
`this is also also a string`
// you can use a backslash (\) to escape newlines for multi-line strings
"this string spans \
multiple lines!"
// you can also use the usual escape sequences
"newline:\n, tab:\t, carriage return: \r, null: \0"
// strings are character arrays. you can access individual characters with a subscript.
// this yields the character '3'. we'll talk more about arrays later!
"012345"[3]
// + appends strings together, yields "strings are nice"
"strings " + "are nice"
// other types are eagerly converted into strings when appended
// this yields "this should say false: false"
"this should say false: " + (false || (false && true))
// backtick strings allow you to inject any js expression into a string with `${expr}`
`this should say false: ${false || (false && true)}`
```

Undefined and null values are kind of special. Undefined is used to indicate that something hasn't been given an explicit value. You'll see undefined values if you try to do something like use a variable that hasn't been assigned to. Null values, on the other hand, are used to indicate an intentional value of 'nothing'. Most of the time, you shouldn't go out of your way to use undefined. It's primarily used by the interpreter to signal errors. Null is useful, though.
<!-- TODO maybe cover operations with null and undefined? idk might be too niche for an article like this -->
```js
undefined
null
```

[^0]: Okay, technically there's also [`bigint`](https://developer.mozilla.org/en-US/docs/Glossary/BigInt) and [`symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol), but most readers probably don't need to worry about those.

## Variables
<!-- TODO dynamic typing -->
<!-- NOTE should we also mention variables with var or no keyword? probably shouldn't be used by new learners -->
You may from time to time want to store values for later use. You can do this using variables.
```js
// declares a new variable `variable0` with initial value `undefined`
let variable0;
// variables can be reassigned
variable0 = "hi";
// js is dynamically typed, so variables can also be reassigned to values with different types
variable0 = 0;
// const variables must be initialized at declaration and cannot be reassigned after declaration
// const variable1; is not allowed!
const variable1 = 1;
// variable1 = 2; is not allowed!
```

## Arrays
Arrays allow you to bundle multiple values into one data structure.
```js
// elements don't have to be the same type
["value zero", "value one", 2, false]
```

## More resources
- https://learnxinyminutes.com/docs/javascript/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://react.dev/learn

## Meta
This article's content is available under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license. It's also one out of a number of other tutorials/quickstarts that you may also find useful, which you can find [here](https://github.com/DevDogs-UGA/DevDogs-Academy).
