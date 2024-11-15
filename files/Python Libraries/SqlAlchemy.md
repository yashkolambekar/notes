# SQL Alchemy

## Installation

```shell
pip install sqlalchemy
```

## Initialisation

We create the engine and Models (Tables) in a seperate file, the Models are declared here and are exported from here, if we many any changes in the model and the table for that model already exists, the table won't be changed and if we try to insert anything, it will throw an error

```py
from sqlalchemy import create_engine
from sqlalchemy.orm import declarative_base

db_url = "dbtype+driver://username@password@host:port/database"
engine = create_engine(db_url)

Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True)
    name = Column(String(length=100))
    age = Column(Integer)

Base.metadata.create_all(engine)
```

## Inserting data

```py
from db import User, engine
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()

user = User(name="John Doe", age=30)

session.add(user)
session.commit()
```

We first make a session using the `sessionmaker` and then create a new user using the User model, we then have to add it to the session and then commit the session to save all the changes

We can also use `add_all` and provide it with an array of objects

```py
session.add_all([user_1, user_2])
```


## Getting data

#### Get all the records

```
users = session.query(User).all()
```

This returns a list of Objects that we can access, although the object is not accessible in a dictionary format, but we can use the `.` notation to get the properties

```py
users = session.query(User).all()

for user in users:
    print(user.name)
```

#### Filter the records

```py
user = session.query(User).filter_by(id=1).all()
```
Returns a list of objects that match the parameter, and an empty list if no objects are found

```py
user = session.query(User).filter_by(id=1).one_or_none()
```

Returns single object or `None` if it is not found. But if there are multiple objects that match this, it will return an error. So use this one only when you are sure that there is only one row that fulfills the requirement


```py
user = session.query(User).filter_by(age=12).first()
```

Returns the first object or returns none

#### Order / Sort

```py
user = session.query(User).order_by(User.age).all() #asc
rev_user = session.query(User).order_by(User.age.desc()).all() #desc
```

#### Multiple sorting options

Here, in this one, if we get multiple users with same age, they will be then sorted according to their id

```py
user = session.query(User).order_by(User.age, User.id).all()
```

### More filtering

If we want to 

```py
adult_users = session.query(User).filter(User.age >= 18).all()
```

If we want AND, multiple queries

```py
adult_users = session.query(User).filter(User.age >= 18, User.name="Yash").all()
```

We can also have `.where()` method, it is same

```py
adult_users = session.query(User).where(User.age >= 18).all()
```

We can also have `or` operator

```py
users = session.query(User).where(or_(User.age >= 18, User.name="Yash")).all()
```