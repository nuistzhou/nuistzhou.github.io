---
layout:     post
title:      "Python Tricks"
subtitle:   " \"Good to know\""
date:       2019-04-18 9:00:00
author:     "Ping"
header-img: "img/in-post/tutorial_pythonpath/post-head-python.jpg"
catalog: true
tags:
    - Python
---

## Sort a Python dictionary by value
Making use of the `sorted()` function, pass in a callable function/object to the `key` parameter to make comparison.

### Using Lambda specify the value (index 1)
```python
d = {'a': 4, 'b': 1, 'c': 10, 'd': 2}
sorted(d.items(), key=lambda x:x[1])
```
> [('b', 1), ('d', 2), ('a', 4), ('c', 10)]


### Using Operator specify the value (index 1)

```python
import operator
d = {'a': 4, 'b': 1, 'c': 10, 'd': 2}
sorted(d.items(), key=operator.itemgetter(1))
```
> [('b', 1), ('d', 2), ('a', 4), ('c', 10)]


## Enable Jupyter notebook code autocomplete ('Intellisense')

Just add the line `%config IPCompleter.greedy=True` at the top of the nb file.  
Then, you should be able to see available methods when pressing the **TAB**.
