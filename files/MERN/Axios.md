### Axios

Axios is a module for http requests, this module reduces the hustle, bustle that goes behind making http requsts

To install it we have to run

```console
npm install axios
```

Axios works on the basis of javascript promises, for example, to make a simple get request we can do

```jsx
const promise = axios.get("http://localhost:3001/notes");
promise.then((response) => {
  console.log(response);
});
```

However we do not handle promises in this way, we use `then` and `catch`

```jsx
axios.get("http://localhost:3001/notes").then((response) => {
  const notes = response.data;
  console.log(notes);
});
```

Put method in http

```jsx
axios.put(url, changedNote).then((response) => {
  setNotes(notes.map((n) => (n.id !== id ? n : response.data)));
});
```

This method, name `put` changes the value of an object in the server.

<br>

We can isolate the axios functions in a different module and make the usage of axios more easier according to our webapp. Example: 

```js
const getAll = () => {
    const request = axios.get(baseUrl);
    return request.then(response => response.data)
}
```

So now in our main app we can just do 
```js
services.getAll().then(data => {console.log(data)})
```

this saves us a lot of boiler plate code in our main app