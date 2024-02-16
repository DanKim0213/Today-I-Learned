# Test as much as Users would use

TL;DR;

- Priority when to query: `Role` > `LabelText` > `Text`.
- Avoid to use `TestId`.
- Use `user-event` over `fire-event`.
- You can't access component methods or the component instance.

Make sure you've read [Introduction to Test](./introduction-to-test.md).

## How users interact with your code

> It should be generally useful for testing the application components in the way the user would use it. - [Guiding Principles](https://testing-library.com/docs/guiding-principles/)

According to [Priority](https://testing-library.com/docs/queries/about#priority):

```
Queries Accessible to Everyone:
Role > LabelText > PlaceholderText > Text > DisplayValue

Semantic Queries:
AltText > Title

Test IDs:
TestId
```

In my experience this doc is not enough. Therefore, here is a practical guide:

1. `Role`
2. (`LabelText` > `PlaceHolderText` to control Input) |
   (`DisplayValue` to control elements based on the Input value) |
   (`Text` to control elements except for Input)
3. `TestId`

Of course, you need to get used to [roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#roles) and [states](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#states_and_properties) for testing as much as users would use, such as:

```js
const $button = screen.getByRole("button", { pressed: true });
```

Here are common states:

```
aria-checked, aria-pressed, aria-level, aria-disabled
```

One thing to avoid is that TestIds because users cannot see (or hear) these, so this is only recommended for cases where you can't match by role or text or it doesn't make sense (e.g. the text is dynamic).

## User Event

> When you are not only serving static content it is of uttermost importance that your components react on user interactions correctly. This is where `user-event` comes into the picture. - [Why you should test with user-event](https://ph-fritsche.github.io/blog/post/why-userevent)

The problem of `fire-event` is that the browser usually does more than just trigger one event for one interaction.

The solution to the problem is `user-event`. `user-event` allows you to describe a user interaction instead of a concrete event. It adds visibility and interactability checks along the way and manipulates the DOM just like a user interaction in the browser would.

In other words,

> `fire-event` dispatches DOM events, whereas `user-event` simulates full interactions, which may fire multiple events and do additional checks along the way. - [Differences from fireEvent](https://testing-library.com/docs/user-event/intro#differences-from-fireevent)

One thing to keep in mind is that `act()` wraps already `user-event` since `user-event` consists of a group of `fire-events`:

> React Testing Library wraps render and fireEvent in a call to act already so most cases should not require using it manually - [Events](https://testing-library.com/docs/react-testing-library/cheatsheet/#events) and [Kent C. Dodds](https://github.com/testing-library/user-event/issues/497#issuecomment-729897974)

For more information of `act()`, check out [what act() is](https://legacy.reactjs.org/docs/testing-recipes.html#act) and [why you should act() from @testing-library/react over react-dom/test-utils](https://legacy.reactjs.org/docs/testing-recipes.html#act).

Whenever possible, use `user-event` over `fire-event` when using React Testing Library:

```js
import * as React from "react";
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import App from "./App";

/** user-event */
describe("App", () => {
  it("renders App component", async () => {
    render(<App />);

    // wait for the user to resolve
    await screen.findByText(/Signed in as/);

    expect(screen.queryByText(/Searches for JavaScript/)).toBeNull();

    await userEvent.type(screen.getByRole("textbox"), "JavaScript");

    expect(screen.getByText(/Searches for JavaScript/)).toBeInTheDocument();
  });
});
/** fire-event */
describe("App", () => {
  it("renders App component", async () => {
    render(<App />);

    // wait for the user to resolve
    await screen.findByText(/Signed in as/);

    expect(screen.queryByText(/Searches for JavaScript/)).toBeNull();

    fireEvent.change(screen.getByRole("textbox"), {
      target: { value: "JavaScript" },
    });

    expect(screen.getByText(/Searches for JavaScript/)).toBeInTheDocument();
  });
});
```

## Avoid Implementation Details

Last but not least you must avoid implementation details.

According to [Testing Implementation details](https://kentcdodds.com/blog/testing-implementation-details),

> Implementation details are things which users of your code will not typically use, see, or even know about.

Back then with `Enzyme`, developers could write tests of `state`.

```js
// __tests__/accordion.enzyme.js
...
test('setOpenIndex sets the open index state properly', () => {
  const wrapper = mount(<Accordion items={[]} />)
  expect(wrapper.state('openIndex')).toBe(0)
  wrapper.instance().setOpenIndex(1)
  expect(wrapper.state('openIndex')).toBe(1)
})
```

However, you are not able to write tests of `state` with `Testing library`. This sounds awesome!:

```js
// __tests__/accordion.rtl.js
...
test("can open accordion items to see the contents", () => {
  const hats = { title: "Favorite Hats", contents: "Fedoras are classy" };
  const footware = {
    title: "Favorite Footware",
    contents: "Flipflops are the best",
  };
  render(<Accordion items={[hats, footware]} />);

  expect(screen.getByText(hats.contents)).toBeInTheDocument();
  expect(screen.queryByText(footware.contents)).not.toBeInTheDocument();

  userEvent.click(screen.getByText(footware.title));

  expect(screen.getByText(footware.contents)).toBeInTheDocument();
  expect(screen.queryByText(hats.contents)).not.toBeInTheDocument();
});
```

The rule of thumb to avoid implementation details is to rely on `queries` and `user-event`.

---

If you have any questions or ideas, please make a comment of this issue :)
