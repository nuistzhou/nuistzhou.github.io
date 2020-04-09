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
    - Leetcode
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
Easiest logic but brute force way, time complexity of O(n^2)
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxProfit = 0
        for i in range(len(prices)-1):
            for j in range(i+1, len(prices)):
                maxProfit = max(prices[j] - prices[i], maxProfit)
        return maxProfit
```
> **Runtime**: Error: Time Limit Exceeded :x:   
This is because various test cases have been performed on the codes, and this approach works for small scale list, but will cause time out error for large ones like in this case, it failed on a list with 220K members, which make sense of course, because it will loop the list for 220K * 220K times, which is 480M, dangerous, huh? 

## Approach 2
Better solution with time complexity of O(n)
### Analysis

Take list [7, 1, 5, 3, 6, 4]  as an example.  
Iterating the list probably is a must for this question as far as I can see, but the problem is how to just find the highest selling and lowest buying in a turn in just one list iteration. Since selling has to be after the buying, it makes more sense to start iterating backwards. So, let's reverse the input list into [4, 6, 3, 5, 1, 7], and for each step, the price could be compared with the default highest selling price which is 0 by default, and replace it when positive, at the same time, compare the max profit (highest selling price - price) with the maxProfit so far. In the end, maxProfit should be result.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        pricesReversed = prices[::-1]
        highestSelling = 0 # In case of empty list
        maxProfit = 0 # Lowest profit should be 0 by default
        for price in pricesReversed:
            if price > highestSelling:
                highestSelling = price
            maxProfit = max(maxProfit, highestSelling - price)
        return maxProfit
```

> Runtime: 64 ms, faster than 62.71% of Python3 online submissions for Best Time to Buy and Sell Stock.  
Memory Usage: 15.3 MB, less than 5.75% of Python3 online submissions for Best Time to Buy and Sell Stock.   

No error, everything works fine.

