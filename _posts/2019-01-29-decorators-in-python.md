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

Decorators are the Functions/Classes which takes other functions as input to add extra functionality to them. Decorators usually wrap around the original function.

## Why use them?

1. Suppose you want to add some common functionality in every function of your project. You can use a decorator to abstract the common code for this functionality and simply wrap it around every function. This will save you from repeating your code.
2. To modify a function without touching the original code of the function.

## How to use them?

There are, in general, two ways to define the decorators, using a class and using a function, prior being a least common way.

### Decorator function:
Here is the simple example of the decorator function.

~~~python
# Defining a decorator.
# Decorator takes the original function as argument
def decorator(original_function):
    # For now wrapper is not returning None
    def wrapper():
        print("EXTAAAAA FUNCTIONALITY!!!")
        # Original function gets called here.
        original_function()
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    # Wrapper function is returned.
    return wrapper

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
print(f'The function name is {speaker.__name__}')
print(f'The function name is {printer.__name__}')
~~~
~~~
# OUTPUT
EXTAAAAA FUNCTIONALITY!!!
I LOVE PRINTING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

EXTAAAAA FUNCTIONALITY!!!
I LOVE SPEAKING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

The function name is wrapper
The function name is wrapper
~~~

#### Observations:

1. Function `decorator` has taken a function `original_function` as input and wrapped it with other function defined inside it.
2. There are two ways to wrap a function, 1. by annotating it with the decorator's name (line 19-21) or 2. by directly calling the decorator with original function as input and then calling the returned function (line 24-28).
3. `printer` and `speaker` both have the extra functionality we intended to add.
4. `printer.__name__` and `speaker.__name__`  both have name `wrapper` which means the original functions did not retain their attributes. This can be fixed using a module in `functools` named `wraps` as follows. 

~~~python
from functools import wraps

# Defining a decorator.
def decorator(original_function): # Decorator takes the original function as argument
    # Using a  decorator inside decorators to preserve attributes of original function.
    # Notice we are passing the original function to the wraps.
    @wraps(original_function)
    # For now wrapper is not returning None
    def wrapper():
        print("EXTAAAAA FUNCTIONALITY!!!")
        # Original function gets called here.
        original_function()
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    # Wrapper function is returned.
    return wrapper

@decorator
def speaker():
    print("I LOVE SPEAKING!!")

speaker()
print()
print(f'The function name is {speaker.__name__}')
~~~
~~~
# OUTPUT
EXTAAAAA FUNCTIONALITY!!!
I LOVE SPEAKING!!
AGAIN EXTAAAAA FUNCTIONALITY!!!

The function name is speaker
~~~

Now, what if our function had some arguments. Let's try the same decorator on a function with arguments.

~~~python
@decorator
def adder(a, b):
    print(f'{a} + {b} = {a+b}')

adder(3, 4)
~~~
~~~
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
    # Receive any number of arguments
    def wrapper(*args, **kwargs):
        print("EXTAAAAA FUNCTIONALITY!!!")
        # Forward same arguments to the original function
        original_function(*args, **kwargs)
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")
    # Wrapper function is returned.
    return wrapper

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
~~~
~~~
# OUTPUT:
EXTAAAAA FUNCTIONALITY!!!
3 + 4 = 7
AGAIN EXTAAAAA FUNCTIONALITY!!!
EXTAAAAA FUNCTIONALITY!!!
I LOVE PRINTING!!!
AGAIN EXTAAAAA FUNCTIONALITY!!!
~~~

Now let's try making the same decorator using a class. The trick is to overwrite the `__call__` method of the decorator class with the wrapper function of your choice. `__call__` method allows the class's instance to be called as a function.

### Decorator class

~~~python
class decorator(object):
    def __init__(self, original_func):
        self.original_func = original_func

    def __call__(self, *args, **kwargs):
        print("EXTAAAAA FUNCTIONALITY!!!")
        # Forward same arguments to the original function
        self.original_func(*args, **kwargs)
        print("AGAIN EXTAAAAA FUNCTIONALITY!!!")

# Set the decorator
@decorator
def adder(a, b):
    print(f'{a} + {b} = {a+b}')

# Call the decorated function
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
    # Define formating string
    FORMAT = '%(levelname)s %(asctime)s %(message)s'
    # Set basic configuration
    logging.basicConfig(
        format=FORMAT,filename=f'{func.__name__}.log',
        level=logging.INFO
        )
    # Set the wrapper
    def wrapper(*args, **kwargs):
        logging.info(f'Function called: {func.__name__}, with parameters: {args}')
        # Execute the original function and return the result
        return func(*args, **kwargs)
    # Return the wrapper
    return wrapper

# Set the decorator
@func_logger
def adder(a, b):
    return a+b

# Call the function
result = adder(6,7)
~~~
~~~
# Contents of adder.log
INFO 2019-01-29 22:45:30,860 Function called: adder, with parameters: (6, 7)
~~~

In the earlier section, we passed an argument to a decorator `wraps`. Also, if you are familiar with flask, you must have seen the `@app.route('\')` decorator which takes the endpoint as an argument. How do you make the decorators with arguments?

We nest the existing decorator with another decorator function which will accept the required argument and then this argument will be available for every function inside the decorator.

Let's see it in an example: A decorator which takes a number as argument and if the number is greater than 5 it calls the original function otherwise it does not calls it.

~~~python
# Decorator function which takes a number as an argument
def conditional_decorator(number):
    # Decorator which takes the function as argument
    def original_decorator(original_function):
        # Wrapper which executes the original function based on a condition
        def wrapper():
            if number > 5:
                return original_function()
            else:
                print(f"The function {original_function.__name__} did not execute")
        # Original decorator returns the wrapper
        return wrapper
    # Outer decorator returns the original decorator
    return original_decorator

# Using conditional_decorator 6
@conditional_decorator(6)
def printer():
    print("I LOVE PRINTING!!")

# Using conditional_decorator 4
@conditional_decorator(4)
def speaker():
    print("I LOVE SPEAKING!!")

printer()
print()
speaker()
~~~
~~~
# OUTPUT:
I LOVE PRINTING!!

The function speaker did not execute
~~~

And this is it.