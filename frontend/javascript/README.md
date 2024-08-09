Outline/TOC/TODO
- [x] Intro
- [ ] Overview
    - [x] Comments
    - [x] Semicolons
    - [x] Primitives and common operations
    - [x] Variables
    - [x] Comparisons
        - [x] `==` vs `===`
        - [x] Truthiness
    - [ ] Conditionals
        - [ ] Short circuiting with `&&`
        - [ ] Ternary
    - [ ] Arrays
    - [ ] Loops
    - [ ] Maps
    - [ ] Classes and objects
- [ ] Functions
    - [ ] Normal functions
    - [ ] Lambdas
    - [ ] Promises and async
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
JavaScript (JS for short) is a dynamically typed, interpreted, multiparadigm language. It also happens to be the *lingua franca* of the web. All the major browsers can run it to make the webpages they display interactive, and you can even use [some tooling](https://en.wikipedia.org/wiki/Node.js) to run it on servers for backend services. We'll be using JS extensively in this club to create our frontends, so it'll serve you well to get familiar with it.

This article is meant to help you hit the ground running. If you're here to review something specific, or you already feel good with your JavaScript abilities, please feel free to aggressively utilize the table of contents (located in the top right corner) to skip to the parts you care about.

Finally, if you feel like messing around with the examples given in this article, you can open up a live JavaScript interpreter on [a blank page](about:blank) in your browser to see how things play out. On Firefox, this can be done with Ctrl+Shift+K (Cmd+Opt+K for macOS). For Chrome, hit Ctrl+Shift+J (Cmd+Opt+J for macOS). Type things in at the bottom of the panel that pops up to run your JS code.

That's it for introductions. Let's get in to it!

## Language overview
JavaScript's syntax is generally C-flavored, so if you have experience in languages like C, C++, C#, or Java, you'll feel right at home. That being said, there are some important differences that you should be aware of before you start writing code.

### Comments
Comments are sections of your source code that the interpreter won't run. They're typically used for documentation and other things that are intended for developers to read, not the computer. Single line comments start with two slashes (`//`) and run until the end of a line. Multiline comments start with a slash and asterisk (`/*`) and run until the next asterish and star (`*/`).
```js
"something here will be run" // but this won't!
/*
multiline comments are nice because they let you
break
things
up
*/
```

### Semicolons
<!-- NOTE instructing to always include semicolons since doing so eliminates some errors and it's probably what readers coming from java are used to anyways -->
Like most other C-family languages, JavaScript terminates statements with a semicolon (`;`). Sometimes, you're able to omit these semicolons in your source code and let the interpreter guess about where to put them. The catch is that the interpreter sometimes won't have enough context to guess correctly, leaving you with some really confusing errors. In this club, we've decided that it's in our best interest to explicitly include semicolons 100% of the time. Please do your best to follow this standard!
```js
// semicolon included
// ------------v
"this is valid";
// semicolon omitted
// -----------------------------------v
"this is also valid (but discouraged)"
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
// logical and, yields false
true && false
// logical not, yields false
!true
```

Numbers are stored as double-precision floating point numbers (think `double` in your C-style language of choice). They look like:
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
// exponiation (think a^b), yields 1
1 ** 2
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
// you can use a backslash (\) to break long strings into multiple lines
// this yields "this string spans multiple lines!" (no new line)
"this string spans \
multiple lines!"
// you can also use the usual escape sequences
"newline: \n, tab: \t, carriage return: \r, null: \0"
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
<!-- TODO maybe cover operations with null and undefined? might not be necessary. -->
```js
undefined
null
```

[^0]: Okay, technically there's also [`bigint`](https://developer.mozilla.org/en-US/docs/Glossary/BigInt) and [`symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol), but most readers probably don't need to worry about those.

### Variables
<!-- NOTE omitting var and no-keyword declarations on the logic that they're mostly legacy features -->
<!-- TODO maybe touch on variable shadowing? -->
You may from time to time want to store values for later use. You can do this using variables.
```js
// declares a new variable `variable0` with initial value `undefined`
let variable0;
// variables can be reassigned
variable0 = "hi";
// js is dynamically typed, so variables can also be reassigned to values with different types
variable0 = 0;
// const variables must be initialized at declaration and cannot be reassigned after declaration
// const variable1; <- not allowed!
const variable1 = 1;
// variable1 = 2; <- not allowed!
```

Sometimes you'll want to do an operation on a variable's value and then store the result back into the variable. JavaScript has a shorthand for this:
```js
let myVariable = 100;
// instead of writing something like this
myVariable = myVariable + 1;
// you can instead write this
myVariable += 1;
```
You use this operation-then-assign syntax with any of the operations mentioned in the previous section.
<!-- NOTE omitting increment (++) and decrement (--) since imo they're often a code smell and explaining their subtleties would take up space disproportionate to their importance -->

### Comparisons
<!-- TODO should we talk about null coalescing and optional chaining? -->
Comparisons let you check whether data structures satisfy some sort of condition.

```js
// double-equals (==) compares values. this yields true:
0 == 0
// but beware! the interpreter will try and convert types to allow for comparison.
// this can lead to unexpected behavior like this (comparing string and number),
// which yields true
"0" == 0

// if you want to do an equals comparison while respecting type differences,
// you'd use a triple-equals (===) comparison.
0 === 0 // true
"0" === 0 // false

// a similar distinction exists for the not-equals comparisons
// the following are equivalent, and yield false
!(0 == 0)
0 != "0"
// the following are equivalent, and yield true
!(0 === "0")
0 !== "0"

// finally, we have the ordering comparisons. these work as you would expect in any other
// language, with the caveat that types are always converted (like with ==)
0 > 0 // false
0 >= "0" // true
0 < "0" // false
0 <= 0 // true
```

JavaScript also has something called 'truthy' and 'falsy' values. Basically, all non-Boolean values will behave like `true` or `false` if you try to use them as if they were Boolean. The rule is pretty simple - all values behave like `true` except for the following, which behave like `false`:
- `0`
- `NaN` (a floating point not-a-number value)
- `""` (the empty string)
- `null`
- `undefined`
```js
// the following all yield `true`
0 === false
-0 === false
"" === false
1 === true
"true" === true
"false" === true
```

### Conditionals
TODO

### Arrays
Arrays let you bundle multiple values into one data structure.
<!-- TODO more array methods -->
```js
// array literals are delimited by square brackets ([])
[0, 1, 2, 3]
// elements don't have to be the same type
let arr = ["value zero", "value one", 2, false];
// elements are accessed using the subscript ([]) operator
// arrays are zero-indexed, meaning they start counting their elements at zero
// yields "value zero"
arr[0]:
// yields "value one"
arr[1];
// yields 2
arr[2];
// you can change the contents at an index by reassigning with =
// after this next line, arr will look like ["value zero", "value one", 2, 3]
arr[3] = 3;
// you can even store other arrays inside of an array!
let nested = [["array 0 element 0"], ["array 1 element 0"], ["array 2 element 0"]];
// you access these values using chained subscripts. the first subscript yields the element stored
// at that index (which is another array) and the second one subscripts into that yielded array
// yields "array 1 element 0"
nested[1][0];
// you can get an array's length using the `.length` property (more on properties in the classes
// section). this yields 4
arr.length;
```

### Loops
<!-- TODO maybe cover destructuring in for-of? -->
Loops let you compress repetitive code into blocks that... well, loop. They come in three primary varieties: `while`, `for`, and `for-of`.
<!-- TODO for-of loops -->
```js
// while loops continue so long as the condition in their parenthesis (()) yields true
let howMany = 0;
let message = "We looped ";
while (howMany < 5) {
    message += howMany + " ";
    howMany += 1;
}
message += "times";

// for loops let you declare and use a variable scoped to the loop, usually for iteration
message = "We looped ";
for (let howMuch = 0; howMuch < 5; howMuch += 1) {
    message += howMuch + " ";
}
message += "times";

// for loops are really just a while loop in a trench coat.
// the previous example could have instead been written as:
{
    let howMuch = 0;
    while (howMuch < 5) {
        message += howMuch + " ";
        howMuch += 1;
    }
    message += "times";
}

// for-of loops are analogous to for-each loops in other languages
message = "We've seen elements ";
let array = [0, 1, 2, 3, 4, 5];
// you can't change the value contained in whatever you're looping through
// with a for-of loop, so we usually use const-declared variables for clarity
for (const element of array) {
    message += element + " "
}
```

### Maps
TODO

### Classes and objects
TODO

## More resources
- https://learnxinyminutes.com/docs/javascript/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://react.dev/learn

## Meta
This article's content is available under the [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) license. It's also one out of a number of other tutorials/quickstarts that you may also find useful, [available here](https://github.com/DevDogs-UGA/DevDogs-Academy).
