---
layout:     post
title:      "Shortest Unsorted Continuous Subarray"
subtitle:   " \"Algorithms\""
date:       2020-04-18 19:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

Example:

```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
````

Note:
1. Then length of the input array is in range [1, 10,000].
2. The input array may contain duplicates, so ascending order here means <=.


## Approach 1

```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        numsSorted = sorted(nums)
        n = len(nums)
        idx_start, idx_end = -1, -1
        i = 0
        while i < n:
            if numsSorted[i] != nums[i]:
                idx_start = i
                break
            i += 1
        if idx_start == -1:
            return 0
        i = n - 1
        while i >= 0:
            if numsSorted[i] != nums[i]:
                idx_end = i
                break
            i -= 1
        return idx_end - idx_start + 1
````

> Runtime: 340 ms, faster than 7.24% of Python3 online submissions for Shortest Unsorted Continuous Subarray.  
Memory Usage: 15 MB, less than 5.00% of Python3 online submissions for Shortest Unsorted Continuous Subarray.