---
layout:     post
title:      "Notebook: use databse index properly"
subtitle:   " \"\""
date:       2020-04-09 16:00:00
author:     "Ping"
header-img: "img/in-post/postgresql/postgresql.jpg"
catalog: true
tags:
    - Database
    - Notebook
---

> This is a notebook including what I have read and summarized from the website: [use-the-index-luke](https://use-the-index-luke.com/)

## Chapter 1. Anatomy of an Index
### Leaf nodes
* Index entry: consists of indexed columns value and corresponding row ID, so it can quickly find the row in data table.  
* Index entries are stored in a block (the smallest database storage unit) and logically linked together using [Doubly Linked Lists](https://en.wikipedia.org/wiki/Doubly_linked_list).     
The hierarchy looks like this: Block(physical) -> Many Leaf Nodes -> Many Index Entries    
Which means in order to find a index, you have to find the right block, then right leaf node, and finally the needed index. So the database needs a second structure to find the right index entry ----> Using the balanced tree: B-Tree

### B-Tree
Here comes branch nodes layer, it is added on top of leaf nodes layer and stores the biggest indexed column value of a leaf node, and this grouping and generalization repeats until finally there is only one root node. 

See below figure about the logical structure.

![root-note_to_index-entry](/img/in-post/database_index/fig01_02_tree_structure.png)

