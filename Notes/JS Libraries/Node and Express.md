# Express

to start a node project at a given directory, we have to do
```console
npm init
```

and then our project is initialised, we start by creating a js file such as `server.js` or `index.js`, the nomenclature depends on your understanding, and then we can run it whenever we want using

```console
node index.js
```

although it is very important that we run this command from npm scripts so we go to `package.json` file and we add the `node index.js` script in the scripts object with the name `start`, you can name it whatever you want, so now all we have to do is

```console
npm start
```

and our project will be running!

We do not use node directly to do the server stuff in real world, we use libraries on top of it to make our work easier. One such very famous and very useful library is **Express**

We will be using express for our server side applications in the MERN. So it is very important to learn Express.

To use express, we first install it using npm

```console
npm i express
```

To start using express in our application we have to import it first

```js
const express = require("express");
const app = express()
```

and we also make an instance of it under the app constant, so now we will use app and it's methods

we have to make the app listen at a port using `app.listen()` method 

```js
const PORT = 3001
app.listen(PORT, () => {
    console.log(`Server running on PORT ${3001}`);
})
```

This code will make the app listen and then print the message once the server starts listening, this will be done at the **last lines** of the js file.

before that we need to make the paths or routes for the user to access using `app.get()` method

```js
app.get("/", (req, res) => {
    res.send("<h1>Hello world</h1>");
})
```

So now, when the user visits `localhost:3001` they will see Hello world

```js
app.get("/api/notes", (req, res) => {
    res.json(notes)
})
```

when, the user will go to `localhost:3001/api/notes` they will see a json object being output there. This is how we make routes in express.

We can also accept dynamic route names by using the `params` feature of express. 

```js
app.get("/api/notes/:id", (request, response) => {
  const id = Number(request.params.id);
  const note = notes.find((note) => note.id === id);
  response.json(note);
});
```

As you can see here, we are taking one additional route in the url with alias name `id` we have added a semicolon in front of that to identify it as an param, so now if someone visits **localhost:30001/api/notes/1**, we can find the note with id 1 using js and return only that single note

We can access the params using `request.paramas.<param name>`


## Middlewares

Middlewares are the logic classes that check for the validity of the inputs that come with the requests, this is done before the input is processed by the business logic


```js
app.get("/login", (req, res) => {

    // middleware here

    // business logic here
})
```

If the middleware checks are failed, we early return with an error.

### How to define Middlewares?

We can add middlewars in our route requests just before the function that does the business logic, for example


```js
app.get("/", function1, function2, function3);
```

the function1 and function2 can be middlewares and function3 can be the final function which will contain the business logic


```js
const function1 = (req, res, next) => {
    if(!someThingLogicalhere){
        res.send("Some error occurred");
        return;
    }
    next();
}
```

Doing `next()` will send the control to the next function, if we do not use it, the request will be hung and will time out.

We can also make a controller be applied to every route of our app by using `.use()`

```js
app.use(counterMiddleware);
```

### Error handling Middleware

A global catching function

```js
app.use((err, req, res, next) => {
    if(err){
        res.send("Some error occured");
    }
})
```

We have to add it in the last, at the end of our app.

## Zod

`zod` is a node package used for input validation


```js
const kidneysSchema = zod.array(zod.number());
return kidneySchema.safeToParse('Yash', 1);
```

This will return an error with detailed information.
