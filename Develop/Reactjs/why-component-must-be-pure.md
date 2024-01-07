# Why Component Must Be Pure

According to [Keeping components pure](https://react.dev/learn/keeping-components-pure)

Rendering must always be a pure calculation:

Same inputs, same output. Given the same inputs, a component should always return the same JSX. (When someone orders a salad with tomatoes, they should not receive a salad with onions!)
It minds its own business. It should not change any objects or variables that existed before rendering. (One order should not change anyone else’s order.)
Otherwise, you can encounter confusing bugs and unpredictable behavior as your codebase grows in complexity. When developing in “Strict Mode”, React calls each component’s function twice, which can help surface mistakes caused by impure functions.

## Furthermore

Previous topic:

- [What Makes React Exceptional](./what-makes-react-exceptional.md)

Next topic:

- [how do declare state cleverly](/)
