---
layout: post
title:  "Book Notes: Python for data analysis Chapter 2"
modified:   2019-02-04 23:00:19
excerpt: "My notes on Wes McKinney's Python for Data Analysis"
categories: [python, book notes]
tags: [ipython, python for data analysis]
comments: true
share: true
pinned: false
use_math : true
# image:
#     feature: https://raw.githubusercontent.com/palash247/palash247.github.io/master/img/rubik.png
#     credit: Andrew Martin
#     creditlink: https://pixabay.com/en/users/aitoff-388338/
---

**Disclaimer**: These are my notes, hence focused on the areas which I am prone to forget. There is a strong possibility of some sections not making sense to you or they are too easy for you.
{: .notice}

Pandas name is derived from *panel data* and *python data analysis*

{% highlight python %}
import numpy as np
# add wildcards and then use object introspection to see matching attributes/methods
np.*lin*?

adder = """
def adder(a,b,c):
    return a+b+c
    
x=1
y=2
z=3.4

result=adder(x,y,z)
"""
with open("adder.py", "w") as f:
    f.write(adder)
    
# %run executes python files with every import, variable, function, object accessible in the current namespace.
%run adder.py
print(x,y,z, result)

# you can also pass the variables in the current namespace to the file by passing -i to %run
adder = """
def adder(a,b,c):
    return a+b+c

result=adder(x,y,z)
"""
with open("adder.py", "w") as f:
    f.write(adder)
x, y, z = (2,5,6)
%run -i adder.py
print(x,y,z, result)
{% endhighlight %}

    1 2 3.4 6.4
    2 5 6 13


%load gets the content of file into current cell


~~~python
# %load adder.py

def adder(a,b,c):
    return a+b+c

result=adder(x,y,z)

~~~

%paste and %cpaste can be used to execute code from the clipboard to **ipython shell only**. %paste will execute code from clipboard immidiately and %cpaste will give you freedom to paste code Ctl+Shift+V as many times as you want before executing.


~~~python
import matplotlib.pyplot as plt
%matplotlib inline
~~~


~~~python
plt.hist(np.random.randn(1000))
~~~




    (array([  5.,  16.,  70., 172., 227., 253., 168.,  51.,  29.,   9.]),
     array([-3.19548746, -2.56284222, -1.93019699, -1.29755175, -0.66490651,
            -0.03226128,  0.60038396,  1.23302919,  1.86567443,  2.49831967,
             3.1309649 ]),
     <a list of 10 Patch objects>)




![png](../../img/output_7_1.png)


Python is a **loosely** typed language. It will do automatic casting in some obvious cases but not always.


~~~python
# obvious case
5+5.5
~~~




    10.5




~~~python
# not obvious
5+'5'
~~~


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~/git/Data-Science-Notes/adder.py in <module>()
          1 # not obvious
    ----> 2 5+'5'
    

    TypeError: unsupported operand type(s) for +: 'int' and 'str'


Knowing type of the object is important while validating the arguments of the function, *isinstance* comes handy for that.


~~~python
a = 1
b = 1.5
def foo(a,b):
    # checking if a and b are both either float or integer
    if isinstance(a,(float,int)) and isinstance(b, (float, int)):
        print("Addition is: ", a+b)
    else:
        raise TypeError()
foo(a,b)
~~~

Accessing attributes and methods of the object is done either by `object.attribute_name` or by using function `getattr(object, 'attribute_name')`. Accessing attributes by their name is known by **reflection** in other languages.


~~~python
a = 'Data Analysis'
# traditional way
print(a.split())
# using getattr
print(getattr(a, "split")())
~~~

Use `is` keyword to check if two references are same. This is different from `==` because `==` compares the value of object refered.


~~~python
a = [1,2,3]
b = a
c = list(a)
print("a is b: ",a is b)
# list() will always create a new object
print("a is c: ",a is c)
print("a == c:", a == c)
~~~

Bitwise operations


~~~python
# Or
print(True | False, 4 | 4)
# And
print(True & False, 4 & 4)
# Ex-Or
print(True ^ False, 4 ^ 4)
~~~

String templating or formating


~~~python
template = 'The float {0:5f}, The int {1:d}'
print(template.format(1/3, 3))
~~~

None is the singleton instance of the class `NoneType` 

The `datetime` module contains `datetime`, `date`, `timedelta` and `time` types all being immutable. `datetime` type combines `time` and `date`. Difference of two `datetime` instance gives `timedelat` object.


~~~python
from datetime import datetime, time, date

# init datetime
dt = datetime(2017, 1, 2, 19, 20, 21)

# display
print(dt)

# change format of printing using strftime, str format time
print(dt.strftime("%Y/%m/%d %H:%M:%S"))

# use strptime to parse a string for datetime values, str parse time
new_dt = datetime.strptime("2017/01/03 12:20:21", "%Y/%m/%d %H:%M:%S")

# print time 
print(dt.time())

# print date
print(dt.date())

# difference of two datetime objects gives timedelta object
delta = new_dt - dt
print(type(delta))
print(delta)

# delta can be added to datetime objects as an offset
print(dt+delta)

# sometimes you may need to replace some components of datetime object
# as the datetime object is immutable, .replace method always returns a new object
print(dt.replace(minute=0, second=0))
~~~
