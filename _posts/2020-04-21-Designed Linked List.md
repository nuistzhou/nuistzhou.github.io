---
layout:     post
title:      "Designed Linked List"
subtitle:   " \"Algorithms\""
date:       2020-04-21 17:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Design your implementation of the linked list. You can choose to use the singly linked list or the doubly linked list. A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node. If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement these functions in your linked list class:

* get(index) : Get the value of the index-th node in the linked list. If the index is invalid, return -1.
* addAtHead(val) : Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
* addAtTail(val) : Append a node of value val to the last element of the linked list.
* addAtIndex(index, val) : Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
* deleteAtIndex(index) : Delete the index-th node in the linked list, if the index is valid.


Example:

```
Input: 
["MyLinkedList","addAtHead","addAtTail","addAtIndex","get","deleteAtIndex","get"]
[[],[1],[3],[1,2],[1],[1],[1]]
Output:  
[null,null,null,null,2,null,3]

Explanation:
MyLinkedList linkedList = new MyLinkedList(); // Initialize empty LinkedList
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);  // linked list becomes 1->2->3
linkedList.get(1);            // returns 2
linkedList.deleteAtIndex(1);  // now the linked list is 1->3
linkedList.get(1);            // returns 3
```

Constraints:

* 0 <= index,val <= 1000
* Please do not use the built-in LinkedList library.
* At most 2000 calls will be made to get, addAtHead, addAtTail,  addAtIndex and deleteAtIndex.


## Approach

```python
class Node:
    def __init__(self, x: float):
        self.val = x
        self.prev = None
        self.next = None

class MyLinkedList:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.size = 0
        self.head = None
        self.tail = None

    def get(self, index: int) -> int:
        """
        Get the value of the index-th node in the linked list. If the index is invalid, return -1.
        """
        if index >= self.size or index < 0:
            return -1
        else:
            node = self.getIndexNode(index)
            return node.val


    def addAtHead(self, val: int) -> None:
        """
        Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
        """
        newNode = Node(val)
        if self.head is None:
            self.head = newNode
            self.tail = newNode
        else:
            newNode.next = self.head
            self.head.prev = newNode
            self.head = newNode
        self.size += 1

    def addAtTail(self, val: int) -> None:
        """
        Append a node of value val to the last element of the linked list.
        """
        newNode = Node(val)
        if self.tail is None:
            self.head = newNode
            self.tail = newNode
        else:
            newNode.prev = self.tail
            self.tail.next = newNode
            self.tail = newNode
        self.size += 1
        

    def addAtIndex(self, index: int, val: int) -> None:
        """
        Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
        """
        if index == self.size:
            self.addAtTail(val)
        elif index == 0:
            self.addAtHead(val)
        elif index <= self.size - 1:
            indexNode = self.getIndexNode(index)
            newNode = Node(val)
            
            newNode.prev = indexNode.prev
            newNode.next = indexNode
            
            indexNode.prev.next = newNode      
            indexNode.prev = newNode

            self.size += 1

    def delHead(self):
        oldHead = self.head
        if self.size == 0:
            return
        elif self.size == 1:
            self.head = None
            self.tail = None
        else:
            oldHead.next.prev = None
            self.head = oldHead.next
        del oldHead

    def delTail(self):
        oldTail = self.tail
        if self.size == 0:
            return
        elif self.size == 1:
            self.head = None
            self.tail = None
        else:
            oldTail.prev.next = None
            self.tail = oldTail.prev
        del oldTail

    def deleteAtIndex(self, index: int) -> None:
        """
        Delete the index-th node in the linked list, if the index is valid.
        """
        if index < 0 or index >= self.size:
            return 
        elif index == 0:
            self.delHead()
        elif index == (self.size - 1):
            self.delTail()
        else:
            indexNode = self.getIndexNode(index)

            indexNode.prev.next = indexNode.next
            indexNode.next.prev = indexNode.prev
            del indexNode
        self.size -= 1
        
    def getIndexNode(self, idx: int) -> Node:
        tmp = self.head
        while idx > 0:
            tmp = tmp.next
            idx -= 1
        return tmp
```

> Beats 73% of Python3 submissions.

