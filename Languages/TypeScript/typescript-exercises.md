# Typescript Exercises

## 1. Objects

## 2. Union types

## 3. Narrowing

## 4. Utility types

## 5. Function overloads

## 6. Generics

## Questions

### Q. Why is `Type Guard` needed instead of `intanceof`?

### Q. Is type Indexing possible with interfaces?

### Q. which one between `Type` and `Interface` should I use since they are interchangeable?

> You should consider consistency and augmentation. - Effective Typescript, item 13

If you are working in a codebase that consistently uses `interface`, stick with `interface`. The same goes for `Type`. 

Else:
- Publishing type declarations for an API? `interface`.
- Using internally in your project? `Type` since declaration merging, which is only available in `interface`, is likely to be a mistake.



### Q. (s: string | null) => void vs (s?: string) => void

A. Same
