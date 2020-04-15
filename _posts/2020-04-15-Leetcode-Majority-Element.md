---
layout:     post
title:      "LeetCode: Majority Element"
subtitle:   " \"Algorithms\""
date:       2020-04-15 16:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![demo](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```


## Approach 1
```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:    
    pascal = [[1] * (i + 1) for i in range(numRows)]
    for i in range(numRows):
        for j in range(1, i):
            pascal[i][j] = pascal[i-1][j-1] + pascal[i-1][j]
    return pascal
```
This is the most elegant approach so far as I can think of.  
It constructs a array filled with default value 1, then iterate row by row, column by column, to calculate the every element value except the most left/right ones according to the Pascal formula.

> Runtime: 32 ms, faster than 28.66% of Python3 online submissions for Pascal's Triangle.
Memory Usage: 13.8 MB, less than 7.14% of Python3 online submissions for Pascal's Triangle.

Not fast enough though.  😿 

## Approach 2

Instead of initializing a default array at the beginning, this solution creates arrays row by row.

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        rowArray = [1]
        array = []
        for i in range(numRows):
            array.append(rowArray)
            rowArray = [1] + [rowArray[j] + rowArray[j + 1] for j in range(len(rowArray) - 1)] + [1]
        return array
```

>Runtime: 24 ms, faster than 89.07% of Python3 online submissions for Pascal's Triangle.  
Memory Usage: 14 MB, less than 7.14% of Python3 online submissions for Pascal's Triangle.

A great time performance improvement. 😸   
Time complexity is O(nˆ2)