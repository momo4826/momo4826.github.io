---
layout: post
title: Getting Started with Github, Sphinx and ReadtheDocs
date: 2022-11-27
categories: [website]
tags: [personal website, github, sphinx, readthedocs]
excerpt: How to build a personal documentation project with Sphinx, Github and ReadtheDocs.
---

### Why
Deep Learning is a fast-growing field with too many models(papers), methods, algorithms and applications. It's easy to forget what you've learned or mix things up if you don't take notes. And documentation is a very good way to collect knowledge, organize notes and share thinking about deep learning. That's why I choose to build a documentation with Sphinx, Github and ReadtheDocs.
### What
This is my [Deep Learning Notes](...) documentation, very welcome to visit and share your thoughts through Github fork of the project.
### How
Actually, I met many errors(from powershell and ReadtheDocs platform) during building this website, this is the simplest way:
1. Install Sphinx through pip.
   1. (better to do)create a new environment for your project using conda.
   ```shell
    conda create -n myenv python=3.7 # choose your own environment name and python version
    conda activate myenv
    ```
   2. install the library
   ```shell
   #if you're in China, because of Great Firewall, use "pip install sphinx -i https://pypi.tuna.tsinghua.edu.cn/simple/" instead.
    pip install sphinx 
   ```
2. Start a project
   ```shell
    sphinx-quickstart
    ```
    You will be asked several questions to finish the initialization:
    ```shell
   Separate source and build directories (y/n) [n]: y
   Project name: your_project_name
   Author name(s): your name
   Project version: 1.0.0
   Project language [en]:en
    ```
3. Create a new page
   1. fisrt, a new rst file
Let's create a rst file called "hello.rst" under *source* directory.
 Write as follows (actually, this is the rst grammer you must know):
    ```text
    This is a Title
    ===============
    That has a paragraph about a main subject and is set when the '='
    is at least the same length of the title itself.
    
    Subject Subtitle
    ----------------
    Subtitles are set with '-' and are required to have the same length
    of the subtitle itself, just like titles.
    
    Lists can be unnumbered like:
    
     * Item Foo
     * Item Bar
    
    Or automatically numbered:
    
     #. Item 1
     #. Item 2
    
    Inline Markup
    -------------
    Words can have *emphasis in italics* or be **bold** and you can define
    code samples with back quotes, like when you talk about a command: ``sudo``
    gives you super user powers!
    ```
   
4. Add a Table of Contents in the index page
   ```text
    Contents:
    .. toctree::
       :maxdepth: 2
       :numbered:
    ```
5. Build the html files
    ```shell
    make html
    ```
    Then we can see there are two new directories under build directory--- doctrees and html.
    Now you can just open the html files to see what your website is like.
6. Upload your project to Github
   1. Create a new public repository on your Github
   2. Connect your local project with this repository
   ```shell
    # in case you're already in the project root directory
   git init
   git branch -M main
   git clone git@github.com:yourgithubaccount/yourrepositoryname.git
   git add .
   git commit -m "init"
   git push origin main
    ```
7. Connect your Github with ReadtheDocs
   1. Sign up [ReadtheDocs(click)](https://readthedocs.org/) by "Sign up with Github" and authorize it.
   2. click "import a project"
   3. choose a repository from you github repository list
   4. click next, then build
8. Dalaaa! Now you have your documentation that you can edit locally, push to Github and build on ReadtheDocs.

 
