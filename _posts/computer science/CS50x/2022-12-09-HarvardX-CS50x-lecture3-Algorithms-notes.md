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

## struct
If we want to create a dictionary like {2:"apple", 5: "banana"} or {"apple":2,"banana":5} to bind the names of fruit and their prices together, in Python we can just use the data structure `dict`, but in C we can use `struct` to create data type like `dict` by ourselves.

There are many ways to declare, define and use structs. The figure below shows four options, you can use any of them during programming.
<figure align="center">
    <img src = "/assets/images/computer%20science/struct_1.png">
    <figcaption>figure from <a href="https://www.coursera.org/learn/programming-fundamentals/supplement/9LmqH/structs">Coursera course</a> by Duke University</figcaption>
</figure>

The code below defines a struct without declaring the struct tag name, and then instantiates a variable `fruit` with this data type Fruit. In the following program, you can directly use this variable like `if (fruit[1].price == 1)`.
```c 
    typedef struct{
        char *name;
        int price;
    }Fruit
    Fruit fruit;
```
We can also see code below, it seems like not any way in the four options, but it can be compiled and ran correctly.
```c 
    struct{
        char *name;
        int price;
    }fruit[] = {
        {"apple", 2},
        {"banana",5}
    };
```
Now we put all related data about fruit together, in computer science this process is called **encapsulation**, which can encapsulate several pieces of information into the same data structure

You can also just use two arrays like array_a = {2, 5} and array_b = {"apple", "banana"} to describe the same thing, when you want to buy banana which is at index 1 in array_b, just check array_a[1] for its price. However, it's not efficient from the point of cache. If the memory cell of banana's price is just near the one of banana, it will take use 1 step to get the value. But if you store fruit names and fruit prices in two arrays, given that array means continuous memory space, banana and banana's price cannot be put together, which leads to inefficiency.
## Recursion
The recursion function is the one that, as part of its execution, invokes itself.

Every recursion function has two cases that could apply, given any input:

* **the base case**, which when triggered will **terminate** the recursive process. It makes sure that we won't call the function over and over again. Without base case, we'll get a segmentation fault, which means that we’ve touched memory in our computer.
* the recursive case, which is whre the recursion will actually occur.
## Sort
Very good [visualization](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html) of sort algorithms by CS50X. Highly recommended!

Comparison:
* Selection sort performs a smaller number of swaps compared to bubble sort; therefore, even though both sorting methods are of $O(n^2)$, selection sort performs faster and more efficiently!

| Methods        | Descriptions                                                                                                                                                                    | Lower bound | Upper bound |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-------------|
| Bubble sort    | * compares pairs of adjacent values one at a time<br>* swaps them if they are in the incorrect order                                                                            | $\Omega(n)$    | $\O(n^2)$   |
| Selection sort | * iterates through the unsorted portions of a list <br> * select the smallest element each time and moving it to its correct location.                                          | $\Omega(n^2)$  | $O(n^2)$    |
| Insertion sort| moves down through the array, swap elements to make sure everything on the left of the current item is in order(while everything on the right of the current item is untouched) | $\Omega(n)$| $O(n^2)$|
| Merge sort     | *  recursively divides the list into two repeatedly<br>* merges the smaller lists back into a larger one in the correct order                                                   | $\Omega(nlogn)$ | $O(nlogn)$    |

### Bubble sort

pseudocode:
```c 
    Set swap counter to a non-zero value
    Repeat until the swap counter is 0:
        Reset swap counter to 0
        For i from 0 to n–2
            If numbers[i] and numbers[i+1] out of order
                Swap them and add one to swap counter
```
Notice, you need to first initialize the swap counter variable as a non-zero value, because we make sure the array is already sorted by the swap counter being 0(which means no need to swap any elements in the array).

Time complexity: $O(n^2)$(`(n-1)*(n-1)`) and $\Omega(n)$.

### Selection sort
If you want to sort the array from the smallest to the biggest, selection sort can do this by finding the smallest unsorted element and swapping it with the first element of the unsorted part until no unsorted elements remain.


pseudocode:
```c 
    For i from 0 to n–1
        Find smallest number between numbers[i] and numbers[n-1]
        Swap smallest number with numbers[i]
```
For this algorithm, we started with looking at all n elements, then n-1, then n-2, ... and finally 1.
So the steps we take are calculated as `n + (n-1) +(n-2)+...+1 = (n+1)*n/2`.

Therefore, the time complexity: $O(n^2)$ and $\Omega(n^2)$. Eeven in the best-case scenario we have to go through all array for n times. Because there's no way to guarantee the array is sorted until we go through for all elements.

### Insertion sort
Insertion sort is kind of like Bubble sort but faster. It moves down through the array, swap elements to make sure everything on the left of the current item is in order(while everything on the right of the current item is untouched).

Time complexity: $O(n^2)$, $\Omega(n)$.
### Merge sort
Take the idea of recursion to sorting with Merge Sort, which sorts smaller arrays and then combines
those arrays together(merge them) in sorted order.

Pseudocode:
```c
    If only one number
      Quit
    Else
        Sort left half of number
        Sort right half of number
        Merge sorted halves
```
Time complexity: $O(nlog_{2}n)$, $\Omega(nlog_{2}n)$.

More memory to merge new lists but shorter running time.
<!--### Quick sort
Pseudocode:
1. Shuffle the array
2. Find a position i, partition the array at i, so that
    * no larger element to the left of j
    * no smaller element to the right of j
3. Sort left part and right part by recursion
### Shell sort
-->

## Problem sets
The main ideas of three algorithms about election.

Structs and sort methods are used.
### Plurality
* define `struct{string name; int votes}` to store vote results.
* use function `vote` to count votes for candidates from voters.
* use function `printf` to sort the candidates by their votes and print the winner.
### Run off
* declare a 2-dimensional array `preferences`, and use function `vote` to store voters' ranked-votes in `preferences`.
* define `struct{string name; int votes; bool eliminated}candidate`, declare a `candidate` array, and use function `tabulate` to count votes for non-eliminated candidates by `preferences`.
* use function `eliminate` to eliminate candidates with the fewest votes by assigning true to their `eliminated` attributes.
* use function `printf` to find the winner with votes that are more than 50% of number of voters.

### Tideman
* declare a 2-dimensional array `preferences` to store the vote ratio between each two candidates; use function `vote` and `record_preference` to calculate `preferences`.
* declare a string array `candidates` to store candidates' names.
* define a `struct{int winner; int loser}pair`; declare a `pair` array `pairs` to indicate the votes between a pair of candidates; use function `add_pairs` to add pairs to `pairs` by `preferences`; then use function `sort_pairs` to sort the pairs in decreasing order by the votes of `winner` in a pair.
* declare a 2-dimensional array `locked` to represent a directional graph that indicates who is the winner; use function `lock_pairs` to build a directional graph by adding all edges in decreasing order of victory strength so long as the edge would not create a cycle.
* use function `printf` to find the source in the directional graph. Source means no edge is directing to it, it's a sign of winning. Finally, print the winner.
# References
1. [CS50X lecture notes](https://cs50.harvard.edu/x/2022/notes/3/#big-o)
2. [Big O](https://stackoverflow.com/questions/23974589/what-is-the-n-in-big-o-notation)
3. [struct options](https://www.coursera.org/learn/programming-fundamentals/supplement/9LmqH/structs)
4. [Cousera course Computer Science: Algorithms, Theory, and Machines by Princeton](https://www.coursera.org/videos/cs-algorithms-theory-machines/1I0fY)











