# TypeScript Cheat Sheet
Cheat Sheet for TypeScript. Please file an issue if you encounter a problem and PR always welcome.

<summary><b>Expand Table of Contents</b></summary>

- [Section 1: Setup](#section-1-setup)
- [Section 2: Data Types](#section-2-data-types)
  - [String, Number, Array, Boolean](#string-number-array-boolean)
  - [Tuples](#tuples)
  - [Enum](#enum)
  - [Union](#union)
  - [Any](#any)
  - [Void](#void)

# Section 1: Setup

1) Go to [TypeScript](https://www.typescriptlang.org) download from there or just type `npm install -g typescript`.
2) Check the installed version `tsc -v`.

# Section 2: Data Types

## String, Number, Array, Boolean

There are some basic types available for TypeScript. Such as `string`, `number`, `Array<number>`, `string[]`, boolean etc. We can do Type Declaration by them.

```ts
let x: number = 5;
let name: string = "John Doe";
let showErrorMsg: boolean = true;
let numbers: Array<number> = [1, 2, 3]
let students: Array<string> = ["John Doe", "Michael"];

function showDetail(name: string, age: number): void {
  console.log(name);
}
```

## Tuples

This is something new in TypeScript 3. A Tuple is an array but the number of elements are fixed.

```ts
let product: [string, number];
product = ["John", 10];

let val: [string, ...number[]]
val = ['John', 5, 7, 9]
```

## Enum

Enum allows us to declare a set of collection in which we can assign them a perticular value such number, string by default TS compiler will assign them in number.

```ts
enum ProgrammingLanguage {
  javascript,
  python,
  php
}

// This will be changed as

enum ProgrammingLanguage {
  javascript = 0,
  python = 1,
  php = 2
}
```

## Union

TypeScript allows us to assign more than one data type for a variable or for a function.

```ts
let address: string | number;
address = "New York"
// or
address = 3100;

function getValue(): string | number {
  return "John Doe";
  // or
  return 123;
}
```

## Any

If you don't know the actual data type or you don't want to assign a data type you can use `any`.

```ts
let detail: any;
detail = "Developer";
// or
detail = 45;

function getValue(): any {
  return "Developer";
  // or
  return 45;
}
```

## Void 

This is usefull when you are not returning something from a function, which is not mandatory.

```ts
function getError(): void {
  console.log("TypeScript is a SuperSet of JavaScript");
}
```