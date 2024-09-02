# Javascript

Javascript is a loosely typed and compiled-on-runtime language.

## Callback functions

A function which is passed as an argument in a function is called a callback function

for example :

```js
function sum(num1, num2, functionToCall){
    let result = num1 + num2;
    functionToCall(result)
}

function displayResult(data) {
    console.log("Result of the sum is : " + data);
}

function displayResultPassive(data) {
    console.log("Sum's result is : " + data);
}

sum(12, 20, displayResult)
```

Here, we passed `displayResult` as an argument to the function `sum()` and `sum()` used that inside itself. We could have passed anything that we like, and processed the `result` variable as per our convenience

## Classes

Classes are blueprints to create objects which are instances of the classes with attributes and functions. Useful when creating similar objects repeatedly with little changes.

```js
class Animal {
    constructor(name, legCount, speaks){
        this.name = name;
        this.legCount = legCount;
        this.speaks = speaks;
    }
    speak(){
        console.log(`${this.name} is saying ${this.speaks}`)
    }
    static myType(){
        console.log("I am an Animal")
    }
}

const dog = new Animal("Tommy", 4,"Bhow bhow");
const cat = new Animal("Mani", 4, "Meooowwww")

dog.speak()
cat.speak()
```

In the above code, the `Animal` is a class which we can use to create objects. 

`dog` and `cat` are objects created using `new Animal()`, we also passed some parameters inside each.

Those parameters are used in the `constructor()` to give some properties to the object when it was created.

`myType` is a static method, which means it stays same for all the objects / instances of the class and on top of that it can be run directly by calling `Animal.myType()`, other methods need an object to run but static methods can run without initalising them into an object.

## Promises

Promises are syntactical sugar that make the Async code with callback functions prettier

**The promise is returned synchronously and is resolved asynchronusly**


```js
function readBook(){
    return new Promise(function(resolve){
        ...
        ...
        resolve(data);
    })
}
```

A promise must have the first argument function and the function needs to have the first argument resolve (can be named anything)

## Async Await

Async Await makes the Promises even more beautiful by eliminating the need of using .then() and rather let's you store the returned data directly in a variable

We are still using promises, just the .then() is replaced by async and await

```js
function someAsyncFunction(){
    return new Promise(resolve => {
        setTimeout(() => {
            resolve("Hello ji")
        }, 1000)
    })
}

async function main(){
    const message = await someAsyncFunction();
    console.log(message);
}

main();
```

As we can see, we are waiting till the promise is resolved and then directly using the value returned from the promise.


## Other Small things

### Map vs ForEach

Map and ForEach array methods are quite alike, the only difference being, The returned elements in the `.map()` are stored in the new returned array and `.forEach()` just performs some action on each element and does not return anything, both have similar syntax

```js
arr.forEach(item => {
    console.log(item + 99);
})
// Logs each element + 99, does not return anything

arr.map(item => {
    return item + 99;
})
// Returns new array with 99 added to each element
```