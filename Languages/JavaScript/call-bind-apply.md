# Call vs Bind vs Apply in JavaScript

These methods are generally used to extend methods **of objects**. Thus, they need `thisArg` for a first argument.

If you need to use a method of an object once, go for `call()` or `bind()`. Or if you need to use it multiple times, create a function using `bind()` and then use it.

Note that, most modules installed by npm are independent so as to use by itself (for example, dependency passed by arguments)

## call() vs apply()

> The `call()` method of Function instances calls this function with a given `this` value and `arguments` provided **individually**.

> The `apply()` method of Function instances calls this function with a given `this` value, and `arguments` provided as **an array (or an array-like object)**.

Note: `call()` is almost identical to `apply()`, except that the function arguments are passed to `call()` individually as a list, while for `apply()` they are combined in one object, typically an array — for example, `func.call(this, "eat", "bananas")` vs. `func.apply(this, ["eat", "bananas"])`.

### Function.prototype.call():

```javascript
// Food extends Product
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = "food";
}

console.log(new Food("cheese", 5).name);
// Expected output: "cheese"
```

### Function.prototype.apply():

```javascript
const numbers = [5, 6, 2, 3, 7];

const max1 = Math.max.apply(null, numbers);
const max2 = Math.max(...numbers);
console.log(max1, max2); // The results are same :)
```

### What is `array-like object`?

(TODO: I couldn't find appropriate reference (e.g. MDN) for this subject. Please update it later.)

There are two objects considered as `array-like object`:

- [arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)
- [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)

According to [Stack overflow](https://stackoverflow.com/a/29707677):

> Array-like object is an Object which has a length property of a non-negative Integer, and usually some indexed properties.

```javascript
const arraylike1 = { length: 0 };
const arraylike2 = { 0: "foo", 5: "bar", length: 6 };

// convert objects to arrays using Array.prototype.slice()
const arr1 = Array.prototype.slice.call(arraylike1); // []
const arr2 = Array.prototype.slice.call(arraylike2); // [ 'foo', <4 empty items>, 'bar' ]

console.log(arr1, arr2);
console.log(Array.isArray(arr1), Array.isArray(arr2)); // true, true
```

## bind()

> The `bind()` method of Function instances creates a new function that, when called, calls this function with its `this` keyword set to the provided value, and a given sequence of arguments preceding any provided when the new function is called.

```javascript
const module = {
  x: 42,
  getX: function () {
    return this.x;
  },
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// Expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// Expected output: 42
```

You can generally see `const boundFn = fn.bind(thisArg, arg1, arg2)` as being equivalent to `const boundFn = (...restArgs) => fn.call(thisArg, arg1, arg2, ...restArgs)` for the effect when it's called (but not when boundFn is constructed).
