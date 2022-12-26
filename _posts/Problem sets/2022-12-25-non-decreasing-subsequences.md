layout: post
title: Non-Decreasing Subsequences
date: 2022-12-25
categories: [Python]
tags: [problem sets]
---

# Non-Decreasing Subsequences
We want to write a function that takes a list and returns a list of lists, where each individual list is a subsequence of the original input. And there is a condition: we only want the subsequences for which consecutive elements are nondecreasing. For example, [1, 3, 2] is a subsequence of [1, 3, 2, 4], but since 2 < 3, this subsequence would not be included in our result.

You may assume that the list passed in as s contains only nonnegative elements.

```python
def non_decrease_subseqs(s):
    """Assuming that S is a list, return a nested list of all subsequences
    of S (a list of lists) for which the elements of the subsequence
    are strictly nondecreasing. The subsequences can appear in any order.

    >>> seqs = non_decrease_subseqs([1, 3, 2])
    >>> sorted(seqs)
    [[], [1], [1, 2], [1, 3], [2], [3]]
    >>> non_decrease_subseqs([])
    [[]]
    >>> seqs2 = non_decrease_subseqs([1, 1, 2])
    >>> sorted(seqs2)
    [[], [1], [1], [1, 1], [1, 1, 2], [1, 2], [1, 2], [2]]
    """
    # recursion 1
    # if not s:
    #     return [[]]
    # else:
    #     res = []
    #     tmp = non_decrease_subseqs(s[1:])
    #     for i in range(len(tmp)):
    #         if tmp[i] and s[0] <= tmp[i][0]:
    #             res.append([s[0]] + tmp[i])
    #         elif  not tmp[i]:
    #             res.append([s[0]])
    #     return res + tmp

    # recursion 2, hard to think
    def subseq_helper(s, prev):
        if not s:
            return [[]]
        elif s[0] < prev:
            return subseq_helper(s[1:], prev)
        else:
            a = subseq_helper(s[1:], s[0])
            b = subseq_helper(s[1:], prev)
            return insert_into_all(s[0], a) + b
    return subseq_helper(s, 0)

def insert_into_all(item, nested_list):
    """Return a new list consisting of all the lists in nested_list,
    but with item added to the front of each. You can assume that
     nested_list is a list of lists.

    >>> nl = [[], [1, 2], [3]]
    >>> insert_into_all(0, nl)
    [[0], [0, 1, 2], [0, 3]]
    """
    return [[item] + x for x in nested_list]
```