---
layout: post
title: More about Pointers
date: 2022-12-14
categories: [computer science]
tags: [pointers, course]
---
# Pointers to sophisticated types
## Pointers to Structs
Pointers can be a part of structs. and we can create a pointer pointing to a struct variable.

From the code below we can see, `.` takes precedence over `*`, which means `*x.p` first executes `x.p` then dereference it.

You can write `z->q` as a shorthand for `(*z).q`. Operator `->` dereferences a pointer to a struct and selects a field in it.
```c 
    typedef struct{
        int *p;
        int q;
    }type_a;
    
    int x = 3;
    type_a y;
    type_a *z;
    y.p = &x;
    y.q = 5;
    z = &y;
    
    int m = *x.p;//3
    int n = (*z).q;//5
    
```
## Pointers to Pointers
Remember that `*` in declaration is a part of the type name, it tells us what type our pointer will point to. Here, `int*` means `y` points to a box of variable with `int` type; `int**` means `z` points to a pointer who points to variable with `int` type; and `int***` means `t` points to a pointer which points to a pointer pointing to a `int` variable. (I think we can consider pointers to pointers such as `int*** t` like this `((int*)*)* t` for better understanding). So when `*` is used for dereferencing, `***t` is actually 3, the value of x.
```c 
    int  x = 3;
    int *y = &x;
    int **z = &y;
    int ***t = &z;
```
> Notice how the types work out ( i.e. match up so that the compiler type check the program). Whenever we take the address of an lvalue of type T, we end up with a pointer of type T * (e.g., p has type int *, so &p has type int **). Whenever we take the address of something, we “add a star” to the type. This rule makes intuitive sense, because we have a pointer to whatever we had before.


## const
`const int* p` means the pointer `p` points to a box which is constant(you can think it as (const int)* p). That means the value of the box pointed by `p` cannot be changed. But we can change the box that `p` points to.

`int const *p` is the same as `const int *p`(the two `const`s both describes the box pointed by `p`).

However, `int* const p` is different. It means the box `p` points to is with type `int`, its value can be changed; while the pointer `p` itself is constant, which means the address `p` points to can not be changed.

### (const)pointers to (const)pointers
Tricky ones:
* `const int *const *p` means that `p` itself is not constant, it points to a constant pointer(because of `*const`, first `*` then `const`) that points to a box with `const int` type. So,
  * `p` is not constant, so `p` can be changed.
  * the box `p` pointing to is constant, so `*p` cannot be changed.
  * the box `*p` pointing to is constant, so `**p` cannot be changed.
* `const int ** const p`
  * `p` is constant, so `p` cannot be changed.
  * the box `p` pointing to is not constant, so `*p` can be changed.
  * the box `*p` pointing to is constant, so `**p` cannot be changed.
* `int *const*const p`
  * `p` is constant, so `p` cannot be changed.
  * the box `p` pointing to is constant, so `*p` cannot be changed.
  * the box `*p` pointing to is not constant, so `**p` can be changed


<figure align = "center">
    <img src = "/assets/images/computer%20science/const_pointer_1.png">
    <figcaption>figure from <a href="https://www.coursera.org/learn/pointers-arrays-recursion/supplement/CG1qU/const">Coursera course</a></figcaption>
</figure>

### where is `const` declared
Case 1 is legal. `p` is declared as a pointer pointing to box with const int type, so we cannot change the value of x by `*p`. However, the `x` variable is not declared as constant, so we can change the value of it by assigning to `x`.

Case 2 is illegal. `int * q = &y;` means `q` points to a box whose type is not constant. However, `y` is a constant variable. So it will raise compiler warning.
```c 
  //case 1
  int x = 3;
  const int * p = &x;
  x = 4;
  //case 2
  const int y = 3;
  int * q = &y;
  *q = 4;
```

# Pointer Arithmetic
The rules of arithmetic among pointers and other variables like integers are the same, but the arithmetic has different meaning.

For example, `adding 1` means getting `one larger` for integers, but has the semantics of `one integer later in memory` for integer pointers. However, after that, you probably don't know where your pointer is pointing to, which is dangerous.

# Valgrind
> Now that you are starting to use pointers, it is crucial to use memory checker tools, such as valgrind. These will help you find erroneous behavior, and make fixing your program easier. Use them all throughout the testing process.

In order to use Valgrind to check `test.c` in your current directory, first compile it then execute `valgrind ./test` where `test` is executable.























