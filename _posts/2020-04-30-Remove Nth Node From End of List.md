---
layout:     post
title:      "Remove Nth Node From End of List"
subtitle:   " \"Algorithms\""
date:       2020-04-30 07:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given a linked list, remove the n-th node from the end of list and return its head.

__Example__:

```
Given linked list: 1->2->3->4->5, and n = 2.  

After removing the second node from the end, the linked list becomes 1->2->3->5.
```


__Note__:

Given n will always be valid.

__Follow up__:

Could you do this in one pass?

## Approach 1 

__Iteration 1__  

Analysis: Brute Force way

Removing the Nth node from the end, means the (L - n + 1)th node from the head of the linked list, where L is the length of the linked list.   

So there has to be 2 steps:   
1. Iterate thorough the linked list once and count its length;
2. Iterate it over again, modify the (L - n)th node's `next` value and point it to (L - n + 2)th node.

A time complexity of O(N) where N is the length of the linked list.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        l = 0
        newHead = head
        while newHead:
            newHead = newHead.next
            l += 1
        i = 1
        dummy = head
        while head:
            if i == (l - n):
                head.next = head.next.next
                head = head.next
                break
            else:
                head = head.next
            i += 1
        if n == l:
            return dummy.next
        return dummy      
```
> Beats 64% online submissions already.


__Iteration 2__

An improved version of using two pointer technique is to initialize two pointers, with one starting at the head of the linked list and the second pointer at (head + n)th position. Finally, when the second pointer reaches the end of the linked list, the first pointer would be positioned at the nth position from the end, because distance between two pointers stays `n` all the time.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode()
        dummy.next = head
        firstPointer = dummy
        secondPointer = dummy
        # Initialize the pointer at head + n position
        while n+1 > 0:
            secondPointer = secondPointer.next
            n -= 1
        #Iterate until the second pointer reaches the end of the linked list.
        while secondPointer:
            firstPointer = firstPointer.next
            secondPointer = secondPointer.next
        # re-link the (n-1)th node to (n+1)th node
        firstPointer.next = firstPointer.next.next
        return dummy.next
```





