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

#### and, or
```shell
scm> (define x 15)
x
scm> (and (> x 10) (< x 20))
#t
scm> (or (< x 10) (> x 20))
#f
```











