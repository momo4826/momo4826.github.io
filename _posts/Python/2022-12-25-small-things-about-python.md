---
layout: post
title: Small things about Python
date: 2022-12-25
categories: [Python]
tags: [python]
---

# Function attributes and decorators
We will take the code below as an example.
```python
def count(f):
    """Count how many times the recursive function runs"""
    def counted(n):
        counted.call_count += 1
        return f(n)
    counted.call_count = 0
    return counted

@count
def fib(n):
    if n == 0 or n == 1:
        return n
    else:
        return fib(n-2) + fib(n-1)
```

## Function attributes
This is not special for python. 
Given that python is object-oriented programming, it's kin of easy to understand that function, which is also an object, can have attributes.

 We can check what attributes and methods `fib` has through `dir`. There are so many things in the list, two important things are `__dict__` and `call_count`. The appearence of `call_count` means we already add a new attribute to this function `fib`.

As for `__dict__`, in [PEP232](https://peps.python.org/pep-0232/),this proposal adds a new dictionary to function objects, called `func_dict`(a.k.a. `__dict__`). 
> This dictionary can be set and get
using ordinary attribute set and get syntax.
> * Deleting a function’s `__dict__`, or setting it to anything other than a concrete dictionary object results in a TypeError. 
> * If no function attributes have ever been set, the function’s `__dict__` will be empty.

```python
>>> dir(fib)
['__annotations__', '__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__get__', '__getattribute__', '__globals__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__kwdefaults__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'call_count']
>>> hasattr(fib, 'call_count')
True
>>> fib.__dict__
{'call_count': 3}
>>> count.__dict__
{}
```

Because we assign a default value `0` to this `cal_count` attribute in the decorator, the value of `fib.__dict__['call_count']` would be `0` when `fib` hasn't been called.
## Decorators
> A decorator is a design pattern in Python that allows a user to add new functionality to an existing object without modifying its structure.

The `@count` we put just above the target function we want to extend is a shorthand for `fib = count(fib)`. These two syntaxes both create a new version of `fib` that can count the number of recursion. 

Given the purpose, we need to ensure the return of decorator is the new version of function we want when design the decorator. Here, `counted` in decorator is exactly the new version of `fib` we want. You can see that we create a new attribute for function `counted`, which means our new version of `fib` will have this attribute.

# List operations
## Slice assignment
slice assignment replaces a slice with new values. If the length of the slice is shorter than the length of the values. extra values will be added and then the length of original list will be larger. Slice assignment can also 
remove elements from a list by assigning [] to a slice.

```python
>>> x = [1,2]
>>> x[0:0]
[]
>>> x[0:0] = [5]
>>> x
[5, 1, 2]
>>> x[1:1] = [0]
>>> x
[5, 0, 1, 2]
>>> x[1:2] = [9]
>>> x
[5, 9, 1, 2]
```

## Copy of lists
The only two ways that you can get a copy of a list are: `list(t)` and `t[:]`.
In the example below, `[t]` doesn't a list of a copy of `t`, so if `t` changes, `[t]` also changes.
```python
>>> t = [1,2,3]
>>> t[1:3] = [t]
>>> t
[1, [...]]
>>> t.extend(t)
>>> t
[1, [...], 1, [...]]
```

# References
1. [PEP232](https://peps.python.org/pep-0232/)
2. [PEP319](https://peps.python.org/pep-0318/#examples)
3. [What is Decorator?](https://www.datacamp.com/tutorial/decorators-python)








