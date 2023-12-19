to start using Axios we have to first install it using npm

```console
npm install axios
```

and then we have to import it in our React app

```js
import axios from "axios"
```

The biggest mistake I do while writing the word Axios is, I write it as axious, so dear self please remember the correct name


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

When we need to use axios synchronously, we use them with the help of `IIFE` which stands form Immediately Invoked Function Expression. These look something like

```js
;()();
```

yes, that thing right there is a valid javascript expression and it is not only a valid javascript expression. It is quite useful in many cases

The first `;` is to end all the previous statements that might have not been terminated. The first `()` is where we define the function and then `()` is where we call the function and the second `;` ends it all.

We will use these to enable use to use `async await` in our axios functions

For example

```js
;(async () => {
      const response = await axios.get("/api/products");
      setProducts(response.data)
  })();
```

We are escaping the use of `then` and `catch` here. We are storing the response in the response variable and then directly using it in the next line.

But that does not mean we have to compromise on the error handling, we can use `try catch` to do that

```js
;(async () => {
      try {
        const response = await axios.get("/api/productsd");
        console.log(response.data);
        setProducts(response.data)
      } catch (error) {
        // Handle the axios error
      }
    })();
```

In the above example, we will handle the error perfectly while our whole axios function is now synchronous.