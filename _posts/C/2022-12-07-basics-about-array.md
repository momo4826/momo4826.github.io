---
layout: post
title: Basics about Array
date: 2022-12-07
categories: [computer science]
tags: [course, introduction to Computer Science]
excerpt: This lecture covers compilation process, how to debug, data structure--array, data type string, user-defined functions and command line arguments.
---
## Compilation process
There are two method to execute a program, interpretation and compilation. Technically, **every language can be interpreted or compiled**. Some languages are called as compiled languages like C, just because we are used to compile it, of course, you can build an interpreter for it.

Here we focus on the process of compilation, and separate it as 4 steps.
### preprocessing
Preprocessing is the first step. The preprocessor obeys commands that begin with # (known as directives) by:
* removing comments
* expanding macros
* expanding included files

All the statements starting with # (hash) symbol are known as **preprocessor directives**/commands therefore, #define and #include are also known as preprocessor directives. Preprocessor directives are executed before any other command in our program. The #define directive is used to define constants or an expression in our C Program, while #include directive is used to include the content of header files in our C program. The process of importing such files that might be system-defined or user-defined is known as **File Inclusion**.
### compiling
**It takes the output of the preprocessor and generates assembly language**, an intermediate human-readable language, specific to the target processor.

The compiling result can differ on different systems. Because the instruction sets of them are different. So sometimes companies like Microsoft will compile their programs twice, one for PC or for Mac.

### assembling
**The assembler will convert the assembly code into pure binary code or machine code (zeros and ones)**. This code is also known as object code.

### linking
**The linker merges all the object code from multiple modules into a single one**. If we are using a function from libraries, linker will link our code with that library function code.

In static linking, the linker makes a copy of all used library functions to the executable file. In dynamic linking, the code is not copied, it is done by just placing the name of the library in the binary file.
## Debug
You can debug by manually printing relevant variables. 

Or Use Debugger in IDE like VS Code and Dev C++. By adding breakpoints, you can clearly see what's going on in every step of your program and find the "bug". There are two properties of Debugger: **Step Over and Step Into**. If the current line contains a function call, Step Over runs the code and then suspends execution at the first line of code after the called function returns. While Step Into will step into the function line by line.

And of course, you can use the Rubber Duck Debugging method, which is a method of debugging code by articulating a problem in spoken or written natural language.

## Array
### What are arrays?
**Array, used for holding values of the same type at contiguous memory locations, is a fundamental data structure**. We can consider array as a container that containing elements of the same data type.

In C, the elements of an array are indexed starting from 0. If an array consists of n elements, the first element is located at index 0, the last element is located at index n-1.

Actually C is the first language whose array index is from 0. That's for the convenience of compiler design.
### Array declaration, initialization, assignment and access its elements
Array declaration is like `type array_name[array_size]`, in array initialization, `array_size` doesn't have to be indicted, so it's like `int array_name[] = {1, 2}`. `array_size` can be a variable after C99.

**Once the size of the array is set, it can not be changed**.

If you want to get the single element located at index 2 in an array `my_array`, you can call `my_array[2]`, it's the third element in the array. Be careful, the index has to be less than the size of the array.

Arrays can consist of more than one dimension, i.e. `char my_dict[2][3] = {"bye", "bob"}`. You can think it's a 2x3 grid of cells. **In memory though, it's really just 1 100-element one-dimensional array**. 

While we can treat individual elements of arrays as variables, **we cannot treat entire arrays as variables, which means we can't assign an array to another array**.
### Passed to functions by reference
**When we pass a variable to functions, we pass a copy of it. While it is not the case with arrays. Rather, they are passed by reference. So the outputs of the code below are**:
```text
10 22
```
That's because in `set_int()` function the passed in parameter is a copy of `a`'s value, so it won't change `a` itself. However, in `set_array` function array is passed by reference, if you do assignment in the function, the parameter(the array) will be changed forever.
```c 
    #include<stdio.h>
    void set_array(int array[4]);
    void set_int(int x);
    int main(void)
    {
        int a = 10;
        int b[4] = {1, 2, 3, 4};
        set_int(a);
        set_array(b);
        printf("%d %d\n", a, b[0]);
    }
    void set_array(int array[4])
    {
        array[0] = 22;
    }
    void set_int(int x)
    {
        x = 22;
    }
```
What does it mean that the array is passed by reference? See the code below.
The outputs are :
```text
Array size inside main() is 8
Array size inside fun() is 1
```
The reason how it works will be mentioned later.
```c 
    #include <stdio.h>
    #include <stdlib.h>
    // Note that arr[] for fun is just a pointer even if square
    // brackets are used
    void fun(int arr[]) // SAME AS void fun(int *arr)
    {
    unsigned int n = sizeof(arr)/sizeof(arr[0]);
    printf("\nArray size inside fun() is %d", n);
    }
    
    // Driver program
    int main()
    {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8};
    unsigned int n = sizeof(arr)/sizeof(arr[0]);
    printf("Array size inside main() is %d", n);
    fun(arr);
    return 0;
    }
```
## string
In order to use string data type, you need first use `#include<string.h>` in your program, because string is not a built-in data type in C.

The last space of string stores null character `\0` as delimiter, that's shorthand notation of 8 zero bits `00000000`. This design is to indicate how much space the string variable takes up for the reason that the memory of the string variable is not fixed.
## Functions
### What is a function?
A function is a block of code with 0 or more inputs and 0 or 1 ouput.

### Why use functions?
* Organization
  break up a complicated problem into more manageable sub-parts.
* Simplification
  smaller parts are easier to design, implement and debug.  
* Reusability
  once written, it can be used as often as you need.
### Function declarations
Declare the functions you defined at the top of the program right before writing `main` function. Only by this, the compiler can know this function truly exist when you call it in your main function. 

You can put the function definitions before main function, so you don't have to declare it separately. But this will make your program design very "heavy" because then main function will be in the middle position of the program, which means programmers can't directly know the main purpose of your program. So this is a bad design. Keep put function declarations before main function and put the function definations after main function.
### Function definitions
To specify what the function does.

Example:
```c
    float mult_two_reals(float x, float y);//declaration
    float mult_two_reals(float x, float y)
    {
        return x*y;
    } //definition
```
You may notice that the function declarations and function definitions are almost identical, except:
* a declaration is with a semicolon behind.
* a definition has a main body included in curly brackets.
## Command Line arguments
Instead of `int main(void)` we usually use, we can declare the main function as `int main(int argc, string argv[])`.

`int argc` tells you how many arguments the command line provided. `string argv[]` tells you what exact data the command line passed in.

When you execute `./my_code` the argc is 1 because `./my_code` also count. If you execute `./my_code arg1 arg2` then the argc is 3 now. 
The command line arguments are separated by white spaces like blank spaces or tabs.


# References
1. [#define and #include in C](https://www.scaler.com/topics/c/define-and-include-in-c/)
2. [How the Compilation Process Works for C Programs](https://medium.datadriveninvestor.com/compilation-process-db17c3b58e62)
