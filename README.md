# Advanced Problem Solving with TypeScript & OOP

## Overview

This repository contains solutions for Assignment B7A1, covering core TypeScript concepts including type safety, generics, interfaces, class inheritance, and utility types.

## File Structure

```
├── solutions.ts    All 7 coding solutions
├── blog-1.md       Blog: any vs unknown and type narrowing
├── blog-2.md       Blog: Generics in TypeScript
└── README.md       This file
```

## Problems Solved

| #   | Problem                               | Concept                           |
| --- | ------------------------------------- | --------------------------------- |
| 1   | `filterEvenNumbers`                   | Array filtering                   |
| 2   | `reverseString`                       | String manipulation               |
| 3   | `checkType` with `StringOrNumber`     | Union types & type guards         |
| 4   | `getProperty`                         | Generics with `keyof` constraints |
| 5   | `Book` interface & `toggleReadStatus` | Interfaces & object spreading     |
| 6   | `Person` & `Student` classes          | Class inheritance                 |
| 7   | `getIntersection`                     | Set-based array intersection      |

## Blog Posts

- **blog-1.md** Why `any` is a type safety hole and how `unknown` with type narrowing is the safer choice
- **blog-2.md** How Generics enable reusable, strictly typed components and functions

## Running the Code

Compile and run the TypeScript file using ts-node:

```bash
npx ts-node solutions.ts
```

Or compile with the TypeScript compiler:

```bash
npx tsc solutions.ts
node solutions.js
```
