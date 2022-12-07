---
layout: post
title: HarvardX CS50x Lecture1 C Notes
date: 2022-12-05
categories: [computer science]
tags: [course, introduction to Computer Science]
excerpt: This lecture is an introduction to C
---
This lecture includes all basic knowledge about C -- data types, operators, conditional statements, loops and overflow.

## Data types and types
In C, you need to declare the data type for all variables. But not all languages are like this, some modern languages like python or javascript don't need this.

### int
The `int` data type is used for variables that will store integers.
Integers always take up 4 bytes of memory, which means 32 bits(8 bits = 1 byte). That limits the range of values that variables with `int` data type can store to `-2^31 - 2^31-1` (half for negative, half for positive, and don't forget 0). 

If you want to double the range of values, you can use `unsigned int`, whose range is `0 - 2^32-1`. `unsigned` is a *qualifier* that can be applied to certain data types(`int`, `long`, `float`, `double`). It efficiently doubles the range positive range of values of that type, at the cost of disallowing negative values.

There are some results of power of two that are good to know.
```text
    2^7 = 128
    2^8 = 256
    2^31 = 2147483648, which is about 2 billion
    2^32 = 4294967296, which is about 4 billion
```
### char
`char` is used for variables that will store only one character. It always takes up 1 byte(8 bits) of memory, which means the range of values they can store is limited to 8 bits of information(`-128 - 127`).

Thanks to ASCII, we've developed a mapping of characters like A, B, C, ... to numeric values in the positive side f this range. For example, 'A' is mapped to 65, 'a' is mapped 97, '0' is mapped 48.

### float and double
`float` and `double` are used for variables that will store floating-point numbers, as known as real numbers.
`float` variable takes up 4 bytes(32 bits) of memory, while `double` variable takes up to 8 bytes(64 bits). So `double` is double precision comparing to `float`, which means it allows us to specify much more precise real numbers with additional 32 bits.
### bool (not build-in)
`bool` is used for variables that will store a Boolean value: true or false. Actually `bool` is not a default data type in C. So if you want to use it, add `#include <stdbool.h>`, or in this course `#include <cs50.h>`.
### structs and typedefs
Structures(structs) and defined types(typedefs) can afford great flexibility in creating data types you need.
### qualifiers
- `unsigned`
- `const`

### void
`void` is a type, but not a data type. Functions can have a void return type, which just means they don't return a value.
The parameter list of a function can be `void`, which just means the function takes no parameters.
### Use the data types
```c
    int number; //declaration
    number = 10; //assignment
    float height = 7.5; // initialization
    height = height + 1; // expression
```
## Operators
Expressions = Operators + Operands.(assignment `=` is also taken as an operator in C)

### Arithmetic operators
- add(+)
- substract(-)
- mutiplu(*)
- divide(/)
- modulus(%)

Shorthands that can be applied to all five arithmetic operators:
```c 
    x += 1; // a shorthand for x = x + 1
    x++; // a further shorthand for x = x + 1
```
Notice this situation:
```c
    x *= y + 2; // it's actually x = x * (y + 2)
```
**Differences when `++`/`--` as prefix and postfix:**

Take `++` as an example, `--` is the same.

- Both prefix `++` and postfix `++` can add 1 to the operand.
- But the result of the prefix `++` operation is the value of the operand that has been added 1.
- While the result of postfix `++` operation is the value of the operand before the operation.
```c 
    int a=14;
    int t1 = a++; // t1 = 14
    int t2 = ++a; // t2 = 16
```

One more thing about operations, the calculation result of two integers is still integer(the decimal part will be thrown away). But in calculation of an integer and a floating-point number, the integer will be transformed to a floating-point number.
### Boolean expressions
Every nonzero value is equivalent to true, and zero is false.

Two main types of Boolean expressions: logical operators and relational operators.
#### Logical operators
- AND(&&)
- OR(||)
- NOT(!)
#### Relational operators
- less than (x < y)
- less than or equal to (x <= y)
- greater than (x > y)
- greater than or equal to (x >= y)
- equality (x == y)
- inequality(x != y)

### [C Operator Precedence and Associativity](http://www.eecs.northwestern.edu/~wkliao/op-prec.htm)

<p align = 'center'>
    <img src = "./assets/images/computer%20science/operator_precedence_associativity.png">
</p>

## Conditional Statements
### if else
`if(1<n<10)` doesn't mean the situation where n is more than 1 and less than 10. This operation will be calculated as:
1. `(1<n)<10`(assume n = 5);
2. `1<10`(because n is truly more than 1, so the result of `1<n` is 1);
3. `1`(because 1 is truly less than 10, so the result of `1<10` is 1).

If you want to express "1<n<10" in C, use `1<n && n < 10` instead.

There is a cute trick of "if else" conditional statements: ternary operator. For example, `int x = (expr)?5:6`, it means if the expression is true, then `x = 5` else `x = 6`.
### switch
`switch` statement is also a conditional statement that permits enumeration of discrete cases, instead of relying on Boolean expressions.

In the example below, `x` is 2, first it meets `case 1`, apparently it's not the case, so it continue going down and meets `case 2`, it satisfied, so it will execute the code in `case2`.

The `break` is very important between each case, or you will "fall through" each case.

If `x = 3`, it doesn't satisfy `case 1` and `case 2`, so it will go to the bottom, the default "case" will be triggered.
```c 
    int x = 2;
    switch(x)
    {
        case 1:
            printf("ONE\n");
            break;
        case 2:
            printf("TWO\n");
            break;
        default:
            printf("BAD"\n);
    }
```
## Loops
- while(expr)
    
    use when you want a loop to repeat an unknown number of times, and possibly not at all
- do{}while(expr)

    use when you want a loop to repeat an unknown number of times, but at least once
- for(int i = 0; i < 10; i++)

    use when you want a loop to repeat a discrete number of times
## Comments
- `//` is for single-line comments
- `/* */` is for multi-line comments
## Others
If some functions are very complicated and/or have high frequency to be used, then we can write them into a file that we can include later into main files to quote these functions.

For example, in this course, cs50.h is a file that includes all functions we need, we add ```#include<cs50.h>``` in our main file in order to use the functions in it.

> ❓ Why it's cs50.h instead of cs50.c?
>
## Deal with Problem Set
Considering that this is the first real program you'll  write, compile, run and submit to CS50 online, I will walk you through the whole process by create and submit a "hello.c", which is the first problem in Problem Set 1.

In order to use the pipeline of CS50X, first please follow [this manual](https://cs50.harvard.edu/x/2022/new/#did-you-start-cs50x-in-2021-or-earlier) to set up your CS50 IDE and CS50 Codespace.

Now create a new file by execute `code hello.c` in terminal of online VS Code. Edit your program like:
```c
    #include<stdio.h>
    #include<cs50.h>
    int main(void)
    {
        // Enter a username
        string name = get_string("What's your name? ");
        // say hello to this user
        printf("hello, %s\n", name);
    }
```
Execute `check50 cs50/problems/2022/x/hello` to check your program.

![chek](/assets/images/computer%20science/cs50_editor_command_1.png)

Use `style50 hello.c` to evaluate the style of your code. It's very useful especially if you're new to Computer Science.

![style](/assets/images/computer%20science/cs50_editor_command_2.png)

To submit your work, execute `submit50 cs50/problems/2022/x/hello` in terminal.

![submit](/assets/images/computer%20science/cs50_editor_command_3.png)

Then you can see your work in `submit.cs50.io`.

# References
1. [edX course of CS50X](https://learning.edx.org/course/course-v1:HarvardX+CS50+X/block-v1:HarvardX+CS50+X+type@sequential+block@5a8092a9bea140d3b1bf752b2d1906a7/block-v1:HarvardX+CS50+X+type@vertical+block@d4cca38e12034cb1a70342f74bf1060c)
2. [Mooc course of C language](https://www.icourse163.org/learn/ZJU-199001?tid=1468796457#/learn/content?type=detail&id=1251282864&cid=1280257847)
3. [C Operator Precedence and Associativity](http://www.eecs.northwestern.edu/~wkliao/op-prec.htm)