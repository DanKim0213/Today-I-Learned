# Handbook

[link](https://www.typescriptlang.org/docs/handbook/intro.html)

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
// 'myName' is inferred as type 'string'
let myName = "Alice";

// 'animalName' is inferred as type 'Cheshire' 
const animalName = "Cheshire"; 

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

There are three workarounds:

1. convert the entire object to be type literals. (recommended)
1. add a type assertion.
1. declare a type alias and use it on both. 

```ts
// 1. type literals
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);

// 2. type assertions
const req = { url: "https://example.com", method: "GET" as "GET" };
handleRequest(req.url, req.method)

// 3. type alias
type Request = {
    url: string;
    method: "GET" | "POST";
}

declare function handleRequest(req: Request): void;
const req: Request = { url: "https://examplem.com", method: "GET" }
handleRequest(req)
```


## 3. Narrowing

When working with Union Types, TypeScript will only allow an operation if it is valid for *every* member of the union.  

```ts
// Return type is inferred as number[] | string
funtion getFirstThree(x: number[] | string) {
    return x.slice(0, 3)
}
```

However, if it is not valid, we need to *narrow* the union.

```ts
// Note that if `x` wasn't a string[], then it must have been a string
function welcomePeople(x: string[] | string) {
    if (Array.isArray(x)) {
        // Here: 'x' is 'string[]'
    } else {
        // Here: 'x' is 'string'
    }
}

```
