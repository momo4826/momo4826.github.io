---
layout: post
title: Even Odd Inlist
date: 2023-01-15
categories: [Java]
tags: [Java]
---
## Exam Prep Discussion 3 from CS61B

Implement the method evenOdd by destructively changing the ordering of a given
IntList so that even indexed links precede odd indexed links.

For instance, if lst is defined as IntList.list(0, 3, 1, 4, 2, 5), evenOdd(lst)
would modify lst to be IntList.list(0, 1, 2, 3, 4, 5).

You may not need all the lines.

Hint: Make sure your solution works for lists of odd and even lengths.

```java
public class IntList {
    public int first;
    public IntList rest;

    public IntList(int f, IntList r) {
        first = f;
        rest = r;
    }
    /** Exam Prep Discussion 3 */
    public static void evenOdd(IntList lst){
        if (lst == null || lst.rest == null){
            return;
        }
        IntList oddList = lst.rest;
        IntList second = lst.rest;
        while (lst.rest != null && oddList.rest != null){
            lst.rest = lst.rest.rest;
            oddList.rest = oddList.rest.rest;
            lst = lst.rest;
            oddList = oddList.rest;
        }
        lst.rest = second;
    }
    public static void main(String[] args) {
        IntList lst = IntList.of(0, 3, 1, 4, 2, 5);
        evenOdd(lst);
        System.out.println(lst.toString());
    }
    /** Return the size of the list using... recursion! */
    public int size() {
        if (rest == null) {
            return 1;
        }
        return 1 + this.rest.size();
    }


    /** Returns the ith item of this IntList. */
    public int get(int i) {
        if (i == 0) {
            return first;
        }
        return rest.get(i - 1);
    }

    /** Method to return a string representation of an IntList */
    public String toString() {
        if (rest == null) {
            // Converts an Integer to a String!
            return String.valueOf(first);
        } else {
            return first + " -> " + rest.toString();
        }
    }

    public static IntList of(int ...argList) {
        if (argList.length == 0)
            return null;
        int[] restList = new int[argList.length - 1];
        System.arraycopy(argList, 1, restList, 0, argList.length - 1);
        return new IntList(argList[0], IntList.of(restList));
    }
}


```