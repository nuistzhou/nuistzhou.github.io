---
layout:     post
title:      "LeetCode: Best Time to Buy and Sell Stock"
subtitle:   " \"Algorithms\""
date:       2020-04-09 10:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
---

## Description
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:

Input: [7,1,5,3,6,4]  
Output: 5  
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.  

Example 2:

Input: [7,6,4,3,1]
Output: 0  
Explanation: In this case, no transaction is done, i.e. max profit = 0.


## Approach 1
Easiest but brute force way, time complexity of O(n^2)
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxProfit = 0
        for i in range(len(prices)-1):
            for j in range(i+1, len(prices)):
                maxProfit = max(prices[j] - prices[i], maxProfit)
        return maxProfit
```
> **Runtime**: 60 ms
