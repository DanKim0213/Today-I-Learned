# What `this` refers to

TL;DR;

- `this` refers to the object that the object method is attached to.
- Arrow function expressions should only be used for non-method functions.
- When a function is passed as a callback, the value of this depends on how the callback is called.

According to [MDN - this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this), I figure out what `this` refers to, based on 3 criteria:

- Is `this` an object or an instance?
- Is `this` used in a regular function or an arrow function?
- Is the function used as a callback or an object method?

Note that when invoked as a standalone function (not attached to an object: func()), `this` typically refers to the global object (in non-strict mode) or undefined (in strict mode).

## `this` is an object or an instance

An object (a.k.a. object literal) is created by `{ property: value }` while an instance is created by constructors with `new` keyword. I'd like to give you a straightforward example:

```js
const obj = {
  name: "hello",
  fn: function () {
    console.log(this);
  },
  afn: () => console.log(this),
};
obj.fn(); // obj
obj.afn(); // undefined

// vs

class Hoi {
  name = "hoi";
  fn = function () {
    console.log(this);
  };
  afn = () => console.log(this);
}
const hoi = new Hoi();
hoi.fn(); // hoi
hoi.afn(); // hoi
```

`obj.fn` is attached to the object and it becomes an object method. On the other hand, `hoi.fn` becomes a Class method and it behaves like methods in object literals — the `this` value is the object that the method was accessed on.

However, you might be confused as you see `obj.afn()` returns `undefined` while `hoi.afn()` returns `hoi`. The reason why `obj.afn()` returns `undefined` is that [none of regular functions determine what `this` refers to](#arrow-functions-do-not-have-their-own-this-binding) whereas what `this` refers to in `hoi.afn` is determined by the instance of `Hoi`.

## `this` in regular functions refers to the object that the method is attached to

The reason why `this` refers to the object that the method is attached to is **reusability**, which means, for a regular function (not an arrow function, bound function, etc.), the value of `this` depends on how a function is invoked (**runtime binding**), not how it is defined.

Note that _the object that the method is attached to_ determines what `this` refers to:

```js
const parent4 = {
  name: "parent4",
  fn: function () {
    console.log(this); // **parent4** since `this` belongs to parent4

    // A
    anotherfn(); // **undefined** since `this` in anotherfn belongs to nothing

    // B
    const obj = {
      name: "p4 - obj",
      fn: anotherfn,
    };
    obj.fn(); // **obj** since `this` in anotherfn belongs to obj

    function anotherfn() {
      console.log(this); // `this` belongs to nothing
    }
  },
};

parent4.fn();
```

## Arrow functions do not have their own `this` binding

Once again, _regular functions determine what `this` refers to._ If you put together a regular function for determinining what `this` refers to and an arrow function for brevity, you can write much simple and intuitive codes:

```js
// from
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],
  // showList: function () {
  //   this.students.forEach(function (student) {
  //     alert(this.title + ": " + student);
  //   }, this);
  // },
  showList: function () {
    this.students.forEach(
      function (student) {
        alert(this.title + ": " + student);
      }.bind(this) // you must bind `this` to the callback function for `this.title`
    );
  },
};

group.showList();

// to
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],
  showList: function () {
    // arrow functions do not have this. If this is accessed, it is taken from the outside.
    this.students.forEach((student) => alert(this.title + ": " + student));
  },
};

group.showList();
```

The reason why [arrow functions do not have their own `this` binding](https://javascript.info/arrow-functions#arrow-functions-have-no-this) is that Arrow function expressions should only [be used for **non-method functions**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#cannot_be_used_as_methods).

Instead of binding, they inherit `this` from the parent scope **at the time they are defined**, which means their `this` value cannot be set by bind(), apply() or call() methods, nor does it point to the current object in object methods:

```js
const globalObject = this;
const foo = () => this;
console.log(foo() === globalObject); // true

const obj = { name: "obj" };

// Attempt to set this using call
console.log(foo.call(obj) === globalObject); // true

// Attempt to set this using bind
const boundFoo = foo.bind(obj);
console.log(boundFoo() === globalObject); // true
```

## The value of `this` depends on how the callback is called

Callbacks are typically called with a `this` value of `undefined` (calling it directly without attaching it to any object):

```js
const parent2 = {
  name: "parent2",
  regularFn: function () {
    console.log(this);
  },
  fn: function (cb) {
    // cb(); // undefined

    // option1
    // this.cfn = cb;
    // this.cfn();

    // option2
    cb.call(this);
  },
  afn: (cb) => cb(),
};

const parent3 = {
  name: "parent3",
  cb: function () {
    console.log(this);
  },
};

parent3.cb(); // parent3
parent2.fn(parent3.cb); // parent2
parent2.afn(parent3.cb); // undefined
```

Some APIs, however, such as [this in DOM event handlers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this#this_in_dom_event_handlers) do not follow the convention (calling it with attaching it to an object):

```js
// When called as a listener, turns the related element blue
function bluify(e) {
  // Always true
  console.log(this === e.currentTarget);
  // true when currentTarget and target are the same object
  console.log(this === e.target);
  this.style.backgroundColor = "#A5D9F3";
}

// Get a list of every element in the document
const elements = document.getElementsByTagName("*");

// Add bluify as a click listener so when the
// element is clicked on, it turns blue
for (const element of elements) {
  element.addEventListener("click", bluify, false);
}
```

And, some APIs allow you to set a `this` value for invocations of the callback:

```js
[1, 2, 3].forEach(logThis, { name: "obj" });
// { name: 'obj' }, { name: 'obj' }, { name: 'obj' }
```

## Rule of Thumb

- Use `regular function expressions` at first instead of `arrow function expressions` because typically you want `this` to refer to its object rather than `undefined`. (In addition, whether or not to use it as an object method, it looks consistent)
- Use `arrow function` as a callback function because typically you want `this` to refer to its outer scope.
- Use `class` instead of `function` to create an instance because it clears up the ambiguity.

## Summary

Guess the output 😉:

```js
const obj = {
  name: "hello",
  fn: function () {
    console.log(this);
    [1, 2].forEach((el) => console.log("fn cb: ", this));
  },
  afn: () => {
    console.log(this);
    [1, 2].forEach((el) => console.log("afn cb: ", this));
  },
};
obj.fn();
obj.afn();

class ParentClass {
  name = "hoi";
  fn = function () {
    console.log("fn: ", this);
    [1, 2].forEach((el) => console.log("fn cb: ", this));
  };
  afn = () => {
    console.log("afn: ", this);
    [1, 2].forEach((el) => console.log("afn cb: ", this));
  };
}

const newParent = new ParentClass();
newParent.fn();
newParent.afn();

/**
 *  output:
 *  fn:  ParentClass { name: 'hoi', fn: [Function: fn], afn: [Function: afn] }
 *  fn cb:  ParentClass { name: 'hoi', fn: [Function: fn], afn: [Function: afn] }
 *  fn cb:  ParentClass { name: 'hoi', fn: [Function: fn], afn: [Function: afn] }
 * /
```

```js
"use strict";

const parent = {
  name: "parent1",
  echo: this.name,
  func: function () {
    console.log(this.name);
  },
  arrowFunc: () => console.log(this.name),
  child: {
    name: "child1",
    echo: this.name,
    func: function () {
      console.log(this.name);
    },
    arrowFunc: () => console.log(this.name),
    cbFunc: function () {
      [1].forEach((el) => console.log("cb: ", this.name));
    },
  },
};

parent.func();
parent.arrowFunc();
parent.child.func();
parent.child.arrowFunc();
parent.child.cbFunc();
```
