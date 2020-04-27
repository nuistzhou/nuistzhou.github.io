---
layout:     post
title:      "Linked List Cycle"
subtitle:   " \"Algorithms\""
date:       2020-04-21 19:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.


Example 1:

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```
![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

Example 2:

```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```
![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

Example 3:

```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

## Approach

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if head is None or head.next is None:
            return False
        pointer = head
        fasterPointer = head.next
        while pointer != fasterPointer:
            if fasterPointer is None or fasterPointer.next is None:
                return False
            pointer = pointer.next
            fasterPointer = fasterPointer.next.next 
        return True
```
> Beats 86% Python submissions.

The main idea is to use two pointers just like two runners racing, one running slower than the other, for example, one goes 1 step per iteration while the other goes 2 steps, the slower runner would finally 