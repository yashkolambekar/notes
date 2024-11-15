# Fast API

FastAPI framework, high performance, easy to learn, fast to code, ready for production


```shell
pip install "fastapi[standard]"
```

## Running the app

```py
from FastAPI import fastapi
app = FastAPI()

@app.get("/")
async def root():
    return {"message":"Hello World"}
```

We can also use a normal function instead of a async function

To return we can return a dict, list, singular values as str, int, etc.

This is the most basic FastAPI app, the starter template, to run it we have to run this in the shell

```shell
fastapi serve main.py
```

## Parameters

We can have parameters in the path using the same syntax as for the python formatted strings

```py
@app.get("/print/{print_string}")
def print_string(print_string: str):
    return {"Your message": print_string}
```

### Dynamic routes should be at the end if conflicting

If we have two routes `/user/me` and `/user/{username}` then, we should keep the `user/me` first so that the interpreter finds it first and executes it or else we will be searching for a user with the username me

### Using Enums

```py
from enum import Enum
from fastapi import FastAPI
app = FastAPI()

class Actions(str, Enum):
    follow = "follow"
    unfollow = "unfollow"
    restrict = "restrict"

@app.get("/action/{action_name}")
def perform(action_name: Actions):
    # your code here
```

This way we can only allow certain values in our paths and everything else will throw errors


## Query Parameters

If we add the parameters to the function under our decorator without mentioning them in the path parmeters, they are treated as query parameters, we have to define the default value for them, or we can set them as optional params if we set the default value to None.

```py
@app.get("/search")
def search(college: str, rank: int | None = None):
    return {"college": college, "id": id}
```