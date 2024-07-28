Outline/TOC/TODO
- [ ] Intro
- [ ] Overview
    - [ ] Primatives and common operations
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
### Primatives and common operations
JavaScript's most basic units of information are categorized into a few primitives[^0]: `boolean`, `number`, `string`, `undefined`, and `null`.

Booleans are values of `true` or `false`. They're used in conditional statements, which we'll cover later.
```js
true  // true!!!
false // false...

```

Strings look like this:
```js
"this is a string"           // double quotes
'this is also a string'      // single quote
`this is also also a string` // backticks (that thing to the left of your 1 key)
"strings " + 
```

Numbers are stored as double-precision floating point numbers (think `double` in your aforementioned C-style language of choice). They look like:
```js
1      // 1
2.     // 2
3.0    // 3
400e-2 // 4 (scientific notation)
0x5    // 5 (hexadecimal)
0b110  // 6 (binary)
```
Please keep in the back of your mind that these are floats, and come with all the usual float weirdness (imprecision, nonassociativity, signed zeroes, infinities, NaNs). You should almost never have to worry about these things, but it's good to know that they exist just in case you ever do.

[^0]: Okay, technically there's also [`bigint`](https://developer.mozilla.org/en-US/docs/Glossary/BigInt) and [`symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol), but most readers probably don't need to worry about those.

## Variables
<!-- TODO let vs var, dynamic typing -->
You may, from time to time, actually want to store values for later use. You can do this using variables.
```js

```

## More resources
- https://learnxinyminutes.com/docs/javascript/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://react.dev/learn

## Meta
This article's content is available under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license. It's also one out of a number of other tutorials/quickstarts that you may also find useful, which you can find [here](https://github.com/DevDogs-UGA/DevDogs-Academy).
