# React + TypeScript

## useContext as a custom hook

## You may not need defaulProps in Functional components

https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/default_props

https://medium.com/@matanbobi/react-defaultprops-is-dying-whos-the-contender-443c19d9e7f1

```ts
const defaultUser = { firstName: "John", lastName: "Doe" }; // for immutability!
const Greet = ({ user = defaultUser }) => {
  return <div>{`Hi ${user.firstName} ${user.lastName}`}</div>;
};
```

## null vs undefined

https://stackoverflow.com/questions/6604749/what-reason-is-there-to-use-null-instead-of-undefined-in-javascript

> When defining a variable that is meant to later hold an object, it is advisable to initialize the variable to null as opposed to anything else. That way, you can explicitly check for the value null to determine if the variable has been filled with an object reference at a later time

https://stackoverflow.com/questions/5076944/what-is-the-difference-between-null-and-undefined-in-javascript

![img](https://i.stack.imgur.com/T9M2J.png)

> TLDR; Don't use the undefined primitive. It's a value that the JS compiler will automatically set for you when you declare variables without assignment or if you try to access properties of objects for which there is no reference. On the other hand, use null if and only if you intentionally want a variable to have "no value".

Use null for the variable to be assigned soon
