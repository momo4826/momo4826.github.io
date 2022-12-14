---
layout: post
title: Small but important things about C
date: 2022-12-09
categories: [computer science]
tags: [c language]
excerpt: There are so many small but import things about C that we maybe don't know but will bring "disaster" during program.
---

# Operator-relevant
## sizeof
From the [C99](https://www.open-std.org/JTC1/sc22/wg14/www/docs/n1256.pdf) Standard 
> The sizeof operator yields the size (in bytes) of its operand, which may be an expression or the parenthesized name of a type. The size is determined from the type of the operand. The result is an integer. If the type of the operand is a variable length array type, the operand is evaluated; **otherwise, the operand is not evaluated and the result is an integer constant**.

Example:

The result is 10.
```c 
    int i=10;
    long long t = sizeof(i++);
    printf("%d", i);
```

By the way, `sizeof(x)` is used to calculate how much memory x takes up. If `x` is an integer array whose elements are all `int`, `sizeof(x)/sizeof(x[0])` returns the length of the array. However, if array is passed in as a function parameter, you can do it in this function body to it.
## comma ,
The comma operator in c comes with the lowest precedence, and  has left-to-right associativity.

Example:

The result is `9 1 20`.
```c
    int i,x,y;	
    i=x=y=0;
    do {
        ++i;
        if ( i%2 ) 
            x+=i, 
        i++;
        y +=i++;
    } while ( i<=7 );
    printf("%d %d %d", i, x, y);
```

## &&
AND operator is left-to-right, if left expression is false, the right ones will not be executed.

Example:

The result is 0.
```c 
    int x=0, y=0, z=0;
    z = (x==1) && (y=2);
    printf("%d ", y);
```

# Data type
## char
Remember, char is signed!

> char is used for variables that will store only one character. It always takes up 1 byte(8 bits) of memory, which means the range of values they can store is limited to 8 bits of information(-128 - 127).

Example:

The result is -1.
```c 
    char ch = -1;
	printf("%d\n", ch);
```
# Control flow
## if else
`else` should follow after `if`. In the code below, there are two expressions (the second one is empty) not included in curly braces. So the nearest expression before `else` is an empty expression instead of `if` expression, which will raise compiling error.
```c 
    if ( i<= 6 ) 
		printf("hello\n");;
	else
		printf("bye-bye\n");;
```
# Array
## Initialization
`int my_array[10] = {2};` will initialize the elements at index 1-9 to be 0 by default.

More fancy way in C99, you can do `int my_array[10] = {[1]=2, [5]=3}` to assign 2 to second element, assign 3 to the sixth element, and the rest will be 0.
# Number system
## Octal number system
When you see an integer variable starting with `0`, it's an octal number, which has its base as 'eight'.

Example:

The result is 10.
```c 
    int x=1, y=012;
    printf(“%d”,y*x++);
```

# compilation
`#include`/`#define` is instruction of compiler, not a part of C language.
# References
1.[HarvardX-CS50x notes](https://github.com/momo4826/HarvardX-CS50x)