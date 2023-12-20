Mongo is a NoSQL database used for storage, processing and retrieval of data. Mongo is a non-relational database. The data in Mongo is stored in the form of Javascript Objects

To use mongodb with our node app we need to install `mongoose`

```console
npm install mongoose
```

We need to first import the JS module

```js
const mongoose = require('mongoose')
```

And we need to define our mongodb url 

```js
const url = `mongodb+srv://${username}:${password@cluster0.o1opl.mongodb.net/${collection_name}?retryWrites=true&w=majority`
```

we will get this link from our mongodb host such as Atlas (official mongodb)

```js
mongoose.connect(url)
```

First we connect mongoose using the url

```js
const noteSchema = new mongoose.Schema({
  content: String,
  important: Boolean,
})
```

We make a new schema named `noteSchema` using the `mongoose.Schema` method, this will be used to define our schema which we can use to make new objects

```js
const Note = mongoose.model('Note', noteSchema)
```

after that we can make a new `note` object using the `Note` model

```js
const note = new Note({
  content: 'HTML is Easy',
  important: false,
})
```

After we have entered the dat in the note object, we can save the object in our database.

```js
note.save().then(result => {
  console.log('note saved!')
})
```