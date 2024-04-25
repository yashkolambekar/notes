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

Then we need to create a Schema using `mongoose.Schema`, that method takes in an object and then we have to save that schema in a new constant

```js
const userSchema = new mongoose.Schema({
    name: String,
    age: Number,
    location: String
})
```

then we have to make a model using that Schema
using `mongoose.model`

```js
module.exports = mongoose.model("User", userSchema)
```

To create a new user in the database, we can do

```js
User.create({name: "Something", age: 18, location: "Mumbai"})
```

it will return a new user object, we can save it in a new object

```js
const yash = User.create({name: "Something", age: 18, location: "Mumbai"})
```

If we need to edit some detail in the created object, we can edit it directly 

```js
yash.location = "Bharat";
yash.save()
```

`.save()` and `.create()` are asynchronous functions, so we might want to use them inside function with `async await` to get proper callbacks

We can specify more properties in the Schema by using Objects as input. For example

```js
age : {
    type: Number,
    required: true,
    default: 18,
    min:1,
    max: 150
}
```

There are other flags too which can be used

```js
{
    lowercase: true,
    uppercase: true,
}
```

We can also write custom validation with validate key

```js
{
    ...
    validate: {
        validator: value => value % 2 == 0,
        message: props => `${props.value} is not even`
    }
    ...
}
```

`validator` is a function with `value` as a parameter which we test for some checks and return true if we want to keep it and false if it is invalid

`message` is the function that returns the message which should be printed in the console with props as a object being sent as a parameter

**Important**: Functions such as `findOneAndUpdate` and `findManyAndUpdate` do not go through validations, so we should refrain from using them, we should rather find our items with `.findById` or `.find` and then edit them and the do `.save()` to go through the validation checks.

Some methods and how they work

`findById`: returns one object which matches the id

`find`: returns an array of all the objects that match

`findOne`: returns the first object that matches the condition