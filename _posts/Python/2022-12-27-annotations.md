---
layout: post
title: Basics about Scheme
date: 2022-12-27
categories: [Python]
tags: [Python, annotations]
---


# Annotations
## Function annotations
###  syntax
1. Function annotations, both for parameters and return values, are completely optional.
2. Function annotations are nothing more than a way of associating arbitrary Python expressions with various parts of a function at compile-time. 

   The only way that annotations take on meaning is when they are interpreted by third-party libraries. These annotation consumers can do anything they want with a function’s annotations. For example, one library might use string-based annotations to provide improved help messages.

In the example below, I add annotations for the parameter and return type of the function. The annotations will not force your program to do things, like forcing your return to be integer, it just indicates things.

```python
def f1(n:'integer')->'result':
    if n <= 0:
        return 1
    else:
        return 1 + f1(n-1)
```

Once compiled, a function’s annotations are available via the function’s `__annotations__` attribute. `__annotations__` is an empty, mutable dictionary if there are no annotations on the function or if the functions was created from a lambda expression.
```shell
>>> f1.__annotations__
{'n': 'integer', 'return': 'integer'}
```

The `return` key was chosen for your annotation of return because it cannot conflict with the name of a parameter; any attempt to use return as a parameter name would result in a SyntaxError.


## Variable annotations
> It should also be emphasized that Python will remain a dynamically typed language, and the authors have no desire to ever make type hints mandatory, even by convention. Type annotations should not be confused with variable declarations in statically typed languages. **The goal of annotation syntax is to provide an easy way to specify structured type metadata for third party tools.**

# References
1. [PEP: Function annotations](https://peps.python.org/pep-3107/)
2. [PEP Syntax for Variable Annotations](https://peps.python.org/pep-0526/#specification)