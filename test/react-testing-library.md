# React Testing Library

> "The more your tests resemble the way your software is used, the more confidence they can give you." - Kent C. Dodds

> "React Testing Library encourages you to test your React components not too much in isolation, but in integration (integration test) with other components." - [RTL Guide](https://www.robinwieruch.de/react-testing-library/)

Utilities are included in this project based on the following guiding principles:

1. If it relates to rendering components, then it should deal with DOM nodes rather than component instances, and it should not encourage dealing with component instances.
2. It should be generally useful for testing the application components in the way the user would use it. We are making some trade-offs here because we're using a computer and often a simulated browser environment, but in general, utilities should encourage tests that use the components the way they're intended to be used.
3. Utility implementations and APIs should be simple and flexible.

## Table of Content

1. [Queries](#1-queries)
1. [Query Priority](#2-query-priority)
1. [User Interactions](#3-fireevent-vs-userevent)
1. [Asynchronous](#4-asynchronous)
1. [References](#5-references)

## 1. Queries

- getBy (default): getBy returns an element or an error. By throwing an error, we as developers notice early that **there is** something wrong in our test.
- queryBy: every time you are asserting that an element **isn't there**, use queryBy.
- findBy: The findBy search variant is used for asynchronous elements which **will be there eventually**.

[Testing Playground](https://testing-playground.com)

## 2. Query Priority

Based on [the Guiding Principles](https://testing-library.com/docs/guiding-principles), your test should resemble how users interact with your code (component, page, etc.) as much as possible.

we recommend [this order](https://testing-library.com/docs/queries/about#priority) of priority:

1. Queries Accessible to Everyone: getByRole > getByLabelText > getByPlaceholderTest > getByText > getByDisplayValue
2. Semantic Queries: getByAltText > getByTitle
3. Test IDs: getByTestId

## 3. fireEvent vs userEvent

- Whenever possible, use userEvent over fireEvent when using React Testing Library.
- "fireEvent dispatches DOM events, whereas user-event simulates full interactions, which may fire multiple events and do additional checks along the way."
- ```javascript
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

- ```javascript
  import * as React from "react";
  import { render, screen } from "@testing-library/react";
  import userEvent from "@testing-library/user-event";
  import App from "./App";

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
  ```

## 4. Asynchronous

- [Async Methods](https://testing-library.com/docs/dom-testing-library/api-async)

  - What is the relationship between findBy and waitFor? findBy methods are a combination of getBy queries and waitFor.
  - Returning a falsy condition is not sufficient to trigger a retry, the callback must throw an error in order to retry the condition. Here's a simple example.
  - waitFor may run the callback a number of times until the timeout is reached. Note that the number of calls is constrained by the timeout and interval options.
  - If you return a promise in the waitFor callback (either explicitly or implicitly with async syntax), then the waitFor utility will not call your callback again until that promise rejects.
  - ```
    await waitFor(() => expect(mockAPI).toHaveBeenCalledTimes(1))
    ```

- [Appearance and Disappearance](https://testing-library.com/docs/guide-disappearance)

  - Is there any case when you cannot avoid of using waitFor? Yes, when it comes to disappearance.
  - Waiting for appearance

    - ```javascript
      /** Using findBy Queries */
      test("movie title appears", async () => {
        // element is initially not present...
        // wait for appearance and return the element
        const movie = await findByText("the lion king");
        expect(movie).toBeInTheDocument();
      });
      ```
    - ```javascript
      /** Using waitFor */
      test("movie title appears", async () => {
        // element is initially not present...

        // wait for appearance inside an assertion
        await waitFor(() => {
          expect(getByText("the lion king")).toBeInTheDocument();
        });
      });
      ```

  - Waiting for disappearance
    - ```javascript
      test("movie title goes away", async () => {
        // element is initially present...
        // note use of queryBy instead of getBy to return null
        // instead of throwing in the query itself
        await waitFor(() => {
          expect(queryByText("i, robot")).not.toBeInTheDocument();
        });
      });
      ```

- Mock

  - When do you use mock? If you are developing in TDD, you could use mock frequently. However, in TDD or not, all apis hidden by mock must be replaced by your actual apis in your own repository eventually. So, I think it is benefitial to use mock when fetching data from servers. Especially, when apis from servers are not tested enough.
  - [REACT TESTING LIBRARY: ASYNCHRONOUS / ASYNC](https://www.robinwieruch.de/react-testing-library/)
  - "How do I fix "an update was not wrapped in act(...)" warnings?"
    - [link](https://testing-library.com/docs/react-testing-library/faq/)
    - "Generally speaking, approach 1 is preferred since it better matches the expectations of a user interacting with your app."
    - "Wait for the result of the operation in your test by using one of the async utilities like waitFor or a find\* query."

- When do you use async-await in test?
  - User Event such as click, change, and etc.
  - Components appear or disappear.
  - Fetch data from servers (alternatively, you can use Mock).

## 5. References

- [Testing Library](https://testing-library.com)
- [React Testing Library](https://www.robinwieruch.de/react-testing-library/)
- [User Interactions: userEvent](https://testing-library.com/docs/user-event/intro)
- [User Actions: fireEvent](https://testing-library.com/docs/dom-testing-library/api-events)
- [Why you should test with user-event](https://ph-fritsche.github.io/blog/post/why-userevent)

```

```
