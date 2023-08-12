# Cheatsheet of Handbook

[link](https://www.typescriptlang.org/docs/handbook/intro.html)

based on `use case`

1. What is TypeScript?
1. How does TypeScript automatically infer types?
1. How do we use TypeScript in Functions?
1. Classes
1. Modules

Table of Content

1. The Basics
1. Everyday Types
1. Narrowing
1. More on Functions
1. object Types
1. Type Manipulation
1. Classes
1. Modules

## 1. The Basics

## 2. Everyday Types

### Why we call TypeScript is *structurally typed* type system?

The below example works just as if we had used an anonymous object type. Note that TypeScript only cares that it has the expected properties. 

```ts
interface Point {
    x: number;
    y: number;
}

function printCoord(pt: Point) {
    console.log("The coordinate's x value is " + pt.x);
    console.log("The coordinate's y value is " + pt.y);
}

printCoord({ x: 100, y: 100 });
```

### How does TypeScript automatically infer types?

- Variables:

```ts
// 'myName' is inferred as type 'string' since it might be changed
let myName = "Alice";

// 'animalName' is inferred as type 'Cheshire' since it is never changed
const animalName = "Cheshire"; 

// 'x' is inferred as type 'string' | 'number'
let x = math.random() < 0.5 ? 10 : "hello";

```

- Functions:

```ts
// The return type is inferred as 'number'
function getFavoriteNumber() {
    return 26; // Return Type is inferred based on this statement
}
```

- Anonymous Functions:

```ts
const names = ["Alice", "Bob", "Eve"];

// Contextual typing for function - parameter `s` is inferred as type 'string'
names.forEach(function (s) {
    console.log(s.toUpperCase());
})

// Contextual typing also applies to arrow functions
names.forEach((s) => {
    console.log(s.toUpperCase());
})

```

- Objects: When you initialize a variable with an object, TypeScript assumes that the properties of that object might change values later.

```ts
// The type of the property `counter` is inferred as 'number'
const obj = { counter: 0 } 
```

This behavior leads to this type error: 

```ts

declare function handleRequest(url: string, method: "GET" | "POST") : void;

const req = { url: "https://exmaple.com", method: "GET" };

// Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.
handleRequest(req.url, req.method);

```


