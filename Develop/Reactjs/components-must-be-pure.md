# Component Must Be Pure

TL;DR;

- Components must be pure since, by doing so, React can restart rendering without wasting time.
- Strict mode can help surface mistakes caused by impure functions as soon as possible.
- `Event handler` is the saviour to comply with purity, in response to side effects.
- `useEffect()` call is your last resort, in response to side effects.

So far, you've looked over [What Makes React Exceptional](./what-makes-react-exceptional.md).

To make use of React, you should know that _Components Must Be Pure_. Let's figure out the surroundings of the concept: _[Keeping components pure](#keeping-components-pure)_, _[Strict Mode](#strict-mode)_, and _[Complying with purity](#complying-with-purity)_.

## Keeping components pure

According to [Keeping components pure](https://react.dev/learn/keeping-components-pure):

> In general, you should not expect your components to be rendered in any particular order. Also, calling components multiple times should not produce different JSX!

To achieve the above behaviors, you keep components pure. The following characteristics define what purity is:

- It minds its own business.
- Same inputs, same output.

Then, Why does React care about purity?

- Your components could run _in a different environment_—for example, on the server!
- You can improve performance by [skipping rendering](https://react.dev/reference/react/memo) components (Momoized component) whose inputs have not changed.
- If some data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render.

However, something has to change for such as updating the screen, starting an animation, changing the data. These changes, _a.k.a side effects_, happen "on the side", not during rendering.

## Strict Mode

Before you gotta know how to comply with purity while side effects happen, you should know `<StrictMode>`. `<StrictMode>` is very useful for letting you find common bugs in your components early during development.

Strict Mode enables the following development-only behaviors:

- Your components will [re-render an extra time](https://react.dev/reference/react/StrictMode#fixing-bugs-found-by-double-rendering-in-development) to find bugs caused by impure rendering.
- Your components will [re-run Effects an extra time](https://react.dev/reference/react/StrictMode#fixing-bugs-found-by-re-running-effects-in-development) to find bugs caused by missing Effect cleanup.
- Your components will [be checked for usage of deprecated APIs](https://react.dev/reference/react/StrictMode#fixing-deprecation-warnings-enabled-by-strict-mode).

## Complying with purity

Do not change any objects or variables that existed before rendering, in order to comply with purity. In other words, in React there are three kinds of inputs that you can read while rendering: `props`, `state`, and `context`.

According to [Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component):

> React components use **props** to communicate with each other. Every parent component can pass some information to its child components by giving them props.

According to [Can event handlers have side effects?](https://react.dev/learn/responding-to-events#can-event-handlers-have-side-effects):

> Unlike rendering functions, **event handlers** don’t need to be pure, so it’s a great place to change something—for example, change an input’s value in response to typing, or change a list in response to a button press.

To make a conclusion by combining the two excerpts, you need to update `state` within `event handlers` since `event handlers` don't run during rendering! What if components communicate with each other with the same `state`? Lift `state` up to its parent component and then pass `state` and `event handlers` as `props` down to them.

Note that props are immutable (i.e. read-only snapshots in time) since every render receives a new version of props. Therefore, components can be pure with props and you must not mutate the props by yourself.

If you’ve exhausted all other options and can’t find the right event handler for your side effect, you can still attach it to your returned JSX with a `useEffect` call in your component. However, this approach should be your last resort.

## Furthermore

- [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

---

If you have any questions or ideas, please leave a comment on this issue :)
