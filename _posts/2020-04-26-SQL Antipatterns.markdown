---
layout:     post
title:      "Notebook: SQL Antipatterns"
subtitle:   " \"\""
date:       2020-04-26 16:00:00
author:     "Ping"
header-img: "img/in-post/postgresql/postgresql.jpg"
catalog: true
tags:
    - Database
    - Notebook
---

> This is a notebook including what I have learned and summarized from the famous book \<SQL Antipatterns>.

# Logical Database Design Antipatterns

## Jaywalking

Definition: In a `Many-To-Many` situation, where one record in table 1 relates to many records in table 2, and also vice versa.    
For example:

```sql
CREATE TABLE Products (
product_id SERIAL PRIMARY KEY,
product_name VARCHAR(1000),
account_id VARCHAR(100), -- comma-separated list -- . . .
);
INSERT INTO Products (product_id, product_name, account_id) VALUES (DEFAULT, 'Visual TurboBuilder', '12,34');
```
One product might have multiple account (`account_id`) related to it, storing them as a array of string/ints might come to mind first when programming because it is fairly intuitive, however, some underlying problems come later when querying, updating, inserting, etc. since you have to parse the string array into a list of account_ids by either using string split functions or Regx, which damage the sql performance and also the functions extension possibilities in the future.

✅
Creating a new `Intersection` table solves the problem neatly.

```sql
CREATE TABLE Contacts (
        product_id  BIGINT UNSIGNED NOT NULL,
        account_id  BIGINT UNSIGNED NOT NULL,
        PRIMARY KEY (product_id, account_id),
        FOREIGN KEY (product_id) REFERENCES Products(product_id),
        FOREIGN KEY (account_id) REFERENCES Accounts(account_id)
);
      INSERT INTO Contacts (product_id, accont_id)
      VALUES (123, 12), (123, 34), (345, 23), (567, 12), (567, 34);
```

## Native Trees

Hierarchical data or treelike data, for example relationship of employees to managers.   

Alternative solutions:

### Path Enumeration
![pic](/img/in-post/sql_antipatterns/path_enumeration.jpg)

Drawbacks: data type VARCHAR has the length limit anyway, not ideal when tree depth is unknown(might unlimited). 

### Nested Sets
Complicated and not neat, ignore for now.

### Closure Table

![pic1](/img/in-post/sql_antipatterns/closure_table_1.jpg)

![pic2](/img/in-post/sql_antipatterns/closure_table_2.jpg)

THis way, the relationship is maintained in a separate table like what we did before for jaywalking. Even if the relations are deleted, the data it self still exists, for example in above case, the `comments` table.  

## ID Required

* when Artificial value that has no meaning in the domain modelled by the table is used as primary key, it is called `pseudokey`.

* Specify other domain related attribute as primary key or composite attributes as compound key when making more sense.

* Pseudokey is not mandatory, it is a convention for a lot of developers, but you don't have to follow it when it doesn't help.

## Keyless Entry

Using foreign keys instead of application code implementation to keep the `Referential Integrity`, avoiding the __Catch-22__ scenario.

```sql
CREATE TABLE Bugs (
-- . . .
reported_by BIGINT UNSIGNED NOT NULL,
status VARCHAR(20) NOT NULL DEFAULT 'NEW', FOREIGN KEY (reported_by) REFERENCES Accounts(account_id)
    ON UPDATE CASCADE
    ON DELETE RESTRICT, /*You cannot delete the account if it is used in Bugs table.*/
  FOREIGN KEY (status) REFERENCES BugStatus(status)
    ON UPDATE CASCADE
    ON DELETE SET DEFAULT /*Whenever a status value, any bugs with that status automatically reset to default.*/
);
```

## Entity Attribute Value (EAV)

Each entity in the table is a `attribute-value` pair, for example:

```sql
INSERT INTO IssueAttributes (issue_id, attr_name, attr_value)
  VALUES
    (1234, 'product', '1' ),
    (1234, 'date_reported', '2009-06-01' ),
    (1234, 'status', 'NEW' ),
    (1234, 'description', 'Saving does not work' ),
    (1234, 'reported_by', 'Bill' ),
    (1234, 'version_affected', '1.0'),
    (1234, 'severity', 'loss of functionality' ),
    (1234, 'priority', 'high');
```

In this way, number of columns doesn't grow even with new attributes introduced in, and NULL value columns that entities with inapplicable attributes can be avoided. It shares something with NoSQL, like the key-value pair.  



# Query Antipatterns

## Fear of Unknown(NULL)

> :white_square_button:   TODO: notes started on page 171 for this chapter, might need to add previous parts later. 

* Recommended to put a `non-null` constraint, and maybe set default values in case the column is omitted when inserting, but for sure, should be a logic value.

* Dynamic default: `COALESCE()` is a good function for this, since it returns the first non-null variable from a list of passed in variables.
