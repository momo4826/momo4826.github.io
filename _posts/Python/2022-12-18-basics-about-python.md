---
layout: post
title: Basics about Python
date: 2022-12-18
categories: [Python]
tags: [python, functions, control, higher-order functions, environment, decorator]
---
This article includes notes of CS61A lectures from week1 to week 3.

# Expressions, names and statements
## Expressions and names
expression includes primitive expressions like number of numeral, name and string, and call expressions.
A name can represent a variable or a function.
### None
`None` is special in python.
The type of `None` is NoneType. It cannot do any operations with any expressions(even `None` itself).

If a function doesn't explicitly return a value, it will return `None`.
In python, we can assign the value of function which returns `None` to a variable whose value will be `None` then; while in c, we use `void` in function definition to declare that a function returns nothing, and we can't assign the value of a void function to any variable.

In c, `printf` returns the number of characters printed, while in Python, `print` return `None`.

Notice, None is not displayed by the interpreter as the value of an expression, which means if you type `None` in the python interpreter and press `enter`, nothing will be displayed. But you can get `None` displayed by `print(None)`.

## Statements
We can use some defined "boxes" to describe what statements are. 
<figure align = "center">
    <img src = "/assets/images/computer%20science/statements_1.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/03-Control_1pp.pdf">CS61A</a></figcaption>
</figure>

<figure align = "center">
    <img src = "/assets/images/computer%20science/statements_2.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/03-Control_1pp.pdf">CS61A</a></figcaption>
</figure>

## Control expression
To evaluate the expression <left> and <right>:
1. Evaluate the subexpression <left>.
2. If the result is a false value v, then the expression evaluates to v.
3. Otherwise, the expression evaluates to the value of the subexpression <right>.

To evaluate the expression <left> or <right>:
1. Evaluate the subexpression <left>.
2. If the result is a true value v, then the expression evaluates to v.
3. Otherwise, the expression evaluates to the value of the subexpression <right>.

In python, `x = True and 12` then the value of x is `12`, while in c, `int x = true && 12` the value of x is `1`.
# Abstraction
Assignment is a basic means of abstraction, binding names to values.
Function definition is a more powerful abstraction means, binding names to expressions

## Functions
Function is only executed when it's called. And every time a function is called, it will be evaluated again. So if the variable in it is changed, then the result of it will be changed.

Procedure of calling a user-defined function
1. add a local frame, forming a new environment
2. bind the function's formal parameters to its arguments in that frame
3. execute the body of the function in that new environment


Different from user-defined functions, Built-in names like “max” or any other names imported from libraries, are in the global frame.

<figure align = "center">
    <img src = "/assets/images/computer%20science/calling_functions_1.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/02-Functions_1pp.pdf">CS61A</a></figcaption>
</figure>

<figure align = "center">
    <img src = "/assets/images/computer%20science/calling_functions_2.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/02-Functions_1pp.pdf">CS61A</a></figcaption>
</figure>

<figure align = "center">
    <img src = "/assets/images/computer%20science/calling_functions_3.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/03-Control_1pp.pdf">CS61A</a></figcaption>
</figure>

### difference between parameters and arguments:

> Function parameters are the names listed in the function's definition. Function arguments are the real values passed to the function. Parameters are initialized to the values of the arguments supplied.

### Design a function
1. Figure out the inputs, outputs and the relation between inputs and outputs
2. Every function only do one thing
3. In order to figure out the approach to solve the problem, start from specific examples, then generalize it

### Pure functions and None-pure functions
Pure functions inputs arguments and then return outputs, nothing else will be displayed or changed when you call pure functions.
While non-pure functions have side effects, which means except values returned, something else is also happened as a consequence of calling non-functions. For example, `print` is a non-pure function, it returns `None`, but it will display something as a side effect when it's called.


### Decorators
In the Hog project of CS61A, you will see:
```python
from ucb import main

@main
def run(*args):
    """Read in the command-line argument and calls corresponding functions."""
    import argparse
    parser = argparse.ArgumentParser(description="Play Hog")
    parser.add_argument('--run_experiments', '-r', action='store_true',
                        help='Runs strategy experiments')

    args = parser.parse_args()

    if args.run_experiments:
        run_experiments()
```
`@main` is called a decorator, and `run` here is a decorated function. The above code is equal to the code below without decorator:
```python
from ucb import main

def run(*args):
    """Read in the command-line argument and calls corresponding functions."""
    import argparse
    parser = argparse.ArgumentParser(description="Play Hog")
    parser.add_argument('--run_experiments', '-r', action='store_true',
                        help='Runs strategy experiments')

    args = parser.parse_args()

    if args.run_experiments:
        run_experiments()
        
run = main(run)
```

The power of decorators is that it allows you to change the behavior of a function without modifying the function itself.

## High-order functions
The formal parameters of functions are expressions. And as we know from the definition of expression, it can be functions(one kind of names). 
A function that takes a function as argument value or returns a function as return value is called high-order function.

When the common structure among functions is a computational process, then use function as parameter is useful for generalization. An example as follows:
<figure align = "center">
    <img src = "/assets/images/computer%20science/function_1.png" height="300">
    <figcaption>figure from <a href="https://cs61a.org/assets/slides/04-Higher-Order_Functions_1pp.pdf">CS61A</a></figcaption>
</figure>
When the function arguments in high-order function has arbitrary number of arguments, you will have to use `*args` syntax. For example:

```python
def make_averaged(original_function, total_samples=1000):
    """Return a function that returns the average value of ORIGINAL_FUNCTION
    called TOTAL_SAMPLES times.

    To implement this function, you will have to use *args syntax(because the number of arguments of `original_function` is arbitary).

    >>> dice = make_test_dice(4, 2, 5, 1)
    >>> averaged_dice = make_averaged(roll_dice, 40)
    >>> averaged_dice(1, dice)  # The avg of 10 4's, 10 2's, 10 5's, and 10 1's
    3.0
    >>> dice = make_test_dice(3, 1, 5, 6)
    >>> averaged_dice = make_averaged(dice, 1000)
    >>> # Average of calling dice 1000 times
    >>> averaged_dice()
    3.75
    """
    def average_helper(*args):
        res = 0
        for i in range(total_samples):
            res += original_function(*args)
        return res / total_samples
    return average_helper
```

### Function currying
Transform a multi-argument function into a single-argument.
### Examples
```python
>>> def cake():
...    print('beets')
...    def pie():
...        print('sweets')
...        return 'cake'
...    return pie
>>> chocolate = cake()
beets

>>> chocolate
Function

>>> chocolate()
sweets
'cake'

>>> more_chocolate, more_cake = chocolate(), cake
sweets

>>> more_chocolate
'cake'
```
## Environments
What is an environment? It's the context of expressions. Because the program is executed sequentially, the current environment changes time to time. The current environment is either global frames or local frames followed by global frames.

Remember：
> 1. An environment is a sequence of frames. 
> 2. A name evaluates to the value bound to that name in the earliest frame of the current
environment in which that name is found.

Example:

to look up some name in the body of the square function:
• Look for that name in the **local frame first**.
• If not found, look for it in the global frame.







# References
1. [Parameters](https://developer.mozilla.org/en-US/docs/Glossary/Parameter)





