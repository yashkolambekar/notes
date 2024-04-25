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

