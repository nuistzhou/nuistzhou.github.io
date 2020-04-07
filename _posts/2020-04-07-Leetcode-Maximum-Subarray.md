---
layout:     post
title:      "LeetCode: Maximum Subarray"
subtitle:   " \"Algorithms\""
date:       2020-04-07 16:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
---

## Description
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],  
Output: 6  
Explanation: [4,-1,2,1] has the largest sum = 6.  

## Analysis
According to [Kadane's algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem), iterate the nums list, for each step _i_, computes the sum ending and including position _i_, stores into a temp variable like _maxEndingHere_, and evalulate if it will postively(+) contribute to next step's sum.


## Approach 1
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        maxEndingHere = maxOverall = nums[0]
        for num in nums[1:]:
            maxEndingHere = max(num, maxEndingHere + num) # If adding maxEndingHere to current num leads to a smaller number, a new start begins
            maxOverall = max(maxOverall, maxEndingHere)
        return maxOverall
```
> **Runtime**: Runtime: 64 ms, faster than 80.85% of Python3 online       submissions for Maximum Subarray.  
Memory Usage: 14.4 MB, less than 5.69% of Python3 online submissions for Maximum Subarray.

The result above looks okay, it has a time complexity of O(n) and space complexity of O(1).

