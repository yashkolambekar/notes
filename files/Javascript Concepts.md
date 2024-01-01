## Callbacks

Callbacks are the functions that are passed inside the functions which will execute once the main function is executed.

```js
const hello = (cb) = {
    console.log("What's up?")
    cb();
}

const bye = () = {
    console.log("See ya!")
}

hello(bye); 
```

The output of the `hello(bye)` is **What's up? See ya!**. First, the because hello function is run and then, the bye function is run. 

Callbacks can be useful for various purposes where we need to perform an action after the completion of the current function or process like reading a file, fetching data from api or some complex calculations. That is where callback functions are used.

Although callbacks are old, the new way to deal with such things are calle Promises

## Promises

Promises are used as alternatives to the Callback functions. Promises are way better than callback functions.

First we have to create a promise

```js
const check = new Promise((resolve, reject) => {

    const age = fetchAgeFromGovt()
    const credits = fetchCreditsFromBank()

    if(age > 18 && credits > 100){

        resolve({"license": "full"})

    }else if(age < 18){

        reject({"error": "Below 18"})

    }else{

        reject({"error": "Insufficient credits"})
        
    }
})
```

We have declared a promise above with the name check. We are imitating a loan approval system. Let's say it takes time for govt servers to fetch age and it takes even more time for credits to be fetched from the bank, so we will need to wait for those values to be fetched to do anything further. We can use callback functions, but here we will need a lot of them, this will create a callback hell. So we put it inside a promise.

```js
check.then((message) => {
    console.log(message)
}).catch((error) => {
    console.log(error)
})
```

we get the data back from the promise in the above way, once the promise has been fulfilled or rejected. It can be accessed through `.then()` and `.catch()` methods.

The code inside then is executed if promise is resolved, and the code inside catch is executed if the promise is rejected.

We also have `.finally()` method at the end which runs irrespective of resolve or reject. It should be run at the last.


## Async Await

