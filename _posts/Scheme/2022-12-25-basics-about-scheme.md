---
layout: post
title: Basics about Scheme
date: 2022-12-25
categories: [Scheme]
tags: [Scheme]
---

Scheme is a Dialect of Lisp.

Scheme's core data type is the **list**, built out of pairs. Scheme code is actually built out of these lists. This means that the code `(+ 1 2)` is constructed as a list of the `+` symbol, the number `1`, and the number `2`, which is then evaluated as a call expression.

# Expression
## Primitive(atomic) expressions
Numbers, booleans, strings, and the empty list (nil).

Numbers are self-evaluating; symbols are atomic, but are not self-evaluating (they instead evaluate to a value that was previously bound to it in the environment). 
## Combinations
The Scheme expressions that are not atomic are called combinations, and consist of one or more subexpressions between parentheses, such as (quotient 10 2), (not true).

### Call expressions
Most forms of combinations are evaluated as call expressions.
Call expressions include **an operator and 0 or more operands in parentheses**.
### Special forms
A combination that is not a call expression is a special form.

The interpreter maintains a set of particular symbols (sometimes called keywords) that signal that a combination is a special form when they are the first subexpression. 

The interpreter always checks the first subexpression of a combination first. If it matches one of the keywords, the corresponding special form is used. Otherwise, the combination is evaluated as a call expression.

#### quote
`(quote <expression>)` or `'<expression>`

Returns the literal expression without evaluating it.

```shell
scm> (+ 1 2)
3
scm> (quote (+ 1 2))
(+ 1 2)
scm> '(+ 1 2)
(+ 1 2)

scm> +
#[+]
scm> '+
+
```
#### define
`(define <name> <expression>)`

Evaluates <expression> and binds the value to <name> in the current environment. 

`(define (<name> [param] ...) <body> ...)`
Constructs a new lambda procedure with params as its parameters and the body expressions as its body and binds it to name in the current environment. This shortcut is equivalent to:
`(define <name> (lambda ([param] ...) <body> ...))`.


Example:
```shell
scm> (define x 2)
x
scm> x
2
scm> (define (f x) 2*x)
f
scm> f
(lambda (x) 2*x)
scm> (define (abs x)
...> (if (< x 0) (- x) x)
...> )
abs
scm> (define a -3)
a
scm> (abs a)
3
scm> abs
(lambda (x) (if (< x 0) (- 0 x) x))
```
#### if
`(if <predicate> <consequent> [alternative])`

Evaluates predicate. If true, the consequent is evaluated and returned. Otherwise, the alternative, if it exists, is evaluated and returned (if no alternative is present in this case, the return value is undefined).

```shell
scm> (define x 2)
x
scm> (if (zero? x) (+ x 5) (* x 2))
4
```

#### cond
```
(cond
    (<test> [expression])
    ...
    (else [expression])
   )
```
Example:
```shell
scm> (define n -3)
n
scm> (cond
    ((< n 0) -1)
    ((> n 0) 1)
    (else 0)
...> )
-1
```
#### begin
The begin special form combines multiple expressions into one expression

```shell
(cond 
  ((> x 0) (begin (print 1) (+ 2 3))) 
  (else 3)
)
```
#### let
The let special form binds symbols to values temporarily; just for one expression

```shell
(define (duplicate lst) 
    (let (
            (tmp (map (lambda (x) (list x x)) lst))
        )
        (cond 
            ((null? tmp) nil)
            (else (reduce append tmp))
        )
    )
)
```
#### and, or
```shell
scm> (define x 15)
x
scm> (and (> x 10) (< x 20))
#t
scm> (or (< x 10) (> x 20))
#f
```
# Types
## Types of value
### undefined
There is also an undefined value that can be returned by some builtin procedures. This value behaves similarly to None in Python. If an expression entered into the REPL evaluates to undefined, it is not printed, just like Python. But the result of `(not undefined)` is `#f`, this is different from python.

## Type checking
Type checking functions all ends with question mark `?`.

Besides these built-in type checkers, it is a common practice in Scheme to name a function with a question mark at the end if the function returns a boolean value indicating whether or not a condition is satisfied. For instance, ascending? is a function that essentially asks "Is the argument in ascending order?", null? is a function that asks "Is the argument nil?", even? asks "Is the argument even?", etc.


### null?
`(null? <arg>)`

Returns true if arg is nil (the empty list); false otherwise.

### atom?
`(atom? <arg>)`

Returns true if arg is a boolean, number, symbol, string, or nil; false otherwise.



# Pair and List Manipulation
```shell
(define (duplicate lst) 
    (let (
            (tmp (map (lambda (x) (list x x)) lst))
        )
        (cond 
            ((null? tmp) nil)
            (else (reduce append tmp))
        )
    )
)
```
## Basics
### car
`(car <pair>)`

Returns the car of pair. Errors if pair is not a pair.

### cdr
`(cdr <pair>)`

Returns the cdr of pair. Errors if pair is not a pair.

```shell
# return the rest excepting the first two elements
(define (cddr s) (cdr (cdr s)))

# return the second element
(define (cadr s) 
        (if (null? (cdr s)) undefined (car (cdr s))))
        
# return the third element
(define (caddr s) 
        (if (< (length s) 3) nil (cadr (cdr s)))
)

```
### cons
`(cons <first> <rest>)`

Returns a new pair with first as the car and rest as the cdr.

### list
`(list <item> ...)`
Returns a list with the items in order as its elements.

```shell
scm> (cons 1 (cons 2 nil))
(1 2)
scm> (cons 1 '(list 2 3))
(1 list 2 3)
scm> (cons 1 (list (cons 3 nil) 4 5))
(1 (3) 4 5)
```

## Useful built-in functions
### append
`(append [lst] ...)`

Returns the result of appending the items of all lsts in order into a single list. Returns nil if no lsts.

```shell
scm> (append '(1 2 3) '(4 5 6))
(1 2 3 4 5 6)
```
### reduce
`(reduce <combiner> <lst>)`

Returns the result of sequentially combining each element in lst using combiner (a two-argument procedure). reduce works from left-to-right, with the existing combined value passed as the first argument and the new value as the second argument. lst must contain at least one item.
### map
`(map <proc> <lst>)`

Returns a list constructed by calling proc (a one-argument procedure) on each item in lst.

### length
`(length <arg>)`

Returns the length of arg. If arg is not a list, this will cause an error.



## Mutation
### set-car!
`(set-car! <pair> <value>)`

Sets the car of pair to value. pair must be a pair.
```shell
scm> (define x (list 1 2 3))
x
scm> x
(1 2 3)
scm> (set-car! x 10)
scm> x
(10 2 3)
```