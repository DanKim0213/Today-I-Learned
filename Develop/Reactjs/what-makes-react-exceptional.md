# What Makes React Exceptional

TL;DR;

- Tell React your destination, not turn by turn where to go - Declarative UI Programming.
- All React “sees” is the UI tree you return, based on which it changes the DOM nodes.

So far, you've looked over [How Browser Renders Content](../Web/how-browser-renders-content.md)

What makes React exceptional? First, _[Declarative UI Programming](#declarative-ui-programming)_ changes the way your codes. And lastly, by _[React applying minimum operations](#react-applies-minimal-necessary-operations)_, the duration of browser painting is decreased.

## Declarative UI Programming

According to [Reacting to input with state](https://react.dev/learn/reacting-to-input-with-state):

> You declare **what you want to show**, and React figures out how to update the UI.

In React, you don’t directly manipulate the UI—meaning you don’t enable, disable, show, or hide components directly.

This could be an answer to _why should you use Reactjs rather than manipulating DOM by ourselves_.

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

According to [Render and Commit](https://react.dev/learn/render-and-commit) and [Preserving and Resetting State](https://react.dev/learn/preserving-and-resetting-state):

> React only changes **the DOM nodes** if there’s a difference between renders.

Let's see two examples:

```js
// tl;dr;React only updates the content of <h1> with the new time.
// Here is a component that re-renders with different props passed from its parent every second.
// The text doesn’t disappear when the component re-renders on the input.
export default function Clock({ time }) {
  return (
    <>
      <h1>{time}</h1>
      <input />
    </>
  );
}
```

Remember that it’s the position in the UI tree—not in the JSX markup—that matters to React!
React doesn’t know where you place the conditions in your function. All it “sees” is the tree you return.

```js
// tl;dr;Same component at the same position preserves state
import { useState } from "react";

export default function App() {
  const [isFancy, setIsFancy] = useState(false);
  return (
    <div>
      {isFancy ? <Counter isFancy={true} /> : <Counter isFancy={false} />}
      <label>
        <input
          type="checkbox"
          checked={isFancy}
          onChange={(e) => {
            setIsFancy(e.target.checked);
          }}
        />
        Use fancy styling
      </label>
    </div>
  );
}

// The above code could be:
import { useState } from "react";

export default function App() {
  const [isFancy, setIsFancy] = useState(false);
  if (isFancy) {
    return (
      <div>
        <Counter isFancy={true} />
        <label> <input ... /> Use fancy styling </label>
      </div>
    );
  }
  return (
    <div>
      <Counter isFancy={false} />
      <label> <input ... /> Use fancy styling </label>
    </div>
  );
}
```

<details>
<summary> 💡 What if you want these two Counters to be independent? </summary>

you can render them in two different positions:

```js
import { useState } from "react";

export default function Scoreboard() {
  const [isPlayerA, setIsPlayerA] = useState(true);
  return (
    <div>
      {isPlayerA && <Counter person="Taylor" />}
      {!isPlayerA && <Counter person="Sarah" />}
      <button
        onClick={() => {
          setIsPlayerA(!isPlayerA);
        }}
      >
        Next player!
      </button>
    </div>
  );
}
```

</details><br />

How is this possible? Let's check out what happens underneath React rendering. There are three steps until you see UI on screen:

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

Consequently, React figures out what DOM nodes to be changed while _Rendering the component_. And then, React applies minimal necessary operations.

## Furthermore

- [Why Component Must Be Pure ](./why-component-must-be-pure.md)
