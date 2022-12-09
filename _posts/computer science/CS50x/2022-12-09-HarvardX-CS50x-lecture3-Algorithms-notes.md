---
layout: post
title: HarvardX CS50x Lecture3 Algorithms Notes
date: 2022-12-09
categories: [computer science]
tags: [course, introduction to Computer Science]
excerpt: In this lecture, we’ll focus on algorithms that solve problems with arrays.
---

## Big O
In order to evaluate algorithm, the running time of the computation definitely is an important factor. `Big O`, which we can think of as “on the order of” something instead of an exact number of milliseconds or steps, is notation introduced to describe it.

Big $O$ represents the upper boundary of how many steps it takes in the worst case for our algorithm, while Big $\Omega$ represents the lower boundary of how many steps it takes in the best case for our algorithm. When the Big $O$ and Big $\Omega$ are the same, we represent the running time by another notation Big $\Theta$.

Common notations:
* $O(1)$, $\Omega(1)$, $\Theta(1)$
* $O(log_{2}^{n})$, $\Omega(log_{2}^{n})$, $\Theta(log_{2}^{n})$
* $O(n)$, $\Omega(n)$, $\Theta(n)$
* $O(nlog_{2}^{n})$, $\Omega(nlog_{2}^{n})$, $\Theta(nlog_{2}^{n})$
* $O(n^2)$, $\Omega(n^2)$, $\Theta(n^2)$

What does the `n` represent? For example, when analyzing the Big-O performance of sorting algorithms, n typically represents the number of elements that you're sorting.
## Searching algorithms
### Linear search
Iterate across the array from left to right, searching for a specified element.

Time complexity: $O(n)$. Because in the worst scenario, the target element we want is at the last position in the arrat.

### Binary search
Binary search is a divide-and-conquer algorithm **for sorted arrays**, which means it reduces the search area by half each time, trying to find a target element.

Pseudocode:
```c 
If no elemnt in the array
    Return false
If the target element == array[middle]
    Return true
Else if the target element < array[middle]
    Search array[0] through darray[middle - 1]
Else if the target element > array[middle]
    Search array[middle + 1] through array[n - 1], where n is the length of array
```

The time complexity is $O(logn)$. Because in the worst scenario, you have to divide and check the array many times until there is no more element left in the array.

# References
1. [CS50X lecture notes](https://cs50.harvard.edu/x/2022/notes/3/#big-o)
2. [Big O](https://stackoverflow.com/questions/23974589/what-is-the-n-in-big-o-notation)



