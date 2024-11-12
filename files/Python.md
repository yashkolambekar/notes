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