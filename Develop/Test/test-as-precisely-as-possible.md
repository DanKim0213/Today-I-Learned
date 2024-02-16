# Test as precisely as possible

TL;DR;

- Use proper queries.
- Make your tests more declarative.
- Query within elements.

Make sure you've read [Introduction to Test](./introduction-to-test.md).

## Use proper queries

Using proper queries helps you to test precisely. Also, it help you to get feedback as soon as possible by throwing an error.

[Types of Queries](https://testing-library.com/docs/queries/about#types-of-queries):

- getBy: `getBy` returns an element or an error. By throwing an error, we as developers notice early that **there is** something wrong in our test.
- queryBy: every time you are asserting that an element **isn't there**, use `queryBy`.
- findBy: The `findBy` search variant is used for asynchronous elements which **will be there eventually**.

Let's see an example:

```js
// ./test/App.Todo.test.js
...
describe("Todo Integration test", () => {
  ...
  it("deletes a task", async () => {
    render(<App tasks={tasks} />);

    const $todo = screen.getByLabelText(/drink/i).closest("li"); // If not existed, throw an error
    const $deleteButton = within($todo).getByRole("button", {
      name: /delete/i,
    });
    await userEvent.click($deleteButton);
    const $drinkCheckbox = screen.queryByLabelText(/drink/i); // If not existed, null

    expect($drinkCheckbox).not.toBeInTheDocument();
  });
});

```

## Make your tests more declarative

> The @testing-library/jest-dom library provides a set of custom jest matchers that you can use to extend jest. These will make your tests more declarative, clear to read and to maintain. - [Jest-dom](https://github.com/testing-library/jest-dom)

For example, you want to test an element disappears. To achieve this, you can assert it either `.toBeNull()` or `.not.toBeInTheDocument()`:

```js
// ./test/App.Todo.test.js
...
describe("Todo Integration test", () => {
  ...
  it("deletes a task", async () => {
    render(<App tasks={tasks} />);

    const $todo = screen.getByLabelText(/drink/i).closest("li");
    const $deleteButton = within($todo).getByRole("button", {
      name: /delete/i,
    });
    await userEvent.click($deleteButton);
    const $drinkCheckbox = screen.queryByLabelText(/drink/i);

    // expect($drinkCheckbox).toBeNull(); // without `jest-dom`
    expect($drinkCheckbox).not.toBeInTheDocument();
  });
});

```

However, `.toBeInTheDocument()` is more worthy because it searches for it from the perspective of DOM:

> This allows you to assert whether an element is present in the document or not. - [API - toBeInTheDocument](https://github.com/testing-library/jest-dom?tab=readme-ov-file#tobeinthedocument)

In addition, assert its state by such as `.toHaveFocus()` or `.toHaveChecked()` instead of its style by `.toHaveClass()`. For more information, check out [ARIA - states and properties](<[states](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#states_and_properties)>):

```js
// ./test/App.Todo.test.js
describe("Todo Integration test", () => {
  it("focuses on Heading when it deletes a task", async () => {
    render(<App tasks={tasks} />);

    await userEvent.click(
      screen.getAllByRole("button", { name: /delete/i })[tasks.length - 1]
    );
    const $title = screen.getByRole("heading", { name: /remaining/i });

    expect($title).toHaveFocus(); // **
  });
});
```

## Query within elements

> `within` (an alias to `getQueriesForElement`) takes a DOM element and binds it to the raw query functions, allowing them to be used without specifying a container. - [API-within](https://testing-library.com/docs/dom-testing-library/api-within/)

`within()` helps you get an element as user would use because by which you can use query subsequently:

```js
// ./test/App.Todo.test.js
...
describe("Todo Integration test", () => {
  ...
  it("deletes a task", async () => {
    render(<App tasks={tasks} />);

    const $todo = screen.getByLabelText(/drink/i).closest("li");
    const $deleteButton = within($todo).getByRole("button", {
      name: /delete/i,
    }); // query within $todo
    await userEvent.click($deleteButton);
    const $drinkCheckbox = screen.queryByLabelText(/drink/i);

    expect($drinkCheckbox).not.toBeInTheDocument();
  });
});
```

Here are mistakes I made:

- `Array.from().find()` cannot throw an error while `getBy()` can:

```js
// ./test/App.Todo.test.js
...
describe("Todo Integration test", () => {
  ...
  it("deletes a task", async () => {
    ...
    const $buttons = screen
      .getByLabelText(/drink/i)
      .closest("li")
      .querySelectorAll("button");
    const $deleteButton = Array.from($buttons).find((el) =>
      new RegExp(/delete/i).test(el.textContent)
    ); // **
    ...
  });
});

```

- Testing with only one Todo is inappropriate when integration testing:

```js
// ./test/App.Todo.test.js
...
describe("Todo Integration test", () => {
  ...
  it("deletes a task", async () => {
    render(<App tasks={[tasks[1]]} />); // **

    const $deleteButton = screen.getByRole('button', { name: /delete/i });
    ...
  });
});
```

---

If you have any questions or ideas, please make a comment of this issue :)
