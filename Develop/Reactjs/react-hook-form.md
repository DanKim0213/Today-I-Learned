# React Hook Form

Simple form validation with React Hook Form.

[Quick Start](https://react-hook-form.com/get-started#Quickstart)

## Example

```ts
import { useForm, SubmitHandler } from "react-hook-form";

type IFormInput = {
  example: string;
  exampleRequired: string;
};

export default function App() {
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors },
  } = useForm<IFormInput>();
  const onSubmit: SubmitHandler<IFormInput> = (data) => console.log(data);

  console.log(watch("example")); // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input defaultValue="test" {...register("example")} />

      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("exampleRequired", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}

      <input type="submit" />
    </form>
  );
}
```

## How do I find out errors

As you see the following code, I could find out which error I encountered by formState: { errors }:

```ts
export default function App() {
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors },
  } = useForm<IFormInput>();
  ...

  console.log(errors); // errors: { exampleRequired: { type: "maxLength", message: "", ref: <input type="text">}}

  return (
    <input {...register("exampleRequired", { required: true, maxLength: 10 })} />
  )

}
```

## How do I set default values for inputs?

As I see the reference, I have two options to declare default values:

```ts
export default function App() {
  /* Option 1: declare default values right away
    const { register, handleSubmit } = useForm({
      defaultValues: {
        firstName: "",
        lastName: "",
        iceCreamType: {},
      },
    }) 
  */

  /* Option 2: declare a default value for each */
  return <input defaultValue="test" {...register("example")} />;
}
```
