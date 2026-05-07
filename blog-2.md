# Generics in TypeScript: Writing Reusable, Strictly Typed Code

## Introduction

One of the most powerful features TypeScript adds on top of JavaScript is Generics. Without generics, you face a difficult choice whenever you write a reusable utility: either use `any` and lose all type safety, or write separate versions of the same logic for every type you need. Generics solve this problem by letting you write a single function, class, or interface that works across many types while preserving the full benefits of the type system. The type is not fixed at definition time it is supplied by the caller, and TypeScript enforces everything accordingly.

## The Problem Generics Solve

Consider a simple function that returns the first element of an array. Without generics, you might write it like this:

```typescript
function first(arr: any[]): any {
  return arr[0];
}

const result = first([1, 2, 3]);
// result is typed as `any` — we've lost the information that it's a number
```

The function works, but the caller gets back `any`. If they try to call `.toFixed()` on the result, TypeScript will not catch a mistake. The type information was thrown away the moment the array was passed in.

## Introducing Generic Syntax

A generic function uses a type parameter conventionally written as `T` that acts as a placeholder for the actual type, which TypeScript infers from the call site:

```typescript
function first<T>(arr: T[]): T {
  return arr[0];
}

const result = first([1, 2, 3]);
// result is typed as `number` — TypeScript inferred T = number
```

Now TypeScript knows the return type is exactly the same type as the array elements. The caller gets a fully typed result, and the function works for arrays of any type without code duplication.

## Generic Constraints

Sometimes you need to restrict what types a generic parameter can be. You do this with the `extends` keyword:

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { id: 1, name: "Alice", age: 30 };
const name = getProperty(user, "name"); // typed as string
const id = getProperty(user, "id"); // typed as number

getProperty(user, "email"); // Compile-time error: "email" doesn't exist on user
```

The constraint `K extends keyof T` ensures the key must actually exist on the object. TypeScript also knows the return type `T[K]` which is the type of that specific property. This is far more powerful than returning `any`.

## Generic Interfaces and Classes

Generics are not limited to functions. You can apply them to interfaces and classes to build strongly typed data structures.

**Generic Interface:**

```typescript
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

const userResponse: ApiResponse<{ id: number; name: string }> = {
  data: { id: 1, name: "Alice" },
  status: 200,
  message: "Success",
};
```

The same `ApiResponse` shape can wrap a user, a product, a list of orders any type you choose. The structure stays consistent and typed throughout.

**Generic Class:**

```typescript
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }

  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }
}

const numberStack = new Stack<number>();
numberStack.push(10);
numberStack.push(20);
const top = numberStack.pop(); // typed as number | undefined
```

A single `Stack<T>` class works for numbers, strings, or any custom type. No duplication, no `any`, no loss of type information.

## Multiple Type Parameters

You can use more than one type parameter when a function or structure involves more than one type:

```typescript
function zip<A, B>(arrayA: A[], arrayB: B[]): [A, B][] {
  return arrayA.map((item, index) => [item, arrayB[index]]);
}

const pairs = zip([1, 2, 3], ["a", "b", "c"]);
// typed as [number, string][]
```

TypeScript infers both `A` and `B` from the call site and applies them consistently through the return type.

## Why Generics Matter in Real Projects

In large codebases, generics prevent a category of bugs that `any`-based code invites incorrect type assumptions that only surface at runtime. They also eliminate the maintenance burden of duplicate functions for different types. A generic `sortBy<T>`, `paginate<T>`, or `findById<T>` works for any domain model, and TypeScript will catch misuse the moment it happens rather than in production.

## Conclusion

Generics are the mechanism that makes TypeScript reusability safe. They let you write logic once, parameterize the types, and let the type system verify every usage at compile time. Whether applied to a small utility function, a data structure class, or a full API layer, generics give you the flexibility of dynamic code with the safety of static types which is precisely the value TypeScript is designed to deliver.
