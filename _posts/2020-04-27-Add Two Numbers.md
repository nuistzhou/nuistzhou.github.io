---
layout:     post
title:      "Add Two Numbers"
subtitle:   " \"Algorithms\""
date:       2020-04-27 14:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example 1:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## Approach

__Iteration 1__
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        i, j = 0, 0
        a, b = 0, 0
        while l1:
            a += l1.val*(10**i)
            i += 1
            l1 = l1.next
        while l2:
            b += l2.val*(10**j)
            j += 1
            l2 = l2.next
        c = a + b
        l3 = ListNode(c%10)
        c //= 10
        pointer = l3
        while c != 0:
            pointer.next = ListNode(c%10)
            pointer = pointer.next
            c //= 10
        return l3
```

> Beat 39.72% submissions.
Time complexity of O(M + N + max(M, N)). M, N is the two Linked List length respectively.

It can be improved using less space and time, and more clean way by generating new node in every iteration of both Linked List simultaneously. 

Here is a brief explanation:
```
For Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
```
1. From units digit, `2 + 5 => 7`, with its remainder (7%10) remains 7, as the new units digit for the sum number (`tempSum`)which is __7__ so far, but since it doesn't contribute to the higher digits, we would omit it.

2. For tens digit, `4 + 6 => 10`, with its remainder (10%10) as `0`, as the new tens digit for the sum number, but keep in mind, this step also contributes 1 plus in the one digit higher unit (hundreds unit), we keep it in variable `tempSum`= 1 by doing dividing by 10.

3. For hundreds unit, `3 + 4 => 7`, AND, don't forget the `1` from last step, so should be `8`. Since it is less than 10 and therefore doesn't adding to higher place, we omit it as well like what we did before by doing dividing by 10.

Finally, we got added numbers' linked list: `7 -> 0 -> 8`  

__Iteration 2__

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        tempSum = 0
        # The way to store the linked list head
        l3 = tempNode = ListNode(0)
        while l1 or l2 or tempSum:
            if l1:
                tempSum += l1.val
                l1 = l1.next
            if l2:
                tempSum += l2.val
                l2 = l2.next
            tempNode.next = ListNode(tempSum%10)
            tempNode = tempNode.next
            tempSum //=10
        return l3.next
```

>  Beats 99.53% submissions. With time complexity of O(N), N here is the max(len(l1), len(l2)).
