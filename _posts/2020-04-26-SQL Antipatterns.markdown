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

# Query Antipatterns

## Fear of Unknown(NULL)

> :white_square_button:   TODO: notes started on page 171 for this chapter, might need to add previous parts later. 

* Recommended to put a `non-null` constraint, and maybe set default values in case the column is omitted when inserting, but for sure, should be a logic value.

* Dynamic default: `COALESCE()` is a good function for this, since it returns the first non-null variable from a list of passed in variables.
