---
layout: post
title: HarvardX CS50x Lecture1 C Notes
date: 2022-12-02
categories: [computer science]
tags: [course, introduction to Computer Science]
excerpt: This lecture is an introduction to C
---
This lecture includes all basic knowledge about C -- data types, operators, conditional statements, loops and overflow.

## Data types
In C, you need to declare the data type for all variables. But not all languages are like this, some modern languages like python or javascript don't need this.


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

4003600000000014