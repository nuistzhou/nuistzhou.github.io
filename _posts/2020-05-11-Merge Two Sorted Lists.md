---
layout:     post
title:      "Merge Two Sorted Lists"
subtitle:   " \"Algorithms\""
date:       2020-05-11 21:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

__Example__:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```


## Approach 1 

__Iteration 1__  

Intuitive way of finding the first element for new LinkedList and iterate both l1 and l2 to add the following nodes.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        head1 = l1
        head2 = l2
        if not l1:
            return l2
        if not l2:
            return l1
        if head1.val < head2.val:
            temp = head1
            l1 = l1.next
        else:
            temp = head2
            l2 = l2.next
        newHead = ListNode(next=temp)
        newHead = newHead.next
        while l1 and l2:
            if l1.val < l2.val:
                newHead.next = l1
                l1 = l1.next
            else:
                newHead.next = l2
                l2 = l2.next
            newHead = newHead.next
        if l1:
            newHead.next = l1
        elif l2:
            newHead.next = l2
        return temp
```
> Beats 70% online submissions already.


__Approach 2__

Using recursion is much more elegant.  

```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1 or not l2:
            return l1 or l2
        if l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```
>> Beats 89% submission.







