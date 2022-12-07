---
layout: post
title: HarvardX CS50x Lecture2 Array Notes
date: 2022-12-07
categories: [computer science]
tags: [course, introduction to Computer Science]
excerpt: 
---

## Compilation process
There are two method to execute a program, interpretation and compilation. Technically, every language can be interpreted or compiled. Some languages are called as compiled languages like C, just because we are used to compile it, of course, you can build an interpreter for it.

Here we focus on the process of compilation, and separate it as 4 steps.
### preprocessing
Preprocessing is the first step. The preprocessor obeys commands that begin with # (known as directives) by:
* removing comments
* expanding macros
* expanding included files

All the statements starting with # (hash) symbol are known as **preprocessor directives**/commands therefore, #define and #include are also known as preprocessor directives. Preprocessor directives are executed before any other command in our program. The #define directive is used to define constants or an expression in our C Program, while #include directive is used to include the content of header files in our C program. The process of importing such files that might be system-defined or user-defined is known as **File Inclusion**.
### compiling
It takes the output of the preprocessor and generates assembly language, an intermediate human-readable language, specific to the target processor.

The compiling result can differ on different systems. Because the instruction sets of them are different. So sometimes companies like Microsoft will compile their programs twice, one for PC or for Mac.

### assembling
The assembler will convert the assembly code into pure binary code or machine code (zeros and ones). This code is also known as object code.

 The linker merges all the object code from multiple modules into a single one. If we are using a function from libraries, linker will link our code with that library function code.

In static linking, the linker makes a copy of all used library functions to the executable file. In dynamic linking, the code is not copied, it is done by just placing the name of the library in the binary file.
### linking

# References
1. [#define and #include in C](https://www.scaler.com/topics/c/define-and-include-in-c/)
2. [How the Compilation Process Works for C Programs](https://medium.datadriveninvestor.com/compilation-process-db17c3b58e62)
uage)