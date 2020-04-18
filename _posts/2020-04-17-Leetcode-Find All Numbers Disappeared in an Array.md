---
layout:     post
title:      "LeetCode: Find All Numbers Disappeared in an Array"
subtitle:   " \"Algorithms\""
date:       2020-04-17 10:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
````


## Approach 1

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        return set(range(1,len(nums)+1)).difference(set(nums))
````

> Runtime: 352 ms, faster than 95.31% of Python3 online submissions for Find All Numbers Disappeared in an Array.  
Memory Usage: 25.3 MB, less than 7.14% of Python3 online submissions for Find All Numbers Disappeared in an Array.

By taking advantage of Python set data structure, it is the easiest solution and Python set difference built-in function has time complexity of O(len(a)). 
