# How to handle errors with Jest

## Agenda

1. The goal of this post
2. expect.assertions(number) rather than done()
3. .rejects rather than try-catch
4. .toThrow rather than toMatch or toEqual
5. Use-case 1: Handle Error in a function
6. Use-case 2: Handle Error in an asynchronous function
7. References

## 1. The goal of this post

The goal of this post is to give you an opinionated way of how to handle error with jest. Since a bunch of source, including the official guide, suggests various ways (but each way has its own rule to comply with 😡), it would mislead to testing.

## 2. expect.assertions(number) rather than done()

Both expect.assertions() and done() are used to test async functions. However, expect.assertions() is focused on to verify that a certain number of assertions are called during a test while done() is focused on to wait a certain assertion to be called. Therefore, expect.assertions() would fail if the number of expectations are not called while done() would fail because of timeout (mostly from not calling done() at the end). 

Let's compare between done() and expect.assertion(number) when doing async calls.

[API - expect.assertions(number)](https://jestjs.io/docs/expect#expectassertionsnumber)

Make sure to add expect.assertions to verify that a certain number of assertions are called. Otherwise a fulfilled promise would not fail the test.
```javascript
test('doAsync calls both callbacks', () => {
  expect.assertions(2);
  function callback1(data) {
    expect(data).toBeTruthy();
  }
  function callback2(data) {
    expect(data).toBeTruthy();
  }

  doAsync(callback1, callback2);
});
```

**VS.**

[Testing Asynchronous Code - callbacks](https://jestjs.io/docs/asynchronous#callbacks)

done() is necessary. Otherwise, the test will complete as soon as fetchData completes, before ever calling the callback.
```javascript
test('the data is peanut butter', done => {
  function callback(error, data) {
    if (error) {
      done(error);
      return;
    }
    try {
      expect(data).toBe('peanut butter');
      done();
    } catch (error) {
      done(error);
    }
  }

  fetchData(callback);
});
```

You could notice at a glance that done(error) is declared in the catch block in order to avoid timeout. On the one hand, you could easily notice errors and reduce your time to figure out what went wrong by doing so. On the other hand, you could easily forget that where you need to declare done() properly. 

The rule of thumbs here is to declare expect.assertions(number) at the beginning of your tests. It never causes a problem at all. 

## 3. .rejects rather than try-catch

[API - .rejects](https://jestjs.io/docs/expect#rejects)

Use .rejects to unwrap the reason of a rejected promise so any other matcher can be chained. If the promise is fulfilled the assertion fails.
```javascript
test('rejects to octopus', async () => {
  await expect(Promise.reject(new Error('octopus'))).rejects.toThrow('octopus');
});
```

**VS.**

[Stack Overflow](https://stackoverflow.com/a/51821147)

You must handle errors at the catch block. 
```javascript
it('calls the API and throws an error', async () => {
  expect.assertions(2);
  try {
    await login('email', 'password');
  } catch (error) {
    expect(error.name).toEqual('Unauthorized');
    expect(error.status).toEqual(401);
  }
});
```

You know the test is supposed to cause an error. The key point of .rejects() is that the assertion fails when the promise is fulfilled. 

[!CAUTION](https://jestjs.io/docs/asynchronous#asyncawait)
Be sure to return (or await) the promise - if you omit the return/await statement, your test will complete before the promise returned from fetchData resolves or rejects. 

[!tip](https://jestjs.io/docs/tutorial-async#rejects)
expect.assertions(number) while using .rejects is not required but recommended to verify that a certain number of assertions are called during a test.

## 4. .toThrow rather than toMatch or toEqual

You can provide an optional argument to test that a specific error is thrown such as regex, string, error object, and error class. However, toMatch and toEqual only do one thing each: to match a string and equal to an object. 

[API - .toThrow](https://jestjs.io/docs/expect#tothrowerror)

```javascript
test('throws on octopus', () => {
  expect(() => {
    drinkFlavor('octopus');
  }).toThrow();
});
```

[Stack Overflow](https://stackoverflow.com/a/46155381)

```javascript
test("Test description", () => {
  const t = () => {
    throw new TypeError("UNKNOWN ERROR");
  };
  expect(t).toThrow(TypeError);
  expect(t).toThrow("UNKNOWN ERROR");
});
```

[!tip](https://jestjs.io/docs/expect#tothrowerror)
You must wrap the code in a function, otherwise the error will not be caught and the assertion will fail.

!tip
You don't need to wrap a promise function. Just invoke it.
[Code Example](https://jestjs.io/docs/asynchronous#asyncawait)
```javascript
test('the fetch fails with an error', async () => {
  await expect(fetchData()).rejects.toMatch('error');
});
```

## 5. Use-case 1: Handle Error in a function

Let's integrate what we learned into a simple code snippet.
```javascript
test("Test description", () => {
  expect.assertions(2);
  const t = () => {
    throw new TypeError("UNKNOWN ERROR");
  };
  expect(t).toThrow(TypeError);
  expect(t).toThrow("UNKNOWN ERROR");
});
```

- I declared expect.assertions(number) even though the above test is not asynchronous. It doesn't matter since expect.assertions() never causes a problem at all.
- I used .toThrow() rather than .toMatch or .toEqual since it handles Error object and string alike. 

## 6. Use-case 2: Handle Error in an asynchronous function

```javascript
test('the fetch fails with an error', async () => {
  expect.assertions(1);
  await expect(fetchData()).rejects.toThrow('error');
});
```

- I declared expect.assertions(number) even though it is not required while using .rejects().
- I handled an error, by using .rejects, within a single block, not within a try-catch block. 
- I used .toThrow rather than .toMatch or .toEqual. 

## 7. References

- [Jest API - expect](https://jestjs.io/docs/expect)
- [Jest Guide - An Async Example](https://jestjs.io/docs/tutorial-async)
- [Jest Introduction - Testing Asynchronous Code](https://jestjs.io/docs/asynchronous)
- [How to test the type of a thrown exception in Jest](https://stackoverflow.com/questions/46042613/how-to-test-the-type-of-a-thrown-exception-in-jest)
- [Necessary to use expect.assertions() if you're awaiting any async function calls?](https://stackoverflow.com/questions/50816254/necessary-to-use-expect-assertions-if-youre-awaiting-any-async-function-calls)
- [Can you write async tests that expect toThrow?](https://stackoverflow.com/questions/47144187/can-you-write-async-tests-that-expect-tothrow/47887098#47887098)
- [Writing Good Assertions](https://freecontent.manning.com/writing-good-assertions/)




