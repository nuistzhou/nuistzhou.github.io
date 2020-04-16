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
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1: 
```
Input: [3,2,3]
Output: 3
```

Example 2:
```
Input: [2,2,1,1,1,2,2]
Output: 2
```


## Approach 1
```python
import collections

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        c = collections.Counter(nums)
        return c.most_common(1)[0][0]
```
By taking advantage of `Collections` module, we could solve this problem with just 2 lines of codes, well, it is kind of cheating for a test, but works perfectly in a real project.

> Runtime: 168 ms, faster than 91.15% of Python3 online submissions for Majority Element.  
Memory Usage: 15.2 MB, less than 7.14% of Python3 online submissions for Majority Element


## Approach 2

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        d = dict()
        l = len(nums)
        for num in nums:
            if num not in d.keys():
                d[num] = 1
            elif d[num] >= l//2:
                return num
            else:
                d[num] += 1
        return nums[0]
```
This solution follows the simplest logic of counting occurrences for each unique element, until any of them reach half number of the array length. 

> Runtime: 188 ms, faster than 29.21% of Python3 online submissions for Majority Element.  
Memory Usage: 15.2 MB, less than 7.14% of Python3 online submissions for Majority Element.

## Approach 3

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums = sorted(nums, reverse=True)
        return nums[len(nums//2)]
````


>Runtime: 164 ms, faster than 96.25% of Python3 online submissions for Majority Element.  
Memory Usage: 15.3 MB, less than 7.14% of Python3 online submissions for Majority Element.