# TypeScript Cheat Sheet
Cheat Sheet for TypeScript. Please file an issue if you encounter a problem and PR always welcome.

### Table of Contents

<details>

<summary><b>Expand Table of Contents</b></summary>

- [Section 1: Setup](#section-1-setup)
- [Section 2: Data Types](#section-2-data-types)
  - [String, Number, Array, Boolean](#string-number-array-boolean)
  - [Tuples](#tuples)
  - [Enum](#enum)
  - [Union](#union)
  - [Any](#any)
  - [Void](#void)
- [Section 3: Interface](#section-3-interface)
- [Section 4: Type Alias](#section-4-type-alias)

</details>
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

function getValue(): any {
  return "Developer";
}
```

## Void 

This is usefull when you are not returning anything from the function(this is not mandatory to include).

```ts
function getError(): void {
  console.log("TypeScript is a SuperSet of JavaScript");
}
```

# Section 3: Interface

An Interface is a group of properties and methods that describe an object but neither does initialization nor implementation.

```ts
interface User {
  name: string;
  age: number;
  getPoints(point: number): number;
}

let user: User = {
  name: "John Doe",
  age: 25,
  getPoints(point: number): number {
    return point * point;
  }
}
```

We can make properties and parameters optional.

```ts
interface User {
  name?: string;
  age: number;
  getPoints(point?: number): number;
}

let user: User = {
  age: 25,
  getPoints(): number {
    return 5 * 5;
  }
}
```

# Section 4: Type Alias

Type Alias creates a new name for a type.

```ts
type GetArea = (width: number, height: number) => number;

interface Rectangle {
  getArea: GetArea;
}

let rectangle: Rectangle = {
  getArea(width: number, height: number): number {
    return width * height;
  }
}
```

> Aliasing doesn’t actually create a new type - it creates a new name to refer to that type. Aliasing a primitive is not terribly useful, though it can be used as a form of documentation.

# Section 5: Class

Just like the other language TypeScript has a class feature. 

```ts
class Product {
  name: string;
  price: number;

  constructor(name: string, price: number) {
    this.name = name;
    this.price = price;
  }

  getTotalPrice(discount: number): number {
    return this.price - discount;
  }
}

const product = new Product("Milk", 250);
```

We can add interface for product class.

```ts
interface IProduct {
  name: string;
  price: number;
  getTotalPrice(discount: number): number
}

class Product implements IProduct {
  name: string;
  price: number;

  constructor(name: string, price: number) {
    this.name = name;
    this.price = price;
  }

  getTotalPrice(discount: number): number {
    return this.price - discount;
  }
}

const product = new Product("Milk", 250);
```

# Section 6 - Type Guards

In order to find specific type when we use union types, we can use the Type Guard. `typeof`, `instanceof`, `in` are the example of Type Guards.

```ts
// typeof
function showMessage(message: string | object): void {
  if(typeof message === 'string') {
    console.log("The type is string");
  } else if(typeof message === 'object') {
    console.log("The type is object");
  }
}

showMessage({ name: "John Doe" });
```

```ts
// instanceof
class User {
  id: number;
}

class Product {
  name: string;
}

function showMessage(message: User | Product): void {
  if(message instanceof User) {
    console.log("Message is an instance of User");
  } else if(message instanceof Product) {
    console.log("Message is an instance of Product");
  }
}

showMessage(new User());
```