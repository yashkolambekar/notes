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