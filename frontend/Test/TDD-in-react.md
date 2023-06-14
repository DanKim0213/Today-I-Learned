# How to TDD in React framework
One of the biggest concerns in React is that we can barely develop based on TDD. The reason why TDD is difficult for us that we cannot decouple a react component into views and logics per se. However, these days MobX saves us to decoulple them. Then, what design pattern allows us to TDD? MVVM?

## MVVM is not appropriate for TDD
You can unit-test on models. But, integration testing is not allowed on the design pattern as logics are tightly coupled onto react components. Thus, we need a proper design pattern: MVC.    

## MVC? That doesn't sound strange. But, is it allowed to use in Server-side architecture?
Yes. Let's see below.

A component in React can possibly consist of html tags (View) and states (Model) . This means that a component can be considered as a Controller: 
```js
const Component = () => {
  const [person, setPerson] = React.useState("Simpson");
  const eventHandler = () => { return "Hello, world!" };
  return (
    <p>Hi, I'm {person}</p>
  )
}
``` 

With the help of MobX, we can change the above component format like below:
```js
import personModel from './models/person';
const Component = () => {
  const [person] = React.useState(personModel);
  const eventHandler = () => { return "Hello, world!" };
  return (
    <p>Hi, I'm {person}</p>
  )
}
```

```js
class Person {
  name;
  constructor() {
    name = "Simpson";
  }
}
```

Now we can easily unit-test on the model.  

## Where can we do unit testing? Model 
Model itself is considered as Value object.
```js
```

However, we'd like to integration-test, too.

## Where can we do Integration testing? Service
With the help of TypeScript, we can introduce Interface and we use it on Service layer:
```js
```
Note that a service must manage its corresponsing model.

## Key Features
Keep in mind that event handlers belong to react component (Controller) and onto which we put services:
```js
import personService from './services/person';
const Component = () => {
  const [person] = React.useState(personService.getModel());
  const eventHandler = () => { 
    personService.doSomething();
    return "Hello, world!" 
  };
  return (
    <p>Hi, I'm {person}</p>
  )
}

```  

Also note that we can possibly introduce View model when we need to handle legacy models or we couldn't help setting models on our own when proceeding a project somewhat without discuss.  

The best way is that setting the same models as back-end developers do. It could get rid of View model layer :)  


## References
- https://medium.cobeisfresh.com/level-up-your-react-architecture-with-mvvm-a471979e3f21
- https://paulallies.medium.com/clean-mvvm-with-react-and-react-hooks-ebc37b22542f 
- https://www.detroitlabs.com/blog/2021/06/25/intro-to-mvvm-in-react-with-mobx/