---
layout:     post
title:      "LeetCode: Move Zeros"
subtitle:   " \"Algorithms\""
date:       2020-04-16 16:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
````

Note:

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.


## Approach 1
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i = 0
        while True:
            if 0 in nums:
                nums.remove(0)
                i += 1
            else:
                break
        nums += [0] * i
````
Keep removing and counting all 0 from list, then add those number of 0 back to the list. The simplest logic, but not efficient, because it has to check if there is 0 left in the array every time, and this check has time complexity of O(N) and method remove has the same complexity.

> Runtime: 188 ms, faster than 17.12% of Python3 online submissions for Move Zeroes.  
Memory Usage: 14.9 MB, less than 5.97% of Python3 online submissions for Move Zeroes.


## Approach 2
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        counter = 0
        for i in range(len(nums)):
            if nums[i-counter] == 0:
                nums.pop(i-counter)
                counter += 1
        nums += [0] * counter
````
>Runtime: 52 ms, faster than 52.77% of Python3 online submissions for Move Zeroes.  
Memory Usage: 15 MB, less than 5.97% of Python3 online submissions for Move Zeroes.

Time efficiency improved a lot, because we omitted the `if element in nums` check in line 9, but the overall logic stays the same.



