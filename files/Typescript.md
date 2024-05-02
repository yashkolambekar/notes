# Typescript

### TypeScript is all about being Strict, so be as strict as you can!

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

### readonly

In the object type, we have option to make the values readonly, which means they cannot be modified once they are defined, to do this, we do

```ts
type User = {
  name: string;
  email: string;
  readonly id: number;
};
```

The above code absolutely works as expected and the `user.id` property is readonly, attempts to modify it throws an error.

### optional

In the object type, we might not require a certain value from all the objects, it is an optional value, and we are provided a method to do that in typescript, we just have to add a `?` as suffix to the key and it becomes optional

```ts
type User = {
  name: string;
  email: string;
  creditCardNumber?: number;
};
```

## Array in TS

An empty array by default has the type of `never` which means we cannot push anything inside and it is not a good thing

to give it the array of type, we have to give it the type of `[]`, yes, it's just close brackets

```ts
const emptyArray : [] = [];
```

Now, we still cannot push anything in this array because it is an empty array and it is supposed to be empty forever, to create arrays that can accept values, we have to prefix the type with the array's items' type

```ts
const rollNumbers = number[] = [];
rollNumbers.push(15);
```

The above code is correct and works absolutely fine, rollNumbers is an array of numbers, it accepts only numbers


```ts
const superHero : [number, string][] = []
superHero.push([12, "Yash"]);
```

The above code also is valid as it defines an array of arrays in which the child array has two children which are number and string respectively

We can have a alias type too

```ts
const allUsers = User[] = [];
```

## Multiple datatypes or Union

```ts
const score : number | string = 44;
```

We use this pipe `|` operator to specify that we want type a OR type b, we can also specify alias or custom types in this manner


```ts
const yash : User | Admin = {};
```

#### To have multiple data types in Arrays

- All items with same datatype

  ```ts
  const arr = number[] | string[] = [1, 2, 4, 5, 6];
  ```

  The above array can be an array of strings or an array of numbers but it cannot have both at the same time

- All items Different datatypes 
  
  ```ts
  const arr = (number | string)[] = [1, 2, 4, "45"];
  ```

  In this example, the array can have a mix of both numbers and strings.

## Tuples

```ts
const rgb : [number, number, number] = [255, 255, 255];
```

The above code will only take 3 elements all the three will be numbers.

```ts
const user : [number, string, boolean] = [19, "Yash", true];
```

The above code, as expected accepts 3 elements in the string of the given type

We can add an optional element(s) in there too but it has to come in last, no required element should come after the optional element and also, we cannot skip optional elements, if we have three optional elements `string?, number?, boolean?` and we want to utilise the number element, we have to give the string element in that case before going to the number or we cannot use it

## Enums

Enums can be used when we have to give limited choice to the user regarding a particular thing, we can use it like

```ts
enum seatChoice {
    AISLE,
    MIDDLE,
    WINDOW
}
const yashSeat = seatChoice.MIDDLE;
console.log(yashSeat); // returns 1
```

We can also specify custom values for the choices :

```ts
enum seatChoice {
    AISLE = "valid",
    MIDDLE = 0,
    WINDOW
}
const yashSeat = seatChoice.MIDDLE;
console.log(yashSeat); // returns 0
```

We can also do `const enum ....` if we do not want any crazy js code in the compiled file


# Video tutorial 

https://youtu.be/30LWjhZzg50?si=Pfw8Pe0JI8ogSbrP&t=8643
Start with interface