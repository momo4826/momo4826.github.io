---
layout: post
title: Fibonacci class
date: 2022-12-20
categories: [Python]
tags: [python, class, instance attributes]
---
Next Virahanka Fibonacci Object
Implement the next method of the VirFib class. For this class, the value attribute is a Fibonacci number. The next method returns a VirFib instance whose value is the next Fibonacci number. The next method should take only constant time.

Hint: This problem doesn't ask you to return next value for VirFib(x) where x is random. It just always starts from VirFib(0), so all you need to do is to keep track the last one.
```python
class VirFib():
    """A Virahanka Fibonacci number.

    >>> start = VirFib()
    >>> start
    VirFib object, value 0
    >>> start.next()
    VirFib object, value 1
    >>> start.next().next()
    VirFib object, value 1
    >>> start.next().next().next()
    VirFib object, value 2
    >>> start.next().next().next().next()
    VirFib object, value 3
    >>> start.next().next().next().next().next()
    VirFib object, value 5
    >>> start.next().next().next().next().next().next()
    VirFib object, value 8
    >>> start.next().next().next().next().next().next() # Ensure start isn't changed
    VirFib object, value 8
    """

    def __init__(self, value=0):
        self.value = value

    def next(self):
        if self.value == 0:
            result = VirFib(1)
        else:
            result = VirFib(self.value + self.previous)
        result.previous = self.value
        return result

    def __repr__(self):
        return "VirFib object, value " + str(self.value)
```