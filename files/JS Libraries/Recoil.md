# Recoil 

```shell
npm i recoil
```

An **Atom** is the smallest data point in a recoil store, it is like a state variable. If we use recoil, we will get rid of the state olympics that we were doing with useState passing it here and there endlessly.

### Folder Structure

we have a `/store` folder in the `/src` folder or anywhere else. And we have `/atoms` folder inside the store folder which contains individual js files for each atom.

For example, `/src/store/atoms/Count.js` looks like

```js
import {atom} from "recoil";

const countAtom = atom({
    key: "countAtom",
    default: 100
});

export default countAtom;
```

We also have to wrap our app in the `<RecoilProvider>` component to enable us to use this library in our app.

## APIs / Functions

To define an atom, we use the `atom` function which is provided by the recoil library. It requires an object as an argument which contains `key` and `default` key-value pairs to initialise the atom. We already saw the example above

### useRecoilValue

This function is used to get the value of that particular atom in the component, this is a readonly value.

```jsx
import { useRecoilValue } from "recoil";
import countAtom from "../store/atoms/count";
...
const count = useRecoilValue(countAtom);
...
```

it takes the exported atom as an argument

### useSetRecoilState

```jsx
import { useSetRecoilState } from "recoil";
import countAtom from "../store/atoms/count";
...
const setCount = useSetRecoilState(countAtom);
...
```

This function is used to update the state/atom. We cannot read the value, this might come handy when we have to set the value of atom from user input or some other external source.


### useRecoilState

```jsx
import { useRecoilState } from "recoil";
import countAtom from "../store/atoms/count";
...
const [count, setCount] = useRecoilState(countAtom);
```

useRecoilState is just like useState and works similarly, it should be used only when we need both value and a function to update the value, it is heavier than the first 2

### selector
