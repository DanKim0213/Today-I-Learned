# JavaScript

JavaScript concept hierarchy

## Hierarchy

<details>
<summary>Hoisting</summary>

- Variable hoisting
  - `var`
    - `var x = 3;`
    - `undefined` if you acess a variable before it's declared
- Function hoisting
  - `"use strict"` is recommended

</details>
<details>
<summary>Block statement</summary>

- `{ StatementList }`
- Block scope
  - declarations
    - let, const, and class
  - statements
    - if...else, for
- Block scoping rule
  - `var` or `function` declaration in non-strict mode
    - **do not** have block scope
  - `let`, `const`, `class`, or `function` declaration in strict mode
- [source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)

</details>
<details>
<summary>Values</summary>

- Primitive Values
  - booleans, numbers, strings, null, and undefined
- Objects
  - All other values are objects
  - Plain objects, Arrays, Regular expressions, etc.

</details>
<details>
<summary>Function</summary>

- Defining functions
  - Function declarations
  - Function expressions
- Closures**
  - Encapsulation
  - Closure scope chain
    - Local scope (Own scope)
    - Enclosing scope (can be block, function, or module scope)
    - Global scope
- Function parameters
  - Default parameters
  - Rest parameters
    - `function multiply(multiplier, ...args){ /** statement */ }`
- Arrow functions
- Predefiined functions
- [source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)

</details>
<details>
<summary>Promises</summary>

- A `promise` is an object representing the eventual completion or failure of an asynchronous operation.
- States**
  - pending
  - fulfilled
  - rejected
- Chaining
  - `Promise.then(res => {/** */});`
  - `Promise.catch(e => {/** */});`
- async/await declaration
- Promise concurrency
  - `Promise.all()`
  - `Promise.allSettled()`
  - `Promise.any()`
  - `Promise.race()`

</details>
<details>
<summary>Module</summary>
</details>
<details>
<summary>Class</summary>
</details>
<details>
<summary>Collections</summary>

- Indexed collections
  - Arrays
  - Typed arrays
- Keyed collections
  - Map
  - WeakMap
  - Set
  - WeakSet

</details>
<details>
<summary>Error handling</summary>

- try/catch/throw
  - `finally` block's returning value becomes the return value of the entire try…catch…finally production
- Error objects
  - throw new Error("The message");
    - `{ name: 'Error', message: 'The message' }`
- [source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#try...catch_statement)

</details>
<details>
<summary>Iterators and generators</summary>

- Iterators
  - `next()`
  - `value`
  - `done`
- Generators
  - `function*` syntact
  - `next()`
  - `yield`
- Iterables
  - `for...of`
  - `String`, `Array`, `TypedArray`, `Map`, and `Set`

</details>
<details>
<summary>Operators</summary>

- Assignment operators
  - Destructuring
    - `const [one, two, three] = ["one", "two", "three"];`
  - Evaluation
    - [discourage chaining assignments](https://github.com/airbnb/javascript/blob/master/README.md#variables--no-chain-assignment)
- Comparison operators
- Arithmetic operators
- Bitwise operators
- Logical operators
  - `const a1 = "cat" && "dog"; // t && t returns "dog"`
  - `const a2 = "cat" || "dog"; // t || t returns "cat"`
- BigInt operators
  - you **cannot mix** BigInts and numbers in calcuations
- String operators
  - `"my" + "string"`
- Conditional (ternary) operator
  - `const status = age >= 18 ? "adult" : "minor";`
- Unary operators
  - delete
    - `delete object.property;`
    - Deleting array elements is not recommended
      - The array length is not affected
      - Other elements are not re-indexed
      - Instead, Array.prototype.splice()
  - typeof
  - Relational operators
    - in
      - `0 in ["one", "two"]; // returns true`
      - `"PI" in Math; // returns true`
    - instanceof

</details>
<details>
<summary>Literal</summary>

- Literals represent **fixed values**
- Array literals
- Boolean literals
- Floating-point literals
- Numeric literals
- Object literals
- RegExp literals
- String literals
- [source](https://developer.mozilla.org/en-US/docs/Glossary/Literal)

</details>
<details>
<summary>Object</summary>

- `this`
- 1급 객체
  - 변수나 데이터 구조안에 할당 가능
  - 매개변수로 전달 가능
  - 변환 값 사용 가능
- 내장 객체 (built-in)
  - 런다임 환경에 존재
  - 표준 객체(standard)
- Object Literal
  - new 연산자와 Constructor Function 없이 객체 생성
  - 가장 대중적인 방식
  - JSON 문법의 기반
- Prototype
- [source](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics)

</details>
<details>
<summary>Execution Context Stack</summary>
</details>

## Questions

- null vs undefined
- statements vs declarations
  - [source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements#difference_between_statements_and_declarations)
- Block vs Closure
  - Block is a statement while closure is a concept.
- Generators vs Iterators

## Caveats

- ~~Block scope VS. Function scope~~
  - I'd rather ask 'const, let scope VS. Function scope'.
