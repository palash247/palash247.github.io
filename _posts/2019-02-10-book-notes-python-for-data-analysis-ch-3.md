---
layout: post
title:  "Book Notes: Python for data analysis Chapter 3"
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


# Built in Data Structures, Functions and Files

## Tuple

**Important Points:**

1. Immutable
2. Can store mutable objects, which can be modified inplace
3. `+` operation results in new concatenated tuple
4. `*` operation as in list, results in concatenating that many copies of tuples

{% highlight python %}
tup = 1,2,[3,4],True
print(tup)
print(tup[2])
{% endhighlight %}

    (1, 2, [3, 4], True)
    [3, 4]

{% highlight python %}
tup[1] = 5
{% endhighlight %}

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-2-d14146d6c2a7> in <module>()
    ----> 1 tup[1] = 5
    

    TypeError: 'tuple' object does not support item assignment

{% highlight python %}
tup[2].append(67)
print(tup)
{% endhighlight %}

    (1, 2, [3, 4, 67], True)

{% highlight python %}
print(tup + (45, 87))
{% endhighlight %}
    (1, 2, [3, 4, 67], True, 45, 87)

{% highlight python %}
print(tup*5)
{% endhighlight %}

    (1, 2, [3, 4, 67], True, 1, 2, [3, 4, 67], True, 1, 2, [3, 4, 67], True, 1, 2, [3, 4, 67], True, 1, 2, [3, 4, 67], True)


**Unpacking Uses**

1. Swapping
2. In loops
3. Filtering partial elements and neglecting rest.


{% highlight python %}
print('unpacking')
a, b = (1, 2)

print(a)
print(b)

print('swapping')
a, b = b, a

print(a)
print(b)

print('nested tuple unpacking')
a,b,(c,d) = 1,2,(3,5)
print(a,b,c,d)

print('loops')
tup = (1,2), (3,5)
for a, b in tup:
    print("a",a)
    print("b",b)
    
print('filtering rest')
(a, _),*rest = tup
print(a)
print("rest: ",rest)
{% endhighlight %}

    unpacking
    1
    2
    swapping
    2
    1
    nested tuple unpacking
    1 2 3 5
    loops
    a 1
    b 2
    a 3
    b 5
    filtering rest
    1
    rest:  [(3, 5)]

**Tuple methods**
It is light on instance method, one useful is `count(element)`, which counts the number of occurrences of the element in tuple.

{% highlight python %}
tup = 1,2,2,2,2,3,4,5,65
tup.count(2)
{% endhighlight %}

    4

## List

**Important Points**

1. `insert` method allows you to insert elements at any index but it is costly operation because some indexes need to be shifted. Insertion index must be between 0 and lenght of the list inclusive.
2. `pop` is opposite of `insert`. It removes and returns the value at particular index.
3. Elements can be removed by value with `remove` method.
4. Checking if a element is in list by using `in` keyword is expensive operations because it is a linear search. Set and Dictionaries uses hash table and hence takes constant time for retrieval.
5. Concatenating two list is possible using `+` or `extend` method. Addition operation is little costly because new objects needs to be created.
6. Sorting is possible using method `sort` and function `sorted` both taking same arguments. It can also take an argument `key`, a function which returns a number to sort on.
7. You can mainatain a binary search tree using `bisect` type from `bisect` module.
8. In slicing, integer after the second colon represents a step. `a[::2]` will produce another list starting from first element of `a` and stepping single element till end. Negative number in slicing represents count from end of the list, i.e, `a[-1]` represents last element of the list. If we combine stepping with this, we can reverse the list very easily by `a[::-1]`.


{% highlight python %}
a = [1,2,3,4,5]
print('`insert` method allows you to insert elements at any index but it is costly operation because \
some indexes need to be shifted. Insertion index must be between 0 and lenght of the list inclusive.')
print(a)
a.insert(1, 89)
print(a)
print()
print('`pop` is opposite of `insert`. It removes and returns the value at particular index.')
print("poped element",a.pop(1))
print(a)
print()
print('Elements can be removed by value with `remove` method.')
a.remove(3)
print(a)
print()
print('Checking if a element is in list by using `in` keyword is expensive operations\
because it is a linear search.')
print(3 in a)
print()
print('Concatenating two list is possible using `+` or `extend` method. Addition operation is little costly\
because new objects needs to be created.')
print(a+[7,8,9])
print(a)
a.extend([7,8,9])
print(a)
print()
print('Sorting is possible using method `sort` and function `sorted` both taking same arguments. \
It can also take an argument `key`, a function which returns a number to sort on.')
b = ['one', 'two', 'three']
b.sort()
print(b)
b.sort(key=len,reverse=True)
print(b)
print()
{% endhighlight %}

    `insert` method allows you to insert elements at any index but it is costly operation because some indexes need to be shifted. Insertion index must be between 0 and lenght of the list inclusive.
    [1, 2, 3, 4, 5]
    [1, 89, 2, 3, 4, 5]
    
    `pop` is opposite of `insert`. It removes and returns the value at particular index.
    poped element 89
    [1, 2, 3, 4, 5]
    
    Elements can be removed by value with `remove` method.
    [1, 2, 4, 5]
    
    Checking if a element is in list by using `in` keyword is expensive operationsbecause it is a linear search.
    False
    
    Concatenating two list is possible using `+` or `extend` method. Addition operation is little costlybecause new objects needs to be created.
    [1, 2, 4, 5, 7, 8, 9]
    [1, 2, 4, 5]
    [1, 2, 4, 5, 7, 8, 9]
    
    Sorting is possible using method `sort` and function `sorted` both taking same arguments. It can also take an argument `key`, a function which returns a number to sort on.
    ['one', 'three', 'two']
    ['three', 'one', 'two']
    


**Functions on List/Sequence**

`enumerate`: Returns sequence of (i, element_i) i being the unique integer index and element_i being the member of the squence.

`zip`: Merges multiple seqences to create sequence of tuples. Can accept any arbitory number of elements in sequence, the pairing will happen according to shortest of sequence. Unzipping is also possible which is actualy convering list of rows to list of columns.

`sorted`: same as sort method.

`reversed`: gives a generator which yield the sequence in reverse order



{% highlight python %}
a = ['a', 'b', 'c', 'd']
print('Returns sequence of (i, element_i) i being the unique integer index and element_i \
being the member of the squence.')
print(enumerate(a))
print()

b = [7,3,9,0]
print('Merge two lists')
print(list(zip(a,b)))
print()

c = [('Elon', 'Musk'), ('Bill', 'Gates')]
print("Converting to list of firstnames and lastnames. Isn't that clever?")
print(list(zip(*c)))
{% endhighlight %}

    Returns sequence of (i, element_i) i being the unique integer index and element_i being the member of the squence.
    <enumerate object at 0x7f3e60320cf0>
    
    Merge two lists
    [('a', 7), ('b', 3), ('c', 9), ('d', 0)]
    
    Converting to list of firstnames and lastnames. Isn't that clever?
    [('Elon', 'Bill'), ('Musk', 'Gates')]


## Dictionary

**Important properties**

1. Access time is always constant.
2. Methods `keys` and `values` gives iterator on keys and values of the dictionary respectively. Though, there is no particular order in dictionary, these method gives output in order.
3. zip can help you in creating dictionary from sequence of keys and values.
4. `a.get(name, default_value)` will get you value of key `name` if it exists in dictionary a, `default_value` otherwise. If `default_value` not given, `None` will be returned.
5. Sometimes, you might need to check if the key exists in the dictionary, set some default value to it if it does not exists, and then update the same value. `a.setdefault('key_name', default_value)` can be used for this.
6. `collections` module has `defaultdict`, which makes this task way simpler.
7. Keys of the dictionary need to be hashable objects. scalars `int`, `float`, `strings` or tuples with its objects hashable. All immutable object in python are hashable.


{% highlight python %}
print('zip can help you in creating dictionary from sequence of keys and values.')
k = list(range(0,5))
a = dict(zip(k,k[::-1]))
print(a)
{% endhighlight %}

    zip can help you in creating dictionary from sequence of keys and values.
    {0: 4, 1: 3, 2: 2, 3: 1, 4: 0}



{% highlight python %}
print('a.get(name, default_value) will get you value of key name if it exists in dictionary a, \
default_value otherwise. If defaul_value not given, None will be returned.')
## get
print(a.get(5, 0))
print()
## Suppose you want to store each word in some sentence by its starting letter.
sent = "Keys of the dictionary need to be hashable objects. scalars int, float, strings or tuples with its objects\
 hashable. All immutable object in python are hashable"
word_map = {}
for word in sent.split():
    word_map.setdefault(word[0], []).append(word)
print(word_map)
print()

{% endhighlight %}

    a.get(name, default_value) will get you value of key name if it exists in dictionary a, default_value otherwise. If defaul_value not given, None will be returned.
    0
    
    {'K': ['Keys'], 'o': ['of', 'objects.', 'or', 'objects', 'object'], 't': ['the', 'to', 'tuples'], 'd': ['dictionary'], 'n': ['need'], 'b': ['be'], 'h': ['hashable', 'hashable.', 'hashable'], 's': ['scalars', 'strings'], 'i': ['int,', 'its', 'immutable', 'in'], 'f': ['float,'], 'w': ['with'], 'A': ['All'], 'p': ['python'], 'a': ['are']}
    



{% highlight python %}
print('Keys of the dictionary need to be hashable objects. scalars \
 int, float, strings or tuples with its objects hashable. All immutable object in python are hashable.')
print()
print(word_map.keys())
print()
print(word_map.values())
{% endhighlight %}

    Keys of the dictionary need to be hashable objects. scalars  int, float, strings or tuples with its objects hashable. All immutable object in python are hashable.
    
    dict_keys(['K', 'o', 't', 'd', 'n', 'b', 'h', 's', 'i', 'f', 'w', 'A', 'p', 'a'])
    
    dict_values([['Keys'], ['of', 'objects.', 'or', 'objects', 'object'], ['the', 'to', 'tuples'], ['dictionary'], ['need'], ['be'], ['hashable', 'hashable.', 'hashable'], ['scalars', 'strings'], ['int,', 'its', 'immutable', 'in'], ['float,'], ['with'], ['All'], ['python'], ['are']])

## Set

**Important Points**

1. Set support set operations like union, intersection, difference, disjoint.
2. Every logical set operation has, inplace counterpart.\

## Comprehensions

Normal list coprehensions `[expr for val in collection if condition]`



{% highlight python %}
[len(x) for x in "Tere Shooteron Ka Khas Meri Gully Mein".split() if len(x)>4]
{% endhighlight %}




    [9, 5]



Nested list comprehensions are little hard to wrap your head around. If you feel stucked, don't bother writing the normal nested loops. In fact, normal nested loops can help you to write the nested list comprehension because the order of the loops is same in both, with the condition at last as usual.


{% highlight python %}
# find words which have length more than 4
collection = [
    "Tere Shooteron Ka Khas Meri Gully Mein".split(),
    "Kiska hain yeh tumko intazaar main hoon na".split(),
    "Wise men says, only fools rush in".split(),
    "Her eyes Her eyes makes the stars look like they're not shining".split()
]

long_words = [word for songs in collection for word in songs if len(word)>4]
print(long_words)
print()
# analyse the close resembalance with normal nested for loops
long_words = []
for songs in collection:
    for word in songs:
        if len(word) >4:
            long_words.append(word)
print(long_words)
{% endhighlight %}

    ['Shooteron', 'Gully', 'Kiska', 'tumko', 'intazaar', 'says,', 'fools', 'makes', 'stars', "they're", 'shining']
    
    ['Shooteron', 'Gully', 'Kiska', 'tumko', 'intazaar', 'says,', 'fools', 'makes', 'stars', "they're", 'shining']


## Functions

**Important Points**
1. positional arguments before keyword arguments
2. Unlike functions defined by `def`, lambda functions don't get the automatic assignment to the `__name__` attribute, hence they are called anonymous functions.
3. *Currying* is a fancy computer science term used for partial argument functions. It can be done using `lambda` functions or `partial` from `functools` module.



{% highlight python %}
def adder(a, b):
    return a+b

square = lambda a: a**2

print("Value in __name__ attrubute of function defined by def: ", adder.__name__)
print("Value in __name__ attribute in lambda function: ", square.__name__)
{% endhighlight %}

    Value in __name__ attrubute of function defined by def:  adder
    Value in __name__ attribute in lambda function:  <lambda>



{% highlight python %}
from functools import partial
adder_5 = partial(adder, 5)
adder_6 = lambda x: adder(x, 6)
print("With partial: ",adder_5(6))
print("With lambda: ",adder_6(5))
{% endhighlight %}

    With partial:  11
    With lambda:  11


## Generators

The *iterator protocol* is a way to make objects iterable. An iterator is an object which will yield objects to the python interpreter when used in a context like `for` loop. Most method which expects list like arguments, also takes iterable object. Generator is a concise way to construct new iterable object.

**Important Points**

1. generator expressions can be generated using comprehension enclosed in round breckets
2. To build a generator you need a function with `yield` instead of `return`
3. Module `itertools` has nice functions to work on generators or any other sequences in python. `groupby`, `combinations`, `permutations` to name few. `groupby` can help you in grouping **consecative elements in sequence** from the given list or generator with respect to a key function


{% highlight python %}
def square(n=10):
    for i in range(n):
        yield i**2
{% endhighlight %}

{% highlight python %}
## Initializing a generator does not executes its code.
gen = square()
type(gen)
# using it in the context like for loop and functions like max, min, sum, list, tuple, dict does
list(gen)
{% endhighlight %}

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

{% highlight python %}
import itertools
{% endhighlight %}

{% highlight python %}
words = ['Elon', 'Bill', 'Lina', 'Bruno', 'Wong', 'Jonas', 'Priyanka']
for key, words in itertools.groupby(words, key = lambda x: len(x)):
    print(key, list(words))
{% endhighlight %}

    4 ['Elon', 'Bill', 'Lina']
    5 ['Bruno']
    4 ['Wong']
    5 ['Jonas']
    8 ['Priyanka']


## Exception Handling

**Important Point**

1. In iPython you can set the detail level of an exception by using `%xmod Verbose`. To revert it back `%xmod Plain`.


{% highlight python %}
def flt(x):
    try:
        return float(x)
    except(ValueError, TypeError):
        print("Failed")
    else:
        print("Successful")
    finally:
        print("Close any resource if it is open.")
    return x

x = flt('1.2')
y = flt('something')
{% endhighlight %}

    Close any resource if it is open.
    Failed
    Close any resource if it is open.


## Files

**Important points**

1. if you read a file with function `open`, you can use the file handel to iterate over lines in the file as a string. Each line will have the `EOL` line character which can be stripped using method `rstrip` or `strip`.
2. To read a binary file you can attach `b` to file read mode `r`. File read in `rb` mode will read a byte as a character.
3. Method `read`, takes the number of characters to read and returns them and advances the file handle position. 
4. Method `tell` will give you the current position of the file handle.
5. Method `seek` will seek the file handle by give number of the integer argument. It also returns the same number.
6. You can check the default encoding from `sys.getdefaultencoding`
7. `x` write mode. Raises error if the file already exists.
8. `r+` read and write.
9. You can write lines in a list to a file using method `writelines`
10. By default, python will read files in text mode, i.e, in Unicode encoding.


{% highlight python %}
# lets create a file first
d = """if you read a file with function open, you can use the file handel to iterate over lines in the file as a string. Each line will have the EOL line character which can be stripped using method rstrip or strip.
To read a binary file you can attach b to file read mode r. File read in rb mode will read a byte as a character.
Method read, takes the number of characters to read and returns them and advances the file handle position.
Method tell will give you the current position of the file handle.
Method seek will seek the file handle by give number of the integer argument. It also returns the same number.
You can check the default encoding from sys.getdefaultencoding
x write mode. Raises error if the file already exists."""

lines = []
with open('file_op_test.txt', 'w') as handle:
    handle.write(d)

with open('file_op_test.txt') as handle:
    lines.extend(list(x.rstrip() for x in handle))
print(lines)
print()
import sys
print(sys.getdefaultencoding())
{% endhighlight %}

    ['if you read a file with function open, you can use the file handel to iterate over lines in the file as a string. Each line will have the EOL line character which can be stripped using method rstrip or strip.', 'To read a binary file you can attach b to file read mode r. File read in rb mode will read a byte as a character.', 'Method read, takes the number of characters to read and returns them and advances the file handle position.', 'Method tell will give you the current position of the file handle.', 'Method seek will seek the file handle by give number of the integer argument. It also returns the same number.', 'You can check the default encoding from sys.getdefaultencoding', 'x write mode. Raises error if the file already exists.']
    
    utf-8
