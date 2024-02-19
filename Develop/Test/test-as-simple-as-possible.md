# Test as simple as possible

TL;DR;

- Write Integration tests rather than Unit tests.
- Isolate modules by mocking.
- Separte concerns by tests for meaningful test fails.

Make sure you've read [Introduction to Test](./introduction-to-test.md).

## Integration tests rather than Unit tests

> Write tests. Not too many. Mostly integration.- [tweeted](https://twitter.com/rauchg/status/807626710350839808) the CEO of Vercel Guillermo Rauch.

In most cases, integration tests are more worthy than unit tests:

```js
// ./test/App.Todo.test.js
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

    expect($drinkCheckbox).not.toBeInTheDocument();
  });
  ...
});
```

```js
// ./src/components/Todo.test.js
describe("Todo", () => {
  ...
  it("deletes a task", async () => {
    const deleteTask = jest.fn();
    render(<Todo name="Eat" id="todo-0" deleteTask={deleteTask} />);

    await userEvent.click(screen.getByRole("button", { name: /delete/i }));

    expect(deleteTask).toHaveBeenCalledTimes(1);
  });
  ...
});
```

As you see, those are testing the same thing, "delets a task". However, the assertions are different from each other. The assertion statement in the integraion test expects that the checkbox disappears while the assertion in the unit test expects that the handler passed to as props is called once.

Therefore, you can skip to write unit tests unless they are necessary. It would be better to write a few worthy tests for maintenance than bunch of worthless unit tests.

Here are exceptions though because the following tests are testing a user accessibility:

```js
// ./src/components/Todo.test.js
describe("Todo", () => {
  ...
  it("focuses on the connected input when editing", async () => {
    render(<Todo name="Eat" id="todo-0" />);

    await userEvent.click(screen.getByRole("button", { name: /edit/i }));
    const $textbox = screen.getByRole("textbox");

    expect($textbox).toHaveFocus();
  });

  it("focuses on the edit button when editing is canceled", async () => {
    render(<Todo name="Eat" id="todo-0" />);

    await userEvent.click(screen.getByRole("button", { name: /edit/i }));
    await userEvent.click(screen.getByRole("button", { name: /cancel/i }));
    const $editButton = screen.getByRole("button", { name: /edit/i });

    expect($editButton).toHaveFocus();
  });
});
```

## Isolation of modules

To write integration tests and detect bugs as soon as possible, you should isolate modules by `mockFn.mock()`.

You don't need to include node_modules:

```js
// ./test/App.Todo.test.js
jest.mock("nanoid", () => {
  return {
    nanoid: jest.fn(),
  };
});
```

And, you don't need to include irrelvant components:

```js
// ./test/App.Todo.test.js
jest.mock("../src/components/FilterButton");
jest.mock("../src/components/Form");
```

However, if you need to include relevant component, use `mockFn.mockImplementation()` or `mockFn.mockReturnValue(value)`:

```js
// ./test/App.Filter.test.js
import App from "../src/App";
import MockTodo from "../src/components/Todo";

jest.mock("../src/components/Todo");
jest.mock("../src/components/Form");

const tasks = [
  { name: "Eat", id: "todo-0", completed: false },
  { name: "Drink", id: "todo-1", completed: true },
];

describe("Filter Integration test", () => {
  it("changes the filter to show only completed tasks", async () => {
    MockTodo.mockImplementation((props) =>
      JSON.stringify({
        id: props.id,
        name: props.name,
        completed: props.completed,
      })
    );
    render(<App tasks={tasks} />);

    expect(MockTodo).toHaveBeenCalledTimes(2);
    MockTodo.mockClear();
    const $filter = screen.getByRole("button", { name: /complete/i });
    await userEvent.click($filter);

    expect(MockTodo).toHaveReturnedWith(
      JSON.stringify({
        id: tasks[1].id,
        name: tasks[1].name,
        completed: tasks[1].completed,
      })
    );
  });
});
```

## Separation of Concerns

When I test `edits and save a task`, I am sure that `<App />` renders with two `<Todo />` components because I've already tested that `renders todo` successes.

Thus, I don't need to `expect($checkboxes).toHaveLength(2);` at the beginning of the test `edits and save a task`:

```js
// ./test/App.Todo.test.js
describe("Todo Integration test", () => {
  it("renders todo", () => {
    render(<App tasks={tasks} />);

    const $checkboxes = screen.getAllByRole("checkbox");

    expect($checkboxes).toHaveLength(2);
  });

  it("edits and save a task", async () => {
    render(<App tasks={tasks} />);

    const $todo = screen.getByLabelText(/drink/i).closest("li");
    const $editButton = within($todo).getByRole("button", { name: /edit/i });
    await userEvent.click($editButton);
    await userEvent.type(screen.getByRole("textbox"), "edited Task");
    await userEvent.click(screen.getByRole("button", { name: /save/i }));
    const $drinkCheckbox = screen.queryByLabelText(/drink/i);
    const $checkboxes = screen.getAllByRole("checkbox");

    expect($drinkCheckbox).not.toBeInTheDocument();
    expect($checkboxes).toHaveLength(2);
  });
});
```

Some developers would say that it looks better to combine the two tests for less codes. However, I can argue that this looks much better because, by separation of concern, you can get a meaningful test fail, e.g. `renders todo`, as soon as possible rather than tracking down error logs.

---

If you have any questions or ideas, please leave a comment on this issue :)
