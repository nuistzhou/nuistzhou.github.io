---
layout:     post
title:      "LeetCode: Two Sum"
subtitle:   " \"Algorithms\""
date:       2019-02-28 20:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---


Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.


Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].


# Approach 1
```python
from typing import List
class Solution():
    def twoSum(self, nums: 'list(int)', target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
            	if nums[i] + nums[j] == target:
                    return [i, j]                
solution = Solution()
nums = [1,2,3,8,9]
target = 10
i, j = solution.twoSum(nums, target)
print ("The sum of {0} element and {1} element is {2}".format(i, j, target))
```
> **Runtime**: 9484 ms, faster than 5.01% of Python3 online submissions for Two Sum.
> **Memory Usage**: 13.7 MB, less than 34.08% of Python3 online submissions for Two Sum.

# Approach 2
