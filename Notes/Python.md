# Python

Python.

## Multithreading

To use multithreading, we import the threading module from the standard library

```py
import threading
```

### Creating a thread

We have to first create a thread using the `Thread` constructor from the multithreading module. This will return a thread.

```py
thread1 = multithreading.Thread(target=function_that_takes_time)
```

### Starting the Thread

The thread created from the Constructor is not started, it's just intiliased, to start the thread we have to 

```py
thread1.start()
```

### Joining the threads

The app will move on with the execution while the threads are running in the background, if we want the threads to complete processing before moving on with the app at a particular point, we can use the `join` method, we will wait for the thread to complete, and only then proceed further from there

```py
# code here does not depends on threads
thread1.join()
thread2.join()
thread3.join()
#code here depends on threads' output
```

### Executing functions with arguments

If your function has arguments, like `send_email(email_id)` we can execute them with args

```py
thread1 = multithreading.Thread(target=send_email, args=("example@email.com",))
```

### Checking number of active threads

```py
threading.active_count()
```

This function returns the number of active threads, by default there is one thread running the main file, and the threads we add afterwards are added in that count


### OOP way of creating threads

We can create our custom threads with the help of Thread class, we inherit that class and add our code as per our choice


```py
import threading
from time import sleep

class MyThread(threading.Thread):

    def __init__(self):
        super().__init__()

    def run(self):
        print("A thread is running")
        sleep(3)
        print("Thread exited")

mt = MyThread()
mt.start()
```

If we want to have parameters in the threads which we will create with the help of classes, we have to define them in the `__init__` class after the self and we can access them in the whole class using `self.param_name`

### Parameters for the Thread constructor function

- `name`: Name of the thread, if not given, is given automatically


### Thread Identity

The `ident` property of the thread is given by python to each thread and it exists even after the thread has exited, it is not given to the thread until and unless the thread is started.

So with the combination of `ident` and `is_alive()` we can differntiate between stopped threads, active threads and threads which were never started.


### Thread locking

We can create a lock which will be a object of type `Lock` from the threading module and then we can use it with threads. What will happen with this, is, we can queue the threads, a lock can be acquired by only on thread at once and has to be released before the other thread can use it.

We can use `lock.acquire()` and `lock.release()` methods to do the respective things. This will help us queue the 

```py
import threading
from time import sleep

sql_lock = threading.Lock()

def run_sql_query(lock, query_number):
    lock.acquire()
    print(f"Running sql query {query_number}")
    sleep(2)    
    print(f"Done executing sql query {query_number}")
    lock.release()

for i in range(10):
    t = threading.Thread(target=run_sql_query, args=(sql_lock, i))
    t.start()
```


## Concurrent.futures

```py
import concurrent.futures as cf
```

































<details>
<summary> 
Multiprocessing
</summary>


## Multiprocessing

In Python Multiprocessing is used to initiate multiple cpu intensive jobs that are going to run in the background, multithreading cannot be used in cpu intensive jobs as it is locked to use 100% cpu (one core) but multiprocessing can go beyound 100%

__Multiprocessing is independent of Global Interprer Lock__

The api of multiprocessing is similar to multithreading

```py
immport multiprocessing as mp
```

### Creating a process

```py
mp.Process(target=func_that_takes_cpu_and_time)
```

</details>