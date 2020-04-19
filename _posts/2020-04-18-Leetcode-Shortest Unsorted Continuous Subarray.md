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

__Iteration 1__
```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        numsSorted = sorted(nums)
        n = len(nums)
        idx_start, idx_end = 0, n - 1
        i = 0
        while i < n:
            if numsSorted[i] != nums[i]:
                idx_start = i
                break
            i += 1
        i = n - 1
        while i >= 0:
            if numsSorted[i] != nums[i]:
                idx_end = i
                break
            i -= 1
        return idx_end - idx_start + 1
````
Result: ❌  
Above codes work well for all test cases provided by Leetcode except one boundary case: array `nums` is already sorted in ascending order, so let's put a check before the two loops to avoid this boundary case.

__Iteration 2__
```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        numsSorted = sorted(nums)
        n = len(nums)
        idx_start, idx_end = 0, n - 1
        i = 0
        if numsSorted == nums:
            return 0
        while i < n:
            if numsSorted[i] != nums[i]:
                idx_start = i
                break
            i += 1
        i = n - 1
        while i >= 0:
            if numsSorted[i] != nums[i]:
                idx_end = i
                break
            i -= 1
        return idx_end - idx_start + 1
````
Result: ✅
> Runtime: 320 ms, faster than 7.71% of Python3 online submissions for Shortest Unsorted Continuous Subarray.
Memory Usage: 15.2 MB, less than 5.00% of Python3 online submissions for Shortest Unsorted Continuous Subarray.

It is worthy note that Leetcodes doesn't really give stable runtime valuations upon multiple submissions, with above codes, result ranges from 7% to 90+%. 