# Component Must Be Pure

TL;DR;

- Components must be pure since, by doing so, React can restart rendering without wasting time.
- TODO: Props
- Strict mode can help surface mistakes caused by impure functions as soon as possible.

So far, we've looked over [What Makes React Exceptional](./what-makes-react-exceptional.md).

TODO: ...

## Keeping components pure

According to [Keeping components pure](https://react.dev/learn/keeping-components-pure):

In general, you should not expect your components to be rendered in any particular order as well as calling components multiple times should not produce different JSX! To achieve these rules, components must comply with purity.

The following characteristics define what purity is:

- It minds its own business.
- Same inputs, same output.

Then, Why does React care about purity?

- Your components could run _in a different environment_—for example, on the server!
- You can improve performance by [skipping rendering](https://react.dev/reference/react/memo) components (Momoized component) whose inputs have not changed.
- If some data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render.

## What can I do to comply with purity?

According to [Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component):

- Props
- strict mode
- Side effect

If you’ve exhausted all other options and can’t find the right event handler for your side effect, you can still attach it to your returned JSX with a useEffect call in your component. However, this approach should be your last resort.

## Furthermore

- [how do declare state cleverly](/)
