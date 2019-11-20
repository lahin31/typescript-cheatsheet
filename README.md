# TypeScript Cheatsheet
Cheatsheet for TypeScript. Please make an issue if you encounter a problem and PR always welcome.

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
  - [Unknown](#unknown)
  - [Void](#void)
  - [Never](#never)
- [Section 3: Interface](#section-3-interface)
- [Section 4: Type Alias](#section-4-type-alias)
- [Section 5: Class](#section-5-class)
- [Section 6: Generics](#section-6-generics)
- [Section 7: Symbol](#section-7-symbol)
- [Section 8: Keyof & Indexed Access Types](#section-8-keyof-and-indexed-access-types)
- [Section 9: Mapped Types](#section-9-mapped-types)
- [Section 10: Type Guards](#section-10-type-guards)

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

## Unknown

`unknown` is the type-safe counterpart of `any`. Anything is assignable to `unknown`, but `unknown` isn’t assignable to anything but itself.

```ts
let value: unknown;

value.trim();   // Error
value();        // Error
new value();    // Error
```

## Void 

This is useful when you are not returning anything from the function(this is not mandatory to include).

```ts
function getError(): void {
  console.log("TypeScript is a SuperSet of JavaScript");
}
```

## Never

Use `never` when a function doesn't return anything. This can be used when a function returns error.

```ts
function error(message: string): never {
    throw new Error(message);
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

We can add interface for Product class.

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

# Section 6: Generics

We can specifically pass the type to any function but what if when we don't know the type to pass, Generic can help us.

```ts
// Generic Function
function removeItem<T>(arr: Array<T>, item: T): Array<T> {
  let index = arr.findIndex(i => i === item);
  arr.splice(index, 1);
  return arr;
}

console.log(removeItem([1, 2, 3], 2));
console.log(removeItem(['John', 'Michael'], 'John'));
```

```ts
// Generic Class
class Country {
  protected countryName: string;

  constructor(countryName: string) {
    this.countryName = countryName;
  }

  getName() {
    return this.countryName;
  }
}

class Australia extends Country { }
class England extends Country { }

let australia = new Australia('Australia');
let england = new England('England');

function getName<T>(country: T): T {
  return country;
}

console.log(getName(australia));
console.log(getName(england));
```

# Section 7: Symbol

Symbol is a primitive data type, which is also immutable and unique.

```ts
let sym1 = Symbol("key");
let sym2 = Symbol("key");

sym1 === sym2; // false
```

# Section 8: Keyof & Indexed Access Types

In TypeScript `keyof` operator extracts the set of keys for a given type.

```ts
interface IUser {
  name: string;
  age: number;
}

type UserKeys = keyof IUser; // "name" | "age"
```

Using the `keyof` operator we can do Indexed Access Types. The key parameter can get the type of each key of obj.

```ts
function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = {
  id: 1,
  name: "John Doe"
}

console.log(getValue(user, "id")) // 1
```

# Section 9: Mapped Types

In TypeScript Mapped Types allow us to create new types from existing types.

```ts
interface Person {
  name: string;
  age: number;
}

type readonlyPerson = {
  readonly [P in keyof Person]: Person[p]
}
```

# Section 10: Type Guards

In order to find specific type when we use union types, we can use the Type Guard. `typeof`, `instanceof`, `in` are the examples of Type Guard.

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