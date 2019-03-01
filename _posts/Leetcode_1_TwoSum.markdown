---
layout:     post
title:      "Two Sum"
subtitle:   " \"Leetcode\""
date:       2019-03-01 20:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.png"
catalog: true
tags:
    - Technology
    - Algorithm
---

# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Example:


Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].



```python
class Solution():
    def twoSum(self, nums: 'list(int)', target: int) -> 'list(int)':
        for i in range(len(nums)):
            for j in range(len(nums)):
                if i != j and nums[i] + nums[j] == target:
                    return [i, j]
```


```python
solution = Solution()
nums = [1,2,3,8,9]
target = 10
i, j = solution.twoSum(nums, target)
print ("The sum of {0} element and {1} element is {2}".format(i, j, target))
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-9af58c512eec> in <module>
    ----> 1 solution = Solution()
          2 nums = [1,2,3,8,9]
          3 target = 10
          4 i, j = solution.twoSum(nums, target)
          5 print ("The sum of {0} element and {1} element is {2}".format(i, j, target))


    NameError: name 'Solution' is not defined



```python

```
