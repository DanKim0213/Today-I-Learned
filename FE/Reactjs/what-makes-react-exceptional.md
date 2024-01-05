# What Makes React Exceptional

## Declarative UI Programming

According to [Reacting to input with state](https://react.dev/learn/reacting-to-input-with-state):

> You declare **what you want to show**, and React figures out how to update the UI.

In React, you don’t directly manipulate the UI—meaning you don’t enable, disable, show, or hide components directly.

This could be an answer to _why should we use Reactjs rather than manipulating DOM by ourselves_.

It seems like, when you take a texi, telling a driver your destination instead of telling him turn by turn where to go.

In other words, reactjs is based on _Declarative UI programming_ while DOM manipulation is based on _Imperative UI programming_

```js
// DOM manipulation; Imperative UI Programming;
async function handleFormSubmit(e) {
  e.preventDefault();
  disable(textarea);
  disable(button);
  show(loadingMessage);
  hide(errorMessage);
  try {
    await submitForm(textarea.value);
    show(successMessage);
    hide(form);
  } catch (err) {
    show(errorMessage);
    errorMessage.textContent = err.message;
  } finally {
    hide(loadingMessage);
    enable(textarea);
    enable(button);
  }
}
```

## React applies minimal necessary operations

According to [Render and Commit](https://react.dev/learn/render-and-commit):

> React only changes **the DOM nodes** if there’s a difference between renders.

There are three steps until you see UI on screen:

1. Triggering a render
2. Rendering the component
3. Committing to the DOM

and then Painting (Browser Rendering).

The detail of these steps depends on either **when initializing a component** or **when updating a component's state**. If you want to know it, check out the above link.

To put it simply,

- _Triggering a render_ comes from outside either by running your app or by occuring user events. Then, initializing the component or updating the component’s (or one of its ancestors’) state has occurred.
- _Redering the component_ is an action inside i.e. React calling your components. In doing so, React will calculate which of their properties, if any, have changed since the previous render.
- _Committing to the DOM_ is that React modifies the DOM.

(Note that Commiting is not equal to Painting.)

## Furthermore

Previous topic:

- [How Browser Works](../Web/how-browser-works.md)

Next topic:

- [Why Component Must Be Pure ](./why-component-must-be-pure.md)
