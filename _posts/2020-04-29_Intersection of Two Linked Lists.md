---
layout:     post
title:      "Intersection of Two Linked Lists"
subtitle:   " \"Algorithms\""
date:       2020-04-29 08:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)



Example 1:

![img2](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3    
Output: Reference of the node with value = 8   
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```
![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

Example 2:

![img3](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1  
Output: Reference of the node with value = 2  
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

Example 3:

![img4](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

Example 4:

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

Notes:

* If the two linked lists have no intersection at all, return null.
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O(n) time and use only O(1) memory.


## Approach 1 

Analysis: Brute Force way

Iterate the first linked list A, for each iteration, iterating the second linked list B thoroughly, compare if there is a intersection.     
Time complexity O(MN) where M, N is the A's and B's length respectively.

This might cause time error for large linked list. Let's consider a better way by reducing the time complexity to O(M + N).

## Approach 2

Iterating the first linked list A and store every node into a Set object `setA`, then go through the second linked list B, and check if any node is within `setA`.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        headA_set = set()
        while headA:
            headA_set.add(headA)
            headA = headA.next
        while headB:
            if headB in headA_set:
                return headB
            headB = headB.next
        return None
```

> This solution could already beat around 80% online submissions on Leetcode.

Next, let's think about `Two Pointers` way.

## Approach 3

Suppose linked list `A` and linked list `B` intersects at node `x`, and the identical list before that is `M` and `N` respectively, the shared part (excluding node x)after is `O`, like this:   

A: M + x + O  
B: N + x + O

If we would like to reach the intersection node `x` at same time for both lists, it is a great idea to append the list to the end of the other, leading to:    

A:  M + x + O + N + `x` + O  
B:  N + x + O + M + `x` + O   

Then if we iterate those two new lists, we should be able to reach the intersection node `x` at the same time, because they share (M + x + O + N) part at the beginning.

See implementation below:

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        a = headA
        b = headB
        while a != b:
            if a:
                a = a.next
            else:
                a = headB
            if b:
                b = b.next
            else:
                b = headA
        return a
```
What if two linked lists don't intersect at all? Like this:

A: M   
B: N   

Appending the list to the end of the other would still work? Let's see:  

A: M + N  
B: N + M

A and B will have same length and can be iterated through within same time, both last element.next point to `None`, making the function returns None which is expected for this non-intersecting situation.

> Beats 91% submissions. Time complexity of O(M + N), where M and N is the list's length respectively.



