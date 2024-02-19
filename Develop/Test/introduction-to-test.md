# Introduction to Test

TL;DR;

- Test as simple as possible.
- Test as much as users would use.
- Test as precisely as possible.

> [The more your tests resemble the way your software is used, the more confidence they can give you.](https://testing-library.com/docs/guiding-principles/)

One of the reasons why you write tests is to get high confidence that your components are working for your users. However, [Testing Implementation Details](https://kentcdodds.com/blog/testing-implementation-details) slow you and your team down. In other words, you must avoid accessing component methods or the component instance!

Then, how do you write tests? Write tests [the way the user would use your application](https://testing-library.com/docs/guiding-principles/). To achieve this, you should use [testing-library](https://testing-library.com), [jest-dom](https://github.com/testing-library/jest-dom), and [jest](https://jestjs.io).

Let's see an example:

```js
import { render, screen } from "@testing-library/react";
import App from "./App";
import "@testing-library/jest-dom";

jest.mock("nanoid", () => {
  return {
    nanoid: jest.fn(),
  };
});

const tasks = [
  { name: "Eat", id: "todo-0" },
  { name: "Drink", id: "todo-1" },
];

describe("App component", () => {
  it("renders App component", () => {
    render(<App tasks={tasks} />);

    const $heading = screen.getByRole("heading", { level: 1 });
    // screen.debug();

    expect($heading).toHaveTextContent(/todomatic/i);
  });
});
```

You will learn three parts of how to write tests based on [MDN Todo tested by DanKim0213](https://github.com/DanKim0213/todo-react) :

- [Test as simple as possible](./test-as-simple-as-possible.md)
- [Test as much as users would use](./test-as-much-as-users-would-use.md)
- [Test as precisely as possible](./test-as-precisely-as-possible.md)

## Furthermore

- ~~[How to setup before Testing]()~~
- ~~[Warning-not wrapped in act()]()~~
- [Check arguments](./check-arguments.md)
- [Index of Kent C. Dodds](./index-of-kent-c-dodds.md)

## Other References

- [MDN todo project](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started)
- [Common Mistakes](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)
- [react-testing-library-course by Kent C. Dodds](https://github.com/kentcdodds/react-testing-library-course/tree/main)
- [Learning](https://testing-library.com/docs/learning/)

---

If you have any questions or ideas, please leave a comment on this issue :)
