---
layout:     post
title:      "LeetCode: Search Insert Position"
subtitle:   " \"Algorithms\""
date:       2020-04-09 10:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:

Input: [1,3,5,6], 5
Output: 2 

Example 2:

Input: [1,3,5,6], 2
Output: 1

Example 3:

Input: [1,3,5,6], 7
Output: 4

Example 4:

Input: [1,3,5,6], 0
Output: 0

## Approach 1
A typical binary search problem.

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if target > nums[mid]:
                left = mid + 1
            elif target < nums[mid]:
                right = mid - 1
            else:
                return mid
        if target > nums[left]:
            return (left + 1)
        return left 
```
Runtime: 44 ms, faster than 91.67% of Python3 online submissions for Search Insert Position.   
Memory Usage: 14.4 MB, less than 5.97% of Python3 online submissions for Search Insert Position.

However, this solution doesn't handle a given empty list, here is a refined version and also more time efficient:

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums)
        while low < high:
            mid = (low + high) // 2
            if target > nums[mid]:
                low = mid + 1
            else:
                high = mid
        return low
```

Runtime: 40 ms, faster than 98.06% of Python3 online submissions for Search Insert Position.
Memory Usage: 14.6 MB, less than 5.97% of Python3 online submissions for Search Insert Position.