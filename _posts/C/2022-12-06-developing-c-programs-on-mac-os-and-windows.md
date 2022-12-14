---
layout: post
title: Developing C programs on Mac OS and Windows
date: 2022-12-02
categories: [computer science]
tags: [C, editor, compiler]
excerpt: Setup C environment on your computer
---
# Mac OS
## Editor
- vim
- Sublime text
## Compiler
- clang
- gcc
## IDE
- Dev C++ (recommended on Windows)
- XCode (recommended on Mac OS)


## Example with editor and compiler
To create a "hello world" program.
### Editing
In Sublime, open a new file, save it as `hello.c`, then the sublime will set the language environment as C for you.
```c
#include<stdio.h>
int main(void){
    printf("hello, world\n");
    return 0;
}
```
To compile and run this file, use shortcut `Command + B`. Then you will find an executable file `hello`, which is the result of compiling, is created in the same file.
Sublime itself doesn't have compiler, it uses external compiler. Moreover, **Sublime can't handle inputs**.

`Command + B` helps you compile and run the program at the same time, if you want to compile and run programs separately by yourself, use clang or gcc:

First edit the program in Sublime, then run `clang -o hello hello.c` in terminal to compile the program and create executable file `hello`. Actually, you can use `clang hello.c` only, but it will assign a name for the executable middle file, such as `a.out`.

In order to run the program, `./hello` or `./a.out`.

Except light editor like Sublime, you can use preinstalled vim in terminal. Run `vi hello.c` to open the file with Vim, then press `I` to start editing, press `esc` and input `:wq` to quit editing, save what you write and exit Vim.
To learn more about Vim, MIT course [Missing Semester](https://missing.csail.mit.edu/2020/editors/) is a good choice.

## Example with IDE
### Dev C++
Too simple, nothing to say, just try by yourself.
### VS Code
For people who prefer VS Code, make sure you have compiler(like clang) already installed. VS Code provides a very detailed [manual](https://code.visualstudio.com/docs/languages/cpp#_install-a-compiler) of how to install a compiler. Or you can see the last two section of this article.
> VS Code is first and foremost an editor, and relies on command-line tools to do much of the development workflow.

Besides this, you need to install C/C++ Extension in VS Code.

Open a terminal window in VS Code, Execute `code hello.c` to create a new file called `hello.c`.

If the `code` command doesn't work for you:
1. Make sure VS Code is in the Application folder.
2. Use shortcut `Command + Shift + P` to open the Command Palette. Enter `shell command`, choose "Install 'code' command in PATH".

After you finished programming in hello.c, execute `make hello` in terminal to compile it. Remember, it's `hello` not `hello.c`, only the name, no suffix.

Check the files by `ls -l`, there will be two files in this directory now, `hello.c` and executable `hello` which is the result of compiling. Finally, execute `./hello` to run the program.

## Install MinGW-x64 on Windows
1. Install [msys2-x86_64-20221028.exe](https://github.com/msys2/msys2-installer/releases/download/2022-10-28/msys2-x86_64-20221028.exe) from [MSYS2](https://www.msys2.org/#installation)
2. After installed, run MSYS2, in the window execute `pacman -S mingw-w64-ucrt-x86_64-gcc` to install gcc or `pacman -S --needed base-devel mingw-w64-x86_64-toolchain` to install the tool chain.
3. [Add MinGW compiler to your Path](https://stackoverflow.com/questions/5733220/how-do-i-add-the-mingw-bin-directory-to-my-system-path)
   1. Right-click "My Computer" and click System.
   2. In the System Properties window, click Advanced tab.
   3. Click the Environment Variables button. 
   4. In the Environment Variables window, in the User Variables section click PATH row. 
   5. Click New, and add your MinGW compiler path, for myself, it's `D:\msys64\mingw64\bin\gcc.exe`, `D:\msys64\mingw64\bin\g++.exe` and `D:\msys64\mingw64\bin\gdp.exe`. By the way, if you only add `D:\msys64\mingw64\bin`, the cmd can find them, but VS Code can't.
   6. Click OK. 
4. Check your MinGW installation. Open cmd, execute 
    ```shell
    gcc --version
    g++ --version
    gdb --version
    ```
   If you're able to check their versions, you've installed compilers successfully.
## Using GCC and GDB with MinGW in VS Code
1. Click Terminal, then click Configure Default Build Tasks, choose gcc in the dropdown menu.
2. In order to use `make` command in VS Code terminal, go to `mingw64\bin`, rename "mingw32-make.exe" as "make.exe". Otherwise, VS Code can't find it.
3. To run your program like "hello" in terminal, execute `.\hello` (not `./hello`).
4. To use debug, edit your launch.json.
   ```json
    // an example
    {
     "version": "0.2.0",
     "configurations": [
       {
         "name": "C/C++ Runner: Debug Session",
         "type": "cppdbg",
         "request": "launch",
         "args": [],
         "stopAtEntry": false,
         "externalConsole": true,
         "cwd": "d:/c_workspace",
         "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
         "MIMode": "gdb",
         "miDebuggerPath": "gdb",
         "setupCommands": [
           {
             "description": "Enable pretty-printing for gdb",
             "text": "-enable-pretty-printing",
             "ignoreFailures": true
           }
         ]
       }
     ]
   }
   ```