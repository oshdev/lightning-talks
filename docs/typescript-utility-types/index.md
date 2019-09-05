# The TypeScript Utility Types

## What is it?

Utility type is not a specific type, but simply an abstraction to create more useful ones.
They are available globally which means that you don't need to import them.

## Why to use it?

They are great at adding more semantical meaning to the type declarations, make an easy way 
Not to mention that they are amazing tool that IDEs can read from and help the coder - 

## How to use it?

Like any other type. You can use them directly or alternatively you can declare a new type by using one of those.
You may potentially gain the benefit of being explicit about what you are trying to achieve by doing so,
but in some cases it might be good enough without that. I guess that's context depending.

## Asumptions

In order to understand these, I assume you have some TypeScript understanding -
the basic and complex types (intersection, union, nullable, alias, etc), interfaces and classes, functions, generics

## The types

### Table of Contents

- [`Partial<T>`](#Partial)
- [`Readonly<T>`](#Readonly)
- [`Record<K,T>`](#Record)
- [`Pick<T,K>`](#Pick)
- [`Omit<T,K>`](#Omit)
- [`Exclude<T,U>`](#Exclude)
- [`Extract<T,U>`](#Extract)
- [`NonNullable<T>`](#NonNullable)
- [`ReturnType<T>`](#ReturnType)
- [`InstanceType<T>`](#InstanceType)
- [`Required<T>`](#Required)
- [`ThisType<T>`](#ThisType)

### Partial
```typescript
Partial<T>
```
Partial type makes all of the properties of `T` as optional, for instance:
```typescript
type SomeOptions = Partial<RequiredOptions>
```


### Pick

Pick is one of the utility types of typescript.
As the other utility types, it’s used for common transformations and is available globally, i.e. no need to import it.
How do you use it?
The signature is as follows:

Pick<T, K>

Where `T` is the type you want to pick from and `K` is the property you want to pick. In practice you will want to pick a complex type, for instance a union of properties as in the following example:

type NineNineLogger = Pick<winston.Logger, 'debug' | 'info' | 'error'>
Why would you want to use it?
There’s a number of potential applications, but in general you will use it when you only want to use a subset of the properties for a specific reason. Following the example above the `winston.Logger` interface defines a lot of properties. We chose it because it’s easy to integrate, however we don’t really need all of the tools that it provides. Also we want to configure it once globally and then just use it. It removes a lot of clutter blah blah

#### Reference:
https://www.typescriptlang.org/docs/handbook/utility-types.html
