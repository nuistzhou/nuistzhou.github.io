---
layout:     post
title:      "Notebook: use database index properly"
subtitle:   " \"\""
date:       2020-04-09 16:00:00
author:     "Ping"
header-img: "img/in-post/postgresql/postgresql.jpg"
catalog: true
tags:
    - Database
    - Notebook
---

> This is a notebook including what I have learned and summarized from the website: [use-the-index-luke](https://use-the-index-luke.com/), all figures are from here as well. 

## Chapter 1. Anatomy of an Index
### Leaf nodes
* Index entry: consists of indexed columns value and corresponding row ID, so it can quickly find the row in data table.  
* Index entries are stored in a block (the smallest database storage unit) and logically linked together using [Doubly Linked Lists](https://en.wikipedia.org/wiki/Doubly_linked_list).     
The hierarchy looks like this: Block(physical) -> Many Leaf Nodes -> Many Index Entries    
Which means in order to find a index, you have to find the right block, then right leaf node, and finally the needed index. So the database needs a second structure to find the left node quickly ----> Using B-Tree

### B-Tree
Here comes branch nodes layer, it is added on top of leaf nodes layer and stores the biggest indexed column value of a leaf node, and this grouping and generalization repeats until finally there is only one root node. 

See below figure about the logical structure.

![root-note_to_index-entry](https://use-the-index-luke.com/static/fig01_02_tree_structure.en.BdEzalqw.png)

This creates a balanced tree: B-Tree, which means the tree depth for each leaf node is the same.

Put as many entries as possible in each node level makes the database handling millions of index entries within just 4 or 5 tree depth.

### Slow Indexes - Part I

* Factor 1: leaf node chain. When there are multiple entries matched when searching the index, the DB must read further next leaf node to see if there are more matching entries. So not only Tree Traversal, but also Leaf Node Chain. But this only applies to non-unique column.

* Factor 2: Access the table. A single leaf node might need many db hits, and those hits might scattered across many table blocks, so IO bottleneck comes.


## Chapter 2. The Where Clause

### The Equality Operator
#### Primary Keys
* An index is created automatically on the Primary Key.
* When primary key is the only column used in WHERE clause, the clause cannot match multiple rows, then the DB doesn't need to follow the index leaf node. An negative example shown below, since the value 57 is not unique, the DB has to go further for each node to check and fetch the index: 

![follow-leaf_node_chain](https://use-the-index-luke.com/static/fig01_03_tree_traversal.en.niC7Q5jq.png)

* The uniqueness of the primary key also guarantees that no more than one table access. 

So, both of the Slow Indexes factors are not present for Where Clause == {Primary Key}.

#### Concatenated Indexes

An index of multiple columns, also known as composite index, combined index.

> The column order of the index does matter, it affects its usability, so has to be chosen carefully.

__Issue__: when query only part of the composite index, a full table scan is performed instead of using the index, this can be verified by the execution plan. This means that with table size grows continuously, the query time can increase tremendously. 

> A full table scan can be more appropriate when retrieving a large part of the table. This is because index lookup reads the data block by block, whereas the full table scan can read larger chunks at one time (multi-block read) and therefore need less fewer read operations.

The most important consideration when defining a composite index is how to choose the column ORDER so it can be used as often as possible.

Of course it is possible to create multiple indexes with each for one column or multiple columns that we need to query, but single-index solution is till preferred for two reasons: 1) save storage space 2) overhead maintenance for the second index. 3) fewer indexes, better insert, delete and update performance.

#### Slow Index - Part II

The __Query Optimizer__ is part of the db system and is used to transform the SQL statement into an execution plan. There are two types of optimizer: 1) Cost-based optimizer, it is based on the operations in use and the estimated row numbers, and finally the cost value serves as the benchmark for pick the "best" execution plan. 2) Rule-based optimizer, the execution plan is generated using a set of hard-coded rules, which means it is less flexible and barely used today.

Choosing the best execution plan based on the table's data distribution, so it is better to keep the database content's statistics up-to-date, so update the statistics after every index change.

### Functions

#### Case-Insensitive Search Using UPPER or LOWER

```sql
SELECT first_name, last_name, phone_number
  FROM employees
 WHERE UPPER(last_name) = UPPER('winand')
```
From above query, you might expect it to use the Index on `last_name` column, whereas it is not the case from the execution plan that a Full Table Scan is performed. The reason is that the db system sees the function as a black box here and would not use the Index as a consequence. The solution is to crate a `Function Based Index (FBI)` as shown below:

```sql
CREATE INDEX emp_up_name 
    ON employees (UPPER(last_name))
```

> PostgresSQL fully supports the __Indexes on Expressions__: meaning the index can not only on columns of the table, but also a function or scala expression computed from columns of the table, sees an example below:

```sql
CREATE INDEX test1_lower_col1_idx ON test1 (lower(col1));

SELECT * FROM test1 WHERE lower(col1) = 'value';
```

> SQL Server and MySQL however don't support function-based indexes, the workaround here is compute the columns and then they can be indexed afterwards.

#### User-defined Functions
