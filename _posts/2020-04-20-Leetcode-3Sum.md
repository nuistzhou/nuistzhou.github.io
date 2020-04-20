---
layout:     post
title:      "3Sum"
subtitle:   " \"Algorithms\""
date:       2020-04-20 12:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```


## Approach 1

__Iteration 1__
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        allTriplets = set()
        positive = [n for n in nums if n > 0]
        negative = [n for n in nums if n<0]
        zero = [n for n in nums if n==0]
        positiveSet = set(positive)
        negativeSet = set(negative)
        
        # zero triplet
        if len(zero) > 2:
            allTriplets.add((0, 0, 0))
        # one zero triplet
        if len(zero) > 0:
            for p in positiveSet:
                if -p in negativeSet:
                    allTriplets.add((p, 0, -p))
        # two positive + one negative
        for i in range(len(positive)):
            for j in range(i+1, len(positive)):
                if -(positive[i] + positive[j]) in negativeSet:
                    allTriplets.add((positive[i], positive[j], -(positive[i] + positive[j])))
        # one positive + two negative
        for i in range(len(negative)):
            for j in range(i+1, len(negative)):
                if -(negative[i] + negative[j]) in positiveSet:
                    allTriplets.add((negative[i], negative[j], -(negative[i] + negative[j])))
        return allTriplets          
```
Result: ❌   
This is the most intuitive solution which separates the problem into four different cases, and deal with them individually:
* [0, 0, 0]
* [positive, 0, negative] # positive + negative == 0
* [positive1, positive2, negative] # positive1 + positive2 + negative == 0
* [positive, negative1, negative2] # positive + negative1 + negative2 == 0

The time complexity is O(nˆ2).

However, above solution gives an exception for test case:  
```         
[-4,-2,1,-5,-4,-4,4,-2,0,4,0,-2,3,1,-5,0]       
```
with output: 
```
[[4,0,-4],[4,1,-5],[0,0,0],[3,1,-4],[-2,-2,4],[1,1,-2],[1,3,-4],[1,4,-5]]   
```
and expected: 
```
[[-5,1,4],[-4,0,4],[-4,1,3],[-2,-2,4],[-2,1,1],[0,0,0]]
```
Obviously, there were duplicated triplets.  
Actually, I didn't expect this, because a `set(tuple())` should have solved this, but seems identical tuples means they need to be exact same, like:
(1,2,3) is different from (3,2,1).  

 We can easily solve this by sorting both `positive` and `negative` lists at the beginning, and each time when found a triplet, always add it into the triplets set in the order of `(positive, positive/negative), negative)`.     

 See an improved solution below:

__Iteration 2__   
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        allTriplets = set()
        positive = sorted([n for n in nums if n > 0])
        negative = sorted([n for n in nums if n<0])
        zero = [n for n in nums if n==0]
        positiveSet = set(positive)
        negativeSet = set(negative)
        
        # zero triplet
        if len(zero) > 2:
            allTriplets.add((0, 0, 0))
        # one zero triplet
        if len(zero) > 0:
            for p in positiveSet:
                if -p in negativeSet:
                    allTriplets.add((p, 0, -p))
        # two positive + one negative
        for i in range(len(positive)):
            for j in range(i+1, len(positive)):
                if -(positive[i] + positive[j]) in negativeSet:
                    allTriplets.add((positive[i], positive[j], -(positive[i] + positive[j])))
        # one positive + two negative
        for i in range(len(negative)):
            for j in range(i+1, len(negative)):
                if -(negative[i] + negative[j]) in positiveSet:
                    allTriplets.add((-(negative[i] + negative[j]), negative[i], negative[j]))
        return list(allTriplets)          
```
Result:  ✅
> Runtime: 436 ms, faster than 98.03% of Python3 online submissions for 3Sum.   
Memory Usage: 17.4 MB, less than 13.57% of Python3 online submissions for 3Sum.
Next challenges:
