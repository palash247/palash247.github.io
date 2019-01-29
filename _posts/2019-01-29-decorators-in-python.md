---
layout: post
title:  "Decorators in Pyhton"
modified:   2019-01-29 23:00:19
excerpt: "Decorators in Pyhton"
categories: [python, programming]
comments: true
share: true
pinned: false
# image:
#     feature: https://raw.githubusercontent.com/palash247/palash247.github.io/master/img/rubik.png
#     credit: Andrew Martin
#     creditlink: https://pixabay.com/en/users/aitoff-388338/
---


## Decorators

Functions/Classes which takes other functions as input to adds extra functionality to them. Decorators usually wraps around the original function.

## Why use them?

1. Suppose you want add some common functionality in every function of your project. You can use a decorator to abstract the common code for this functionality and simply wrap it around the every function. This will save you from repeating your code.
2. To modify a function without touching the original code of the function.

## How to use them?

Their are, in general two ways to define the decorators, using a class and using a function, prior being least common way.

### Decorator function:
Here is the simple example of the decorator function.

~~~python
# Defining a decorator.
def decorator(original_function): # Decorator takes the original function as argument
    def wrapper(): # For now wrapper is not returning None
        print("EXTAAAAA FUNCTIONALITY!!!")
        original_function() # Original function gets called here.
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    return wrapper # Wrapper function is returned.

# Defining a function with limited functionality without annotating with the decorator.
def printer():
    print("I LOVE PRINTING!!")

# Another function with limited functionality with annotation.
# More common way of using decorators.
@decorator
def speaker():
    print("I LOVE SPEAKING!!")

# Another way of wrapping function within decorator.
printer = decorator(printer)
print()

# Calling modified printer with extra functionality.
printer()
print()

# Calling speaker
speaker()
print()

# Printing name of the functions
print(f'Function name is {speaker.__name__}')
print(f'Function name is {printer.__name__}')
~~~
~~~
# OUTPUT
EXTAAAAA FUNCTIONALITY!!!
I LOVE PRINTING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

EXTAAAAA FUNCTIONALITY!!!
I LOVE SPEAKING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

Function name is wrapper
Function name is wrapper

~~~

#### Observations:

1. Function `decorator` has taken a function `original_function` as input and wrapped it with other function defined inside it.
2. There are two ways to wrap a function, 1. by annotating it with the decorator's name (line 15-17) or 2. by directly calling the decorator with original function as input and then calling the returned function (line 19-24).
3. `printer` and `speaker` both has the extra functionality we intended to add.
4. `printer.__name__` and `speaker.__name__`  both has name `wrapper` which means the original functions did not retain their attributes. This can be fixed using a module in `functools` named `wraps` as follows. 

~~~python
from functools import wraps

# Defining a decorator.
def decorator(original_function): # Decorator takes the original function as argument
    # Using a  decorator inside decorators to preserve attributes of original function.
    # Notice we are passing the original function to the wraps.
    @wraps(original_function)
    def wrapper(): # For now wrappern is not returning None
        print("EXTAAAAA FUNCTIONALITY!!!")
        original_function() # Original function gets called here.
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    return wrapper # Wrapper function is returned.

@decorator
def speaker():
    print("I LOVE SPEAKING!!")

speaker()
print()
print(f'Function name is {speaker.__name__}')
~~~
~~~
EXTAAAAA FUNCTIONALITY!!!
I LOVE SPEAKING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

Function name is speaker
~~~

Now, what if our function had some arguments. Let's try same decorator on a function with arguments.

~~~python
@decorator
def adder(a, b):
    print(f'{a} + {b} = {a+b}')

adder(3, 4)
# OUTPUT
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
----> adder(3,4)

TypeError: wrapper() takes 0 positional arguments but 2 were given
~~~

This error makes sense because we are, in a way, calling the wrapper function and we have defined it to take 0 arguments. Let's modify it take any number of arguments.

~~~python
# Redefining our decorator
def decorator(original_function): 
    def wrapper(*args, **kwargs): # Receive any number of arguments
        print("EXTAAAAA FUNCTIONALITY!!!")
        original_function(*args, **kwargs) # Forward same arguments to the original function
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    return wrapper # Wrapper function is returned.

# Try executing functions with and without arguments.
@decorator
def adder(a, b):
    print(f'{a} + {b} = {a+b}')

@decorator
def printer():
    print("I LOVE PRINTING!!!")

# Call function with arguments
adder(3, 4)

# Call function without  arguments
printer()

# OUTPUT:
~~~
~~~
EXTAAAAA FUNCTIONALITY!!!
3 + 4 = 7
AGAIN EXTAAAAA FUNCTIONALITY!!!
EXTAAAAA FUNCTIONALITY!!!
I LOVE PRINTING!!!
AGAIN EXTAAAAA FUNCTIONALITY!!!
~~~

Now let's try making same decorator using a class. The trick is to overwrite the `__call__` method of the decorator class with the wrapper function of your choice. `__call__` method allows the class's instance to be called as a function.

### Decorator class

~~~python
class decorator(object):
    def __init__(self, original_func):
        self.original_func = original_func

    def __call__(self, *args, **kwargs):
        print("EXTAAAAA FUNCTIONALITY!!!")
        self.original_func(*args, **kwargs) # Forward same arguments to the original function
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")

@decorator
def adder(a, b):
    print(f'{a} + {b} = {a+b}')

adder(2, 3)

# OUTPUT:
EXTAAAAA FUNCTIONALITY!!!
2 + 3 = 5
AGAIN EXTAAAAA FUNCTIONALITY!!!

~~~

Let's do something useful now. We will write a decorator which when wrapped around a function, logs the function call in a log file named after the function name itself.

~~~python
def func_logger(func):
    import logging
    FORMAT = '%(levelname)s %(asctime)s %(message)s'
    logging.basicConfig(
        format=FORMAT,filename=f'{func.__name__}.log',
        level=logging.INFO
        )
    def wrapper(*args, **kwargs):
        logging.info(f'Function called: {func.__name__}, with parameters: {args}')
        return func(*args, **kwargs)
    return wrapper

@func_logger
def adder(a, b):
    return a+b

result = adder(6,7)
~~~
~~~
# Contents of adder.log
INFO 2019-01-29 22:45:30,860 Function called: adder, with parameters: (6, 7)
~~~

If you find any mistake in above code please comment down below I'll be happy to fix it immediately.