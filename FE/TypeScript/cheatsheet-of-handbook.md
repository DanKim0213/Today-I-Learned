# Cheatsheet of Handbook

based on `use-case`

Table of Content

1. What is TypeScript?
1. How does TypeScript automatically infer types?
1. How do we use TypeScript in Functions?
1. Classes
1. Modules

OFF-TOPIC
1. Which one between `interfaces` and `types` should I use?
1. `unknown`

## What is TypeScript?

> TypeScript is JavaScript with syntax for types.

TypeScript’s type system aims to make it as easy as possible to write typical JavaScript code without bending over backwards to get type safety.

We know how useful typescript is. As the [homepage](https://www.typescriptlang.org/) says, "Catch errors early in your editor" is one of the reasons why we should use TypeScript. 

However, what does 'Type' mean practically? Let's see referring to TS Handbook:

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

The example works just as if we had used an anonymous object type. Note that TypeScript only cares that it has the expected properties. That's why TypeScript is *structurally typed* type system. 

## How does TypeScript automatically infer types?

When you don’t specify a type, and TypeScript can’t infer it from context, the compiler will typically default to `any`. With a value of type `any`, you can access any properties of it. 

> Tip💡: You usually want to avoid this, though, because `any` isn’t type-checked. Use the compiler flag `noImplicitAny` to flag any implicit `any` as an error.

```ts
let obj: any = { x: 0 };
// None of the following lines of code will throw compiler errors.
// Using `any` disables all further type checking, and it is assumed 
// you know the environment better than TypeScript.
obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;
```

It doesn't mean a value of type `any` is always attached to when you don't specify a type. In fact, `any` is attached to when TypeScript cannot automatically infer types. Let's see how TypeScript infers types:

- Variables: `let` represents changes while `const` represents consistency. 

```ts
// 🤖 let myName: string
let myName = "Alice";

// 🤖 const animalName: "Cheshire"
const animalName = "Cheshire"; 

// 🤖 let x: string | number
let x = math.random() < 0.5 ? 10 : "hello";

```

- Functions: Though `parameter` type must be specified, `return` type can automatically be inferred. 

```ts
// The return type is inferred as 'number'
function getFavoriteNumber(s: string) {
    return 26; // Return Type is inferred based on this statement
}
```

- Anonymous Functions: TypeScript uses *Contextual typing* to infer types of *Anonymouse Functions*. 

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
// 🤖 const obj: { counter: number; }
const obj = { counter: 0 } 

// 🤖 const names: string[]
const names = ["Alice", "Bob", "Eve"];
```

## How do we use TypeScript in Functions?

1. Basic
1. Overload
1. Union
1. Narrowing
1. Generic

### 1. Basic 

> In addition to `any`, there is `Function` type. Even though `Function` is available as a global type, it is generally best avoided because of the unsafe `any` return type. 

Functions accept either variables or callback functions as arguments. If you don't specify parameters of functions, it is declared as `any`. 


Let's see general functions:

```ts
// 🤖 function greet(s: string): string
function greet(s: string) {
    return s
}

// 🤖 function doSomething(cbfn: () => void): void
function doSomething(cbfn: () => void) {
    return cbfn(1, 2, 3)
}
```

> Rule: When writing a function type for a callback, never write an optional parameter unless you intend to call the function without passing that argument

[TBD]

### 2. Function Overloads 

In TypeScript, we can specify a function that can be called in different ways by writing overload signatures.

The signature of the implementation is not visible from the outside. When writing an overloaded function, you should always have two or more signatures above the implementation of the function:

```ts
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
  if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
  } else {
    return new Date(mOrTimestamp);
  }
}

// 🤖 function makeDate(timestamp: number): Date (+1 overload)
const d1 = makeDate(12345678);
// 🤖 function makeDate(m: number, d: number, y: number): Date (+1 overload)
const d2 = makeDate(5, 5, 5);

// ⚠️ No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.
const d3 = makeDate(1, 3);
```

However, TypeScript can only resolve a function call to a single overload:

```ts
function len(s: string): number;
function len(arr: any[]): number;
function len(x: any) {
  return x.length;
}

len(""); // OK
len([0]); // OK
len(Math.random() > 0.5 ? "hello" : [0]); // ⚠️ No overload matches this call.
```

Because both overloads have the same argument count and same return type, we can instead write a non-overloaded version of the function with *parameters with union types*:

```ts
function len(x: any[] | string) {
  return x.length;
}
```

Callers can invoke this with either sort of value, and as an added bonus, we don’t have to figure out a correct implementation signature.


### 3. Union

> Always prefer parameters with union types instead of overloads when possible

A union type is a type formed from two or more other types, representing values that may be *any* one of those types. We refer to each of these types as the union’s *members*:

```ts
function printId(id: number | string) {
    console.log("Your ID is: " + id);
}

// Optional Parameters
// `last?` represents last: string | undefined
function printName(first: string, last?: string) {
    // ...
}
```

We can make functions that only accepts a certain set of known values. By *combining literal types*:

```ts
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}

printText("Hello, world", "left"); // OK
printText("G'day, mate", "centre"); // ⚠️ Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.
```

However, you might be cautious when using properties of an object as arguments:  

```ts

declare function handleRequest(url: string, method: "GET" | "POST") : void;

// 🤖 const req: { url: string; method: string; }
const req = { url: "https://exmaple.com", method: "GET" };

// ⚠️ Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.
handleRequest(req.url, req.method);
```
As you see above, TypeScript assumes that the properties of that object might change values later. There are three workarounds:

1. convert the entire object to be type literals.
1. add a type assertion.
1. declare a type alias. 

```ts
// 1. type literals
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);

// 2. type assertions
const req = { url: "https://example.com", method: "GET" as "GET" };
handleRequest(req.url, req.method);

// 3. type alias
type Req = {
    url: string;
    method: "GET" | "POST";
}

const req: Req = { url: "https://examplem.com", method: "GET" };
handleRequest(req.url, req.method);
```

### 4. Narrowing

TypeScript looks at special checks (called *type guards*) and assignments, and the process of refining types to more specific types than declared is called *narrowing*.

When working with Union Types, TypeScript will only allow an operation if it is valid for *every* member of the union:  

```ts
// Return type is inferred as number[] | string
funtion getFirstThree(x: number[] | string) {
    return x.slice(0, 3)
}
```

However, if it is not valid, we need to *narrow* the union. *Narrowing* occures within our `if` check:

- typeof (for primitives)

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    // (parameter) padding: number
    return " ".repeat(padding) + input;
  }
  // (parameter) padding: string
  return padding + input;
}
```
- instanceof (for classes)

```ts

```
- "property" in object (for objects)

```ts
```
- type-guard functions (for anything)

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

- When to use custom type guards?
- Discriminated union + `never`

### 5. Generic

- How generic works
- You should not use Generic if ...

## References

- [Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [Private class features](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)
- [Interface vs Types](https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c)
