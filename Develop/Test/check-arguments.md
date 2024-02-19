# Check arguments

TL;DR;

- You have two options to check arguments.
- One of them is `mockFn.toHaveBeenCalledWith()`.
- The other is `mockFn.toHaveBeenReturnedWith()`.

Make sure you've read [Introduction to Test](./introduction-to-test.md).

## How do I check arguments?

If you want to know what exactly the function have been called with, use `mockFn.toHaveBeenCalledWith()`.

However, "exactly" is not cooperated with testing :)

Sometimes, you only know an target object, such as `{ id, name }`, will be passed over with some callback functions and unknown arguments. And, you don't need to check other than the target object.

You are able to have two solutions to this problem:

- use `jest.toHaveBeenCalledWith()` in addition to `jest.mock()` with `jest.fn()`.
- use `jest.toHaveReturnedWith()` in addition to `jest.mock()`.

As you'll see, the option 1 is verbose while the option 2 is obvious.

## Option 1. `jest.toHaveBeenCalledWith()` + `jest.mock()` with `jest.fn()`

```js
// ./test/App.Filter.test.js
import App from "../src/App";
import Todo from "../src/components/Todo";

jest.mock("../src/components/Todo");
jest.mock("../src/components/Form");

const tasks = [
  { name: "Eat", id: "todo-0", completed: false },
  { name: "Drink", id: "todo-1", completed: true },
];

describe("Filter Integration test", () => {
  it("changes the filter to show only completed tasks", async () => {
    const mockTodo = jest.fn((props) => "this is: " + props);
    Todo.mockImplementation((props) => {
      return mockTodo({
        id: props.id,
        name: props.name,
        completed: props.completed,
      });
    });
    render(<App tasks={tasks} />);

    expect(mockTodo).toHaveBeenCalledTimes(2);
    mockTodo.mockClear();
    const $filter = screen.getByRole("button", { name: /complete/i });
    await userEvent.click($filter);

    expect(mockTodo).toHaveBeenCalledWith(tasks[1]);
  });
});
```

## Option 2. `jest.toHaveBeenReturnedWith()` + `jest.mock()`

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

## Caution: when checking React component with props

> Objects are not valid as a React child (found: object with keys {id, name, completed, toggleTaskCompleted, deleteTask, editTask}).

You will encounter the above error when `mockFn.mockImplementation((props) => props)` is used.

Therefore, I make the mock todo component return string type using `JSON.stringify()` because:

- `<Todo />` is considered as a component in `<App />` and string type is one of the return types of components.
- `JSON.stringify()` helps you stringify an object or an array.

```js
MockTodo.mockImplementation((props) =>
  JSON.stringify({
    id: props.id,
    name: props.name,
    completed: props.completed,
  })
);
```

---

If you have any questions or ideas, please leave a comment on this issue :)
