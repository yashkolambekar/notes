# Typescript

Typescript is a superset of Javascript which adds typesafety on top of Javascript. In a way, making Javascript a compiled language.

## Installation

```shell
npm i typescript --save-dev
```

## Export

```shell
tsc filename.ts
```

this creates a file named filename.js in the same directory

## Types

- **string**
- **number**

  Number can be a integer or a float, negative or positive.

- **boolean**

- **null**
- **undefined**
- **void**

- **object**
- **array**
- **tuples**
- **...**

- **any (do not use)**
- **never**
- **unkown**

## Syntax

To declare a variable with a type

```ts
let variableName: type = value;
```

### Type Inference

At some places we do not have to specify a type for our variable where it is obvious

```ts
let userId = 123;
```

In the above example, the typescript automatically assigns the type (number) to the variable `userId` and we do not have to specify it, everything will work normally.

### Functions in TS

```ts
const addTenToNumber = (val: number) => {
  return val + 10;
};
```

We have to define the expected class of the parameter as well.

```ts
const addTenToNumber = (val: number = 13) => {
  return val + 10;
};
```

In the above function we are defining the type to the parameter and on top of that, we are giving a default value for the parameter.

But in this case, we can rely on type inference, `(val = 13)` will also work the same and the type will be infered by the the typescript engine

#### Taking in objects as parameter

```ts
const createUser = ({name: string, age: number}) : boolean {
  return true;
}
createUser({name: "Yash", age: 19});
```

### Types on the returned values

To define the type of the returned value, we can add the type anotation after the parameters colon

```ts
const greet = (): string => {
  return "Hello";
};
```

The above function returns a string.

We also apply this in functions such as map

```ts
const arr = [1, 2, 3, 4, 5, 6];

arr.map((item): string => {
  return `This is ${item}`;
});
```

In this function, we have defined that, the items that will returned after each loop will be of type string.

- #### Functions that return nothing

  While defining functions, we may create functions that do not return any thing, in that scenario, typescript defines the type of returned value as `void` which means it does not return anything. We will use the same

  ```ts
  const printThis = (msg: string): void => {
    console.log(msg);
  };
  ```

- #### Functions that do not end / crash the program

  Many a times we need functions that do not end or throw an error, after which the program stops working, what type of return type do we define for it? Because these functions never end, we use `never` as an type to define such functions.

  ```ts
  const errorPrint = (msg: string): never => {
    throw new Error("msg");
  };
  ```

- #### Functions that return object

  ```ts
  const createUser = () : {name: string, price: number} {
    return {name: "Python", price: 1192}
  }
  ```

## Type alias

We can create alias names for our types as per our liking

```ts
type bool = boolean;
type s = str;
type v = void;
```

We generally do not use it for such purposes, we rather use the alias to define type of complex objects that we are going to use in the app

For example,

```ts
type User = {
  name: string;
  age: number;
  isPaid: boolean;
};

function createUser(user: User) : boolean {
  ...
}
```



